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
