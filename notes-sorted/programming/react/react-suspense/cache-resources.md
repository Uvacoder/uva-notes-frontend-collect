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
