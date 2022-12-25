
# Advanced React Patterns Notes

## 1. Context Controller


```javascript
// src/context/counter.js
const CounterContext = React.createContext()

function CounterProvider({step = 1, initialCount = 0, ...props}) {
  const [state, dispatch] = React.useReducer(
    (state, action) => {
      const change = action.step ?? step
      switch (action.type) {
        case 'increment': {
          return {...state, count: state.count + change}
        }
        case 'decrement': {
          return {...state, count: state.count - change}
        }
        default: {
          throw new Error(`Unhandled action type: ${action.type}`)
        }
      }
    },
    {count: initialCount},
  )

  const value = [state, dispatch]
  return <CounterContext.Provider value={value} {...props} />
}

function useCounter() {
  const context = React.useContext(CounterContext)
  if (context === undefined) {
    throw new Error(`useCounter must be used within a CounterProvider`)
  }
  return context
}

export {CounterProvider, useCounter, increment, decrement}
```

```javascript
// src/screens/counter.js
import {useCounter, increment, decrement} from 'context/counter'

function Counter() {
  const [state, dispatch] = useCounter()
  const increment = () => dispatch({type: 'increment'})
  const decrement = () => dispatch({type: 'decrement'})
  return (
    <div>
      <div>Current Count: {state.count}</div>
      <button onClick={decrement}>-</button>
      <button onClick={increment}>+</button>
    </div>
  )
}
```

```javascript
// src/index.js
import {CounterProvider} from 'context/counter'

function App() {
  return (
    <CounterProvider>
      <Counter />
    </CounterProvider>
  )
}
```

What Dan recommends (and what Facebook does) is pass dispatch as we had
originally. And to solve the annoyance we were trying to solve in the first
place, they use importable "helpers" that accept `dispatch`. Let's take a look
at how that would look:

```javascript
// src/context/counter.js
const CounterContext = React.createContext()

function CounterProvider({step = 1, initialCount = 0, ...props}) {
  const [state, dispatch] = React.useReducer(
    (state, action) => {
      const change = action.step ?? step
      switch (action.type) {
        case 'increment': {
          return {...state, count: state.count + change}
        }
        case 'decrement': {
          return {...state, count: state.count - change}
        }
        default: {
          throw new Error(`Unhandled action type: ${action.type}`)
        }
      }
    },
    {count: initialCount},
  )

  const value = [state, dispatch]

  return <CounterContext.Provider value={value} {...props} />
}

function useCounter() {
  const context = React.useContext(CounterContext)
  if (context === undefined) {
    throw new Error(`useCounter must be used within a CounterProvider`)
  }
  return context
}

const increment = dispatch => dispatch({type: 'increment'})
const decrement = dispatch => dispatch({type: 'decrement'})

export {CounterProvider, useCounter, increment, decrement}
```

```javascript
// src/screens/counter.js
import {useCounter, increment, decrement} from 'context/counter'

function Counter() {
  const [state, dispatch] = useCounter()
  return (
    <div>
      <div>Current Count: {state.count}</div>
      <button onClick={() => decrement(dispatch)}>-</button>
      <button onClick={() => increment(dispatch)}>+</button>
    </div>
  )
}
```

## 2. Compound Components

```html
<select>
  <option value="1">Option 1</option>
  <option value="2">Option 2</option>
</select>
```

The `<select>` is the element responsible for managing the state of the UI, and
the `<option>` elements are essentially more configuration for how the select
should operate (specifically, which options are available and their values).

Let's imagine that we were going to implement this native control manually. A
naive implementation would look something like this:

```jsx
<CustomSelect
  options={[
    {value: '1', display: 'Option 1'},
    {value: '2', display: 'Option 2'},
  ]}
/>
```

This works fine, but it's less extensible/flexible than a compound components
API. For example. What if I want to supply additional attributes on the
`<option>` that's rendered, or I want the `display` to change based on whether
it's selected? We can easily add API surface area to support these use cases,
but that's just more for us to code and more for users to learn. That's where
compound components come in really handy!

**Real World Projects that use this pattern:**

