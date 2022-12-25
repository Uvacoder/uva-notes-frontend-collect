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
