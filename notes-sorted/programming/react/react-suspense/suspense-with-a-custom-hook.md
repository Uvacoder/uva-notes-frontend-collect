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
