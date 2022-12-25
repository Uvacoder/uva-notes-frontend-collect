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
