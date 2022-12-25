# React Suspense Notes 

## 1. Simple Data-fetching 

- **Here's the basic idea of React Suspense**:
- A <Suspense> component that lets you “wait” for some code to load and declaratively specify a loading state (like a spinner) while we’re waiting. **Example:**

```javascript
function Component() {
  if (data) {
    return <div>{data.message}</div>
  }
  throw promise
  // React with catch this, find the closest "Suspense" component
  // and "suspend" everything from there down from rendering until the
  // promise resolves.
  // 🚨 THIS "API" IS LIKELY TO CHANGE
}

ReactDOM.createRoot(rootEl).render(
  <React.Suspense fallback={<div>loading...</div>}>
    <Component />
  </React.Suspense>,
)

```

- Where the `data` and `promise` values are coming from all
depends on how you implement things.

- Imagine when your app loads, you need some data before you can show anything
useful. Typically we want to put the data loading requirements right in the
component that requires the data, via something like this:

```javascript
React.useEffect(() => {
  let current = true
  setState({status: 'pending'})
  doAsyncThing().then(
    p => {
      if (current) setState({pokemon: p, status: 'success'})
    },
    e => {
      if (current) setState({error: e, status: 'error'})
    },
  )
  return () => (current = false)
}, [pokemonName])

// render stuff based on the state
```

- The best approaches to using Suspense involve kicking off the
request for the data as soon as you have the information you need for the
request. This is called the "Render as you fetch" approach.

- **Final code of lesson 1.** This handles error handler. 
```jsx
let pokemon
let pokemonPromise = fetchPokemon('pikachu').then(p => (pokemon = p))

function PokemonInfo() {
  if (!pokemon) {
    throw pokemonPromise
  }
  return (
    <div>
      <div className="pokemon-info__img-wrapper">
        <img src={pokemon.image} alt={pokemon.name} />
      </div>
      <PokemonDataView pokemon={pokemon} />
    </div>
  )
}

function App() {
  return (
    <div className="pokemon-info-app">
      <div className="pokemon-info">
        <React.Suspense fallback={<div>Loading Pokemon...</div>}>
          <PokemonInfo />
        </React.Suspense>
      </div>
    </div>
  )
}

export default App

```

## 2. Render as you fetch

- Here's the ultimate goal we're looking
for: https://twitter.com/kentcdodds/status/1191922859762843649

- Get the data **as soon as you have the information you need**
for the data. 
  - This sounds obvious, but if you think about it, how often do you
have a component that requests data once it's been mounted. There's a few
milliseconds between the time you click "go" and the time that component is
mounted... Unless that component's code is **lazy-loaded**.

- "Render as you fetch" is intended to fix this problem because you can make the
request for the code and the data at the same time.

- Final code should look something like this: 

```jsx

function App() {
  const [pokemonName, setPokemonName] = React.useState(null)
  const [pokemonResource, setPokemonResource] = React.useState(null)

  function handleSubmit(newPokemonName) {
    setPokemonName(newPokemonName)
    setPokemonResource(createPokemonResource(newPokemonName))
  }

return (
    <div className="pokemon-info-app">
      <PokemonForm onSubmit={handleSubmit} />
      <hr />
      <div className="pokemon-info">
        {pokemonResource ? (
          <ErrorBoundary>
            <React.Suspense
              fallback={<PokemonInfoFallback name={pokemonName} />}
            >
              <PokemonInfo pokemonResource={pokemonResource} />
            </React.Suspense>
          </ErrorBoundary>
        ) : (
          'Submit a pokemon'
        )}
      </div>
    </div>
  )
}

export default App

```

## 3. useTransition for improved loading states

- When a component suspends, it's literally telling React: "Don't render any
updates at all from the suspense component on down until I'm ready to roll."

- And here's how it looks like: 

```javascript
const SUSPENSE_CONFIG = {timeoutMs: 4000}

function Component() {
  const [startTransition, isPending] = React.useTransition(SUSPENSE_CONFIG)
  // etc...

  function handleClick() {
    // do something that triggers some interum state change we want to
    // happen before suspending starts
    startTransition(() => {
      // do something that triggers a suspending component to render
    })
  }

  // if needed, you can use the `isPending` boolean to display a loading spinner
  // or similar
}
```

