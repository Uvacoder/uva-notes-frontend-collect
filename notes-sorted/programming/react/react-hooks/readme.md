
# React Hooks
## Table of Contents

1.  React Hooks
    1.  [General](#orge14fed7)
    2.  [useState: greeting](#org24ad32c)
        1.  [useState](#orgf6e53f5)
        2.  [insitial Props](#orga116987)
    3.  [useEffect: persistent state](#org9105d5d)
    4.  [Hooks Flow](#org847ed77)
    5.  [Lifting state](#org08466be)
        1.  [Solution: Lift State](#orge478632)
        2.  [ECS01: Colocate State](#org2874516)
    6.  [useState: tic tac toe](#org6284874)
        1.  [Solution: Managaged and Derieved State](#org231cce9)
        2.  [ECS01: Preserve State in localStorage](#orgeb73776)
        3.  [ECS02: useLocalStorageState Custom Hook](#org1f9afa0)
        4.  [ECS03: Add Game History Feature](#orgcc7ebe6)
    7.  [Class Refactor](#org0c74463)
    8.  [useRef and useEffect: DOM interaction](#orgfec64e8)
        1.  [Solution](#orgf84cfdd)
    9.  [useEffect: HTTP requests](#org38b8d3a)
        1.  [Solution Fetch Data](#orgdc06b56)
        2.  [ECS01 handle errors](#orge152a5a)
        3.  [ECS02 use a status](#orgc4e8134)
        4.  [ECS03 store the state in an object](#org5475b08)
        5.  [ECS04 create an ErrorBoundary component](#org2d5777a)
        6.  [ECS05 re-mount the error boundary](#org29a94d5)
        7.  [ECS06 use react-error-boundary](#org303ffe2)
        8.  [ECS07 reset the error boundary](#org6cb7934)
        9.  [ECS08 use resetKeys](#org2710252)


<a id="orge14fed7"></a>

## General

<https://github.com/kentcdodds/react-hooks>


<a id="org24ad32c"></a>

## useState: greeting

React uses &rsquo;hooks&rsquo; to build in interactivity into an application

Common hooks are:
React.useState
React.useEffect
React.useContext
React.useRef
React.useReducer


<a id="orgf6e53f5"></a>

### useState

We can name these variables whatever we want. Common convention is to choose a name for the state variable, then prefix set in front of that for the updater function.

-> `setVariable`

if you were to declare a variable in a React component, you can&rsquo;t update it because the function that gets called only get&rsquo;s called once.

    function Greeting(props) {
      let name = ''
    
      function handleChange(event) {
        // 🐨 update the name here based on event.target.value
        name = event.target.value
      }
    
      return (...)
    
    }

`name` will only ever get set once and we won&rsquo;t be able to update it.

`useState` will help us out here! you can `setName` which is a function that will let you update state that is returned to use from `useState`

    const [name, setName] = useState('')

Now you just set the name and you are updating state in React!

    function handleChange(event) {
        // 🐨 update the name here based on event.target.value
        setName(event.target.value)
      }


<a id="orga116987"></a>

### insitial Props

useState accepts an arguement that it will initialize state with.

You can use React props to initialize that state and pass it in!

You can set the value of the input to name so that it&rsquo;s a controlled React input

    function Greeting({initialName = ''}) {
      const [name, setName] = useState(name)
    
        // ...
      return (
          <div>
            <form>
              <label htmlFor="name">Name: </label>
              <input value={name} onChange={handleChange} id="name" />
            </form>
            {name ? <strong>Hello {name}</strong> : 'Please type your name'}
          </div>
      )
    }
    
    function App() {
      return <Greeting initialName="Jill" />
    }


<a id="org9105d5d"></a>

## useEffect: persistent state

side effects are handled through the useEffect hook.

an example is setting state values in localStorage so State can persist through a refresh

<https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage>

Any time the component renders, useEffect will get called

    function Greeting({initialName = ''}) {
      // 🐨 initialize the state to the value from localStorage
    
      const [name, setName] = React.useState(
        window.localStorage.getItem('name') || initialName,
      )
    
      // 🐨 Here's where you'll use `React.useEffect`.
      // The callback should set the `name` in localStorage.
      // 💰 window.localStorage.setItem('name', name)
      React.useEffect(() => {
        window.localStorage.setItem('name', name)
      }, [name])
    
    //...
    }

1.  ECS01: lazy state initialization

    React will initialize state every time in a useState hook if you simply pass it a value.
    
    It will re-render every time a value changes.
    
    React’s useState hook allows you to pass a function instead of the actual value, and then it will only call that function to get the state value when the component is rendered the first time. So you can go from this: React.useState(someExpensiveComputation()) To this: React.useState(() => someExpensiveComputation())
    
        const [name, setName] = React.useState(
          () => window.localStorage.getItem('name') || initialName,
        )
    
    This optimization isn&rsquo;t often needed. Accessing localStorage on initialization is one of the few times that you&rsquo;d need this.

2.  ECS02: effect dependencies

    There are various reasons a component can re-render. Sometimes you don&rsquo;t want an effect to be triggered on a re-render. This is often tied to a specific piece of state that we want to watch for updates.
    
    useEffect gives us an optional array argument that we can use to specifify when we want the effect to run.
    
        React.useEffect(() => {
          window.localStorage.setItem('name', name)
        }, [name])
    
    The above code will only run when the name variable changes. Other state changes or renders will not run the effect.
    
    Passing an empty array will have the effect only run on initializaion of the Component.
    
    React does a shallow comparison of the item passed into the array.

3.  ECS03: custom hook

        const useLocalStorageState = ({key, initialState = ''}) => {
          const [state, setState] = React.useState(
            () => window.localStorage.getItem(key) || initialState,
          )
        
          React.useEffect(() => {
            window.localStorage.setItem(key, state)
          }, [state])
        
          return [state, setState]
        }
    
    The variables and functions you export from a hook can be renamed in the resulting call to the hook so the hook itself can be generic.
    
        const [name, setName] = useLocalStorageState(initialName)
    
    There is a convention to prepend a function with `use` but doing so isn&rsquo;t what makes it a custom hook. Using other hooks and adding custom functionality is what makes it a custom hook!

4.  ECS04: flexible localStorage hook

    The amount of logic that you include in your custom hook does not have to affect the complexity to use it.
    
    The example here is making the hook more flexible by stringifying the localstorage value and parsing it when it gets read.
    
    You can even give someone the option to roll their own serilization in a third argument.
    
    Another optimization is to allow the default State value to be a function like we&rsquo;ve seen in lazy state initialization lesson.
    
    in the useState hook:
    
        return typeof initialState === 'function' ? initialState() : initialState
    
    if you want to keep track of a value without triggering a re-render, useRef is your friend. The case here is tracking if the key for localstorage changes to update it to the new one without scraping the current value.
    
        const prevKeyRef = React.useRef(key)
        
          React.useEffect(() => {
            const prevKey = prevKeyRef.current
            if(prevKey !== key) {
              window.localStorage.removeItem(prevKey)
            }
            prevKeyRef.current = key
            window.localStorage.setItem(key, serialize(state))
          }, [state, serialize, key])


<a id="org847ed77"></a>

## Hooks Flow


<a id="org08466be"></a>

## Lifting state


<a id="orge478632"></a>

### Solution: Lift State


<a id="org2874516"></a>

### ECS01: Colocate State


<a id="org6284874"></a>

## useState: tic tac toe

Managed State: State that you need to explicitly manage
Derived State: State that you can calculate based on other state

Not all state has to be managed by React! You can declare variables in state that derive from the state that you want to manage

[Don&rsquo;t sync state; derive it](https://kentcdodds.com/blog/dont-sync-state-derive-it)


<a id="org231cce9"></a>

### Solution: Managaged and Derieved State

    const [squares, setSquares] = React.useState(Array(9).fill(null))
    
    const nextValue = calculateNextValue(squares)
    const winner = calculateWinner(squares)
    const status = calculateStatus(winner, squares, nextValue)

`nextValue`, `winner`, and `status` don&rsquo;t need to be managed through react because they are determined by the values within `squares`

This will keep all values in sync where if you tried to sync them through React you could run into subtle bugs where values don&rsquo;t update automatically like you would expect


<a id="orgeb73776"></a>

### ECS01: Preserve State in localStorage


<a id="org1f9afa0"></a>

### ECS02: useLocalStorageState Custom Hook


<a id="orgcc7ebe6"></a>

### ECS03: Add Game History Feature

Adding complexity into an application can get messy real quick.

One great place to start is the static representation of what the data will look like on the screen when it&rsquo;s there. Once you get that rendering correctly, you can work backwards to add the dynamic aspects of the feature.

For the history feature, starting with what `moves` looks like is the way:

    const moves = history.map((stepSquares, step) => {
      const desc = step ? `Go to move #${step}` : 'Go to game start'
      const isCurrentStep = step === currentStep
      return (
        <li key={step}>
          <button disabled={isCurrentStep} onClick={() => setCurrentStep(step)}>
            {desc} {isCurrentStep ? '(current)' : null}
          </button>
        </li>
      )
    })

There are two new variables here from before: history and currentStep

Set them to expected values

    const history = [Array(9).fill(null)]
    const currentStep = 0

Once that renders correctly, try more complex data

    const history = [[], Array(9).fill(null), []]
    const currentStep = 2

Now the UI renders correctly, we can implement this.

    const [history, setHistory] = useLocalStorageState('tic-tac-toe:history', [
        Array(9).fill(null),
      ])
      const [currentStep, setCurrentStep] = useLocalStorageState(
        'tic-tac-toe:step',
        0,
      )

The rest of our logic expects 1 array that represents the board - that can be derived from history because the current board state is now a derivative to the whole game history

    const currentSquares = history[currentStep]

🤔 You don&rsquo;t need to force the functionality into the current implementation, build it on top and transfer. I made the mistake of trying to extend `squares` to include a history instead of building history and then seeing that the current squares could be derived.

The only updates to existing code is setting history and current step. and subsequently

    function selectSquare(square) {
        if (winner || currentSquares[square]) {
          return
        }
    
        const newHistory = history.slice(0, currentStep + 1)
        const squares = [...currentSquares]
    
        squares[square] = nextValue
        setHistory([...newHistory, squares])
        setCurrentStep(newHistory.length)
      }
    
      function restart() {
        setHistory([Array(9).fill(null)])
        setCurrentStep(0)
      }


<a id="org0c74463"></a>

## Class Refactor


<a id="orgfec64e8"></a>

## useRef and useEffect: DOM interaction

You don&rsquo;t normally have access to DOM nodes in the ReactDOM render method.

React&rsquo;s method for giving you access to the actual DOM is through Refs.

We&rsquo;ve seen refs before as they don&rsquo;t trigger renders and stay consistent between

Because you need the component to be mounted, you will do direct DOM munipulation in a useEffect


<a id="orgf84cfdd"></a>

### Solution

    function Tilt({children}) {
        console.log(tiltRef)
    
        // ...
    }

tiltRef will be undefined because the component isn&rsquo;t fully mounted when console.log is run.

Need a useEffect to ensure the Component is mounted.

useEffect&rsquo;s return will be the clean up function that you might need to run when the Component is removed from the DOM. In our case, we need to destroy vanillaTilt

The Ref `current` property is mutable

`Do you need to synchronize the state of the world with the state of your application?`
-> Answer is what you put in your useEffect dependency array


<a id="org38b8d3a"></a>

## useEffect: HTTP requests


<a id="orgdc06b56"></a>

### Solution Fetch Data

Write the UI first! then add the interactivity.

    return !pokemonName ? (
        'Submit a Pokemon'
      ) : pokemon ? (
        <PokemonDataView pokemon={pokemon} />
      ) : (
        <PokemonInfoFallback name={pokemonName} />
      )

HTTP requests are side effects of a component so they go in a useEffect

    React.useEffect(() => {
        if (!pokemonName) return
    
        setLoadState('pending')
        setPokemon(null)
        fetchPokemon(pokemonName).then(pokemonData => {
          setPokemon(pokemonData)
          setLoadState('resolved')
        })
      }, [pokemonName])


<a id="orge152a5a"></a>

### ECS01 handle errors

If you pass in a value that doesn&rsquo;t exist you&rsquo;ll make your user think they are stuck in a loading state.

Alot of handling errors is UX.

Start with static data again!

    fetchPokemon(pokemonName)
       .then(pokemonData => setPokemon(pokemonData))
       .catch(err => setError(err))
    )

You can &rsquo;catch&rsquo; an error like this or pass the function in as a second argument to then:

    fetchPokemon(pokemonName).then(
      pokemonData => setPokemon(pokemonData),
      err => setError(err),
    )


<a id="orgc4e8134"></a>

### ECS02 use a status

Using Booleans to define what JSX gets rendered starts getting cumbersome. If you set an error boolean, you have to remember to unset it when a user performs another action or else that error UI will persist.

Using a seperate &rsquo;status&rsquo; variable we can define what gets shown. For HTTP requests there are typically 4 states: idle, pending, resolved, or rejected

    const STATUS = {
      idle: 'idle',
      pending: 'pending',
      resolved: 'resolved',
      rejected: 'rejected',
    }
    
    if (status === STATUS.idle) {
        return 'Submit a Pokemon'
    } else if (status === STATUS.rejected) {
        return (
          <div role="alert">
            There was an error:{' '}
            <pre style={{whiteSpace: 'normal'}}>{error.message}</pre>
          </div>
        )
      } else if (status === STATUS.pending) {
        return <PokemonInfoFallback name={pokemonName} />
      } else if (status === STATUS.resolved) {
        return <PokemonDataView pokemon={pokemon} />
      }


<a id="org5475b08"></a>

### ECS03 store the state in an object

When you have a handful of state objects that depend on eachother (status and pokemon), managing them in separate useState calls can be cumbersome and introduce subtle errors.

One of these errors is that you have to set state in the right order or you will try to render data before it&rsquo;s available. In this case `status` and `pokemon`

You can fix this issue by putting your seperate state items into one object that a useState call manages.

    const [state, setState] = React.useState({
      status: 'idle',
      pokemon: null,
      error: null,
    })
    const {status, pokemon, error} = state

then you just have to update your `setState` calls

    React.useEffect(() => {
      if (!pokemonName) {
        return
      }
      setState({status: 'pending'})
      fetchPokemon(pokemonName).then(
        pokemon => {
          setState({status: 'resolved', pokemon})
        },
        error => {
          setState({status: 'rejected', error})
        },
      )
    }, [pokemonName])

Something to keep in mind, when you `setState({status: 'pending'})` you remove the pokemon and error attributes in state. This isn&rsquo;t a problem for us in this case but if you depended on those values elsewhere in your UI you could run into issues.


<a id="org2d5777a"></a>

### ECS04 create an ErrorBoundary component

ErrorBoundary&rsquo;s are one of the only things you&rsquo;ll have to use that still implement classes.

Runtime errors do happen sometime, so a useful error is much nicer than the white screen of death.

Every class component needs to have a render method on it.

    class ErrorBoundary extends React.Component {
        state = {error: null}
    
        static getDerivedStateFromError(error) {
         return {error}
        }
    
        render() {
          if (this.state.error) {
            // You can render any custom fallback UI
            return (
              <div role="alert">
                <h1>Something went wrong.</h1>
                <details style={{whiteSpace: 'pre-wrap'}}>
                  {this.state.error && this.state.error.toString()}
                  <br />
                </details>
              </div>
            )
          }
    
          return this.props.children
        }
    }

getDerivedStateFromError will set the error property in state because you returned it so you don&rsquo;t need to do any setState calls. (Maybe you can&rsquo;t when React is v16.13.1 - I was running into errors trying to setState).

To make the component much more flexible, you can pass a prop to it called FallbackComponent so that the user can define what UI they want to use for showing their error

    class ErrorBoundary extends React.Component {
        state = {error: null}
    
        static getDerivedStateFromError(error) {
         return {error}
        }
    
        render() {
          if (this.state.error) {
            // You can render any custom fallback UI
            return <this.props.FallbackComponent error={error} />
          }
    
          return this.props.children
        }
    }
    
    function ErrorFallback({error}) {
      return (
        <div role="alert">
          There was an error:{' '}
          <pre style={{whiteSpace: 'normal'}}>{error.message}</pre>
        </div>
      )
    }
    
    //...
      <ErrorBoundary FallbackComponent={ErrorFallback}>
        <PokemonInfo pokemonName={pokemonName} />
      </ErrorBoundary>


<a id="org29a94d5"></a>

### ECS05 re-mount the error boundary

When an error boundary is triggered - that state is stuck so the app will no longer work.

All you need to do is add a key that is unique (which happens to be pokemonName) which will force React to rerender the component and reset the state thus clearing the error so we can search for pokemon again.

    
    return (
      <div className="pokemon-info-app">
        <PokemonForm pokemonName={pokemonName} onSubmit={handleSubmit} />
        <hr />
        <div className="pokemon-info">
          <ErrorBoundary key={pokemonName} FallbackComponent={ErrorFallback}>
            <PokemonInfo pokemonName={pokemonName} />
          </ErrorBoundary>
        </div>
      </div>
    )


<a id="org303ffe2"></a>

### ECS06 use react-error-boundary

    import {ErrorBoundary} from 'react-error-boundary'

react-error-boundary will let you handle your error boundaries without you having to build out a class component, YAY!


<a id="org6cb7934"></a>

### ECS07 reset the error boundary

Switching the props currently re-renders the whole component every single time since we set the key.

The library we imported has quite a few features. one of those is a resetErrorBoundary function that will reset the state and a onReset prop that we can use to clear our component state with the ErrorBoundary reset.

    function App() {
      const [pokemonName, setPokemonName] = React.useState('')
    
      function handleSubmit(newPokemonName) {
        setPokemonName(newPokemonName)
      }
    
    function handleReset() {
        setPokemonName('')
      }
    
      return (
        <div className="pokemon-info-app">
          <PokemonForm pokemonName={pokemonName} onSubmit={handleSubmit} />
          <hr />
          <div className="pokemon-info">
            <ErrorBoundary FallbackComponent={ErrorFallback} onReset={handleReset}>
              <PokemonInfo pokemonName={pokemonName} />
            </ErrorBoundary>
          </div>
        </div>
      )
    }
    
    function ErrorFallback({resetErrorBoundary, error}) {
      return (
        <div role="alert">
          <h1>Something went wrong.</h1>
          <button
            onClick={() => {
              resetErrorBoundary()
            }}
          >
            Try Again
          </button>
          <details style={{whiteSpace: 'pre-wrap'}}>
            {error && error.toString()}
            <br />
          </details>
        </div>
      )
    }


<a id="org2710252"></a>

### ECS08 use resetKeys

The api gets nicer!

`resetKeys` is a prop you can pass to the `ErrorBoundary` that will reset the error state similar to our keys implimentation we had earlier.

Now the user has the flexibility to use the `Try Again` button or try another pokemon name.

    function App() {
      const [pokemonName, setPokemonName] = React.useState('')
    
      function handleSubmit(newPokemonName) {
        setPokemonName(newPokemonName)
      }
    
      function handleReset() {
        setPokemonName('')
      }
    
      return (
        <div className="pokemon-info-app">
          <PokemonForm pokemonName={pokemonName} onSubmit={handleSubmit} />
          <hr />
          <div className="pokemon-info">
            <ErrorBoundary
              FallbackComponent={ErrorFallback}
              onReset={handleReset}
              resetKeys={[pokemonName]}
            >
              <PokemonInfo pokemonName={pokemonName} />
            </ErrorBoundary>
          </div>
        </div>
      )
    }