- [`@reach/tooltip`](https://reacttraining.com/reach-ui/tooltip)
- Actually most of [Reach UI](https://reacttraining.com/reach-ui) implements
  this pattern


## 3. Flexible Compound Components

Right now our component can only clone and pass props to immediate children. So
we need some way for our compound components to implicitly accept the on state
and toggle method regardless of where they're rendered within the Toggle
component's "posterity" :)

The way we do this is through context. `React.createContext` is the API we want.

**Real World Projects that use this pattern:**

- [`@reach/accordion`](https://reacttraining.com/reach-ui/accordion)

### Final Code

```jsx
// Flexible Compound Components with context
// http://localhost:3000/isolated/final/03.js

import React from 'react'
import {Switch} from '../switch'

const ToggleContext = React.createContext()
ToggleContext.displayName = 'ToggleContext'

function Toggle({children}) {
  const [on, setOn] = React.useState(false)
  const toggle = () => setOn(!on)

  return (
    <ToggleContext.Provider value={{on, toggle}}>
      {children}
    </ToggleContext.Provider>
  )
}

function useToggle() {
  return React.useContext(ToggleContext)
}

function ToggleOn({children}) {
  const {on} = useToggle()
  return on ? children : null
}

function ToggleOff({children}) {
  const {on} = useToggle()
  return on ? null : children
}

function ToggleButton({...props}) {
  const {on, toggle} = useToggle()
  return <Switch on={on} onClick={toggle} {...props} />
}

function App() {
  return (
    <div>
      <Toggle>
        <ToggleOn>The button is on</ToggleOn>
        <ToggleOff>The button is off</ToggleOff>
        <div>
          <ToggleButton />
        </div>
      </Toggle>
    </div>
  )
}

export default App
```

## 4. Prop Collections and Getters

In typical UI components, you need to take accessibility into account. For a
button functioning as a toggle, it should have the `aria-pressed` attribute set
to `true` or `false` if it's toggled on or off. In addition to remembering that,
people need to remember to also add the `onClick` handler to call `toggle`.

Lots of the reusable/flexible components and hooks that we'll create have some
common use-cases and it'd be cool if we could make it easier to use our
components and hooks the right way without requiring people to wire things up
for common use cases.

**Real World Projects that use this pattern:**

- [downshift](https://github.com/downshift-js/downshift) (uses prop getters)
- [react-table](https://github.com/tannerlinsley/react-table) (uses prop
  getters)
- [`@reach/tooltip`](https://reacttraining.com/reach-ui/tooltip) (uses prop
  collections)
  
```jsx
/ Prop Collections and Getters
// http://localhost:3000/isolated/final/04.js

import React from 'react'
import {Switch} from '../switch'

function useToggle() {
  const [on, setOn] = React.useState(false)
  const toggle = () => setOn(!on)

  return {
    on,
    toggle,
    togglerProps: {
      'aria-pressed': on,
      onClick: toggle,
    },
  }
}

function App() {
  const {on, togglerProps} = useToggle()
  return (
    <div>
      <Switch on={on} {...togglerProps} />
      <hr />
      <button aria-label="custom-button" {...togglerProps}>
        {on ? 'on' : 'off'}
      </button>
    </div>
  )
}

export default App
```

## 5. Prop Collections and Getters

```jsx
// state reducer
// http://localhost:3000/isolated/final/05.js

import React from 'react'
import {Switch} from '../switch'

const callAll = (...fns) => (...args) => fns.forEach(fn => fn?.(...args))

function toggleReducer(state, {type, initialState}) {
  switch (type) {
    case 'toggle': {
      return {on: !state.on}
    }
    case 'reset': {
      return initialState
    }
    default: {
      throw new Error(`Unsupported type: ${type}`)
    }
  }
}

function useToggle({initialOn = false, reducer = toggleReducer} = {}) {
  const {current: initialState} = React.useRef({on: initialOn})
  const [state, dispatch] = React.useReducer(reducer, initialState)
  const {on} = state

  const toggle = () => dispatch({type: 'toggle'})
  const reset = () => dispatch({type: 'reset', initialState})

  function getTogglerProps({onClick, ...props} = {}) {
    return {
      'aria-pressed': on,
      onClick: callAll(onClick, toggle),
      ...props,
    }
  }

  function getResetterProps({onClick, ...props} = {}) {
    return {
      onClick: callAll(onClick, reset),
      ...props,
    }
  }

  return {
    on,
    reset,
    toggle,
    getTogglerProps,
    getResetterProps,
  }
}

function App() {
  const [timesClicked, setTimesClicked] = React.useState(0)
  const clickedTooMuch = timesClicked >= 4

  function toggleStateReducer(state, action) {
    switch (action.type) {
      case 'toggle': {
        if (clickedTooMuch) {
          return {on: state.on}
        }
        return {on: !state.on}
      }
      case 'reset': {
        return {on: false}
      }
      default: {
        throw new Error(`Unsupported type: ${action.type}`)
      }
    }
  }

  const {on, getTogglerProps, getResetterProps} = useToggle({
    reducer: toggleStateReducer,
  })

  return (
    <div>
      <Switch
        {...getTogglerProps({
          disabled: clickedTooMuch,
          on: on,
          onClick: () => setTimesClicked(count => count + 1),
        })}
      />
      {clickedTooMuch ? (
        <div data-testid="notice">
          Whoa, you clicked too much!
          <br />
        </div>
      ) : timesClicked > 0 ? (
        <div data-testid="click-count">Click count: {timesClicked}</div>
      ) : null}
      <button {...getResetterProps({onClick: () => setTimesClicked(0)})}>
        Reset
      </button>
    </div>
  )
}

export default App

```

## 6. Control Props

This concept is basically the same as controlled form elements in React that
you've probably used many times: 📜
https://reactjs.org/docs/forms.html#controlled-components

```javascript
function MyCapitalizedInput() {
  const [capitalizedValue, setCapitalizedValue] = React.useState('')

  return (
    <input
      value={capitalizedValue}
      onChange={e => setCapitalizedValue(e.target.value.toUpperCase())}
    />
  )
}
```


**Real World Projects that use this pattern:**

- [downshift](https://github.com/downshift-js/downshift)
- [`@reach/listbox`](https://reacttraining.com/reach-ui/listbox)