- React Suspense with Concurrent mode comes with a default optimization that is optimistic in that it waits a tiny bit for your suspending promise to resolve before making any DOM updates. But this can make the app feel unresponsive for some use cases. 

- The experimental useTransition hook from React gives us more fine-grained control over the timing as well as the ability to show a pending state. Let's try that out here.

## 4. Cache resources

- Caching is a really hard problem, but it's important for good user experiences to make the app snappy, especially when you know that the data you're showing to the user is unchanged on the server. 

- similar for this exercise:

```javascript
const promiseCache = {}
function MySuspendingComponent({value}) {
  let resource = promiseCache[value]
  if (!resource) {
    resource = doAsyncThing(value)
    promiseCache[value] = resource // <-- this is very important
  }
  return <div>{resource.read()}</div>
}
```

- Final solution: 

```javascript
function App() {
  const [pokemonName, setPokemonName] = React.useState('')
  const [startTransition, isPending] = React.useTransition(SUSPENSE_CONFIG)
  const [pokemonResource, setPokemonResource] = React.useState(null)

  function handleSubmit(newPokemonName) {
    setPokemonName(newPokemonName)
    startTransition(() => {
      setPokemonResource(getPokemonResource(newPokemonName))
    })
  }

  return (
    <div className="pokemon-info-app">
      <PokemonForm onSubmit={handleSubmit} />
      <hr />
      <div className={`pokemon-info ${isPending ? 'pokemon-loading' : ''}`}>
        {pokemonResource ? (
          <ErrorBoundary>
            <React.Suspense
              fallback={<PokemonInfoFallback name={pokemonName} />}
            >
              <PokemonInfo pokemonResource={pokemonResource} />
            </React.Suspense>
          </ErrorBoundary>
        ) : (
          'Submit a pokemon'
        )}
      </div>
    </div>
  )
}
```

## 5. Suspense Image

- Now that we know how to preload images, we can create a custom <Img /> component which suspends until the image has been loaded into the browser cache. 
- This way we avoid issues where contents bounce around when the image is loads and ensure that there aren't consistency issues with the data and the image that's displayed.

- Suspense can help us with this too! Luckily for us, we can pre-load images into the browser's cache using the following code:

```javascript
function preloadImage(src) {
  return new Promise(resolve => {
    const img = document.createElement('img')
    img.src = src
    img.onload = () => resolve(src)
  })
}
```

- Final code: 

```javascript
function getPokemonResource(name) {
  const lowerName = name.toLowerCase()
  let resource = pokemonResourceCache[lowerName]
  if (!resource) {
    resource = createPokemonResource(lowerName)
    pokemonResourceCache[lowerName] = resource
  }
  return resource
}

function createPokemonResource(pokemonName) {
  return createResource(() => fetchPokemon(pokemonName))
}

function App() {
  const [pokemonName, setPokemonName] = React.useState('')
  const [startTransition, isPending] = React.useTransition(SUSPENSE_CONFIG)
  const [pokemonResource, setPokemonResource] = React.useState(null)

  function handleSubmit(newPokemonName) {
    setPokemonName(newPokemonName)
    startTransition(() => {
      setPokemonResource(getPokemonResource(newPokemonName))
    })
  }

  return (
    <div className="pokemon-info-app">
      <PokemonForm onSubmit={handleSubmit} />
      <hr />
      <div className={`pokemon-info ${isPending ? 'pokemon-loading' : ''}`}>
        {pokemonResource ? (
          <ErrorBoundary>
            <React.Suspense
              fallback={<PokemonInfoFallback name={pokemonName} />}
            >
              <PokemonInfo pokemonResource={pokemonResource} />
            </React.Suspense>
          </ErrorBoundary>
        ) : (
          'Submit a pokemon'
        )}
      </div>
    </div>
  )
}
```

## 6. Suspense with a custom hook

- React Hooks are amazing. Combine them with React Suspense, and you get some
really awesome APIs.

```javascript
function usePokemonResource(pokemonName) {
  const [pokemonResource, setPokemonResource] = React.useState(null)
  const [startTransition, isPending] = React.useTransition(SUSPENSE_CONFIG)

  React.useEffect(() => {
    if (!pokemonName) {
      return
    }
    startTransition(() => {
      setPokemonResource(getPokemonResource(pokemonName))
    })
  }, [pokemonName, startTransition])

  return [pokemonResource, isPending]
}

function App() {
  const [pokemonName, setPokemonName] = React.useState('')

  const [pokemonResource, isPending] = usePokemonResource(pokemonName)

  function handleSubmit(newPokemonName) {
    setPokemonName(newPokemonName)
  }

  return (
    <div className="pokemon-info-app">
      <PokemonForm onSubmit={handleSubmit} />
      <hr />
      <div className={`pokemon-info ${isPending ? 'pokemon-loading' : ''}`}>
        {pokemonResource ? (
          <ErrorBoundary>
            <React.Suspense
              fallback={<PokemonInfoFallback name={pokemonName} />}
            >
              <PokemonInfo pokemonResource={pokemonResource} />
            </React.Suspense>
          </ErrorBoundary>
        ) : (
          'Submit a pokemon'
        )}
      </div>
    </div>
  )
}

export default App

```

## 7. Coordinate Suspending components with `SuspenseList`

-  this delay function just allows us to make a promise take longer to resolve so we can easily play around with the loading time of our code.

- `SuspenseList` takes two props:

  - revealOrder (forwards, backwards, together) defines the order in which the `SuspenseList` children should be revealed.
  - together reveals all of them when they’re ready instead of one by one.
tail (collapsed, hidden) dictates how unloaded items in a `SuspenseList` is shown.
  - By default, `SuspenseList` will show all fallbacks in the list.
collapsed shows only the next fallback in the list.
hidden doesn’t show any unloaded items.

```javascript
function App() {
  const [startTransition] = React.useTransition(SUSPENSE_CONFIG)
  const [pokemonResource, setPokemonResource] = React.useState(null)

  function handleSubmit(pokemonName) {
    startTransition(() => {
      setPokemonResource(createResource(() => fetchUser(pokemonName)))
    })
  }

  if (!pokemonResource) {
    return (
      <div className="pokemon-info-app">
        <div
          className={`${cn.root} totally-centered`}
          style={{height: '100vh'}}
        >
          <PokemonForm onSubmit={handleSubmit} />
        </div>
      </div>
    )
  }

  return (
    <div className="pokemon-info-app">
      <div className={cn.root}>
        <ErrorBoundary>
          <React.SuspenseList revealOrder="forwards" tail="collapsed">
            <React.Suspense fallback={fallback}>
              <NavBar pokemonResource={pokemonResource} />
            </React.Suspense>
            <div className={cn.mainContentArea}>
              <React.SuspenseList revealOrder="forwards">
                <React.Suspense fallback={fallback}>
                  <LeftNav />
                </React.Suspense>
                <React.SuspenseList revealOrder="together">
                  <React.Suspense fallback={fallback}>
                    <MainContent pokemonResource={pokemonResource} />
                  </React.Suspense>
                  <React.Suspense fallback={fallback}>
                    <RightNav pokemonResource={pokemonResource} />
                  </React.Suspense>
                </React.SuspenseList>
              </React.SuspenseList>
            </div>
          </React.SuspenseList>
        </ErrorBoundary>
      </div>
    </div>
  )
}

export default App

```

The `SuspenseList` component has the following props:

- `revealOrder`: the order in which the suspending components are to render
  - `{undefined}`: the default behavior: everything pops in when it's loaded (as
    if you didn't wrap everything in a `SuspenseList`).
  - `"forwards"`: Only show the component when all components before it have
    finished suspending.
  - `"backwards"`: Only show the component when all the components after it have
    finished suspending.
  - `"together"`: Don't show any of the components until they've all finished
    loading
- `tail`: determines how to show the fallbacks for the suspending components
  - `{undefined}`: the default behavior: show all fallbacks
  - `"collapsed"`: Only show the fallback for the component that should be
    rendered next (this will differ based on the `revealOrder` specified).
  - `"hidden"`: Opposite of the default behavior: show none of the fallbacks
- `children`: other react elements which render `<React.Suspense />` components.
  Note: `<React.Suspense />` components do not have to be direct children as in
  the example above. You can wrap them in `<div />`s or other components if you
  need.
