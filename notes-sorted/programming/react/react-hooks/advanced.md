# Notes Advanced React Hooks 🎣

## 01. `useReducer`

The `useReducer` hook is a more powerful alternative to the `useState` hook. Both have the same purpose: maintaining state values, the difference with the `useReducer` hook is that it uses a reducer function to mutate the state when any action or state change is “dispatched”.

- **The `useReducer` function accepts 3 parameters:**
  - The function to be executed after a dispatch is called. This function will receive the previous state and the action information and should return the new state: `(state, action) => newState`
  - The initial value for the state, or `initialState`
  - A function to initialize the state, this function will receive the second argument as parameter, a `initialState`

- **And returns an array with 2 values:**
  - The `currentState` of the component
  - A dispatch function

Example of using `useReducer` to manage the value of a name in an `input`.

```js
function nameReducer(previousName, action) {
  return action
}

const initialNameValue = 'Joe'

function NameInput() {
  const [name, setName] = React.useReducer(nameReducer, initialNameValue)
  const handleChange = event => setName(event.target.value)
  return (
    <>
      <label>
        Name: <input defaultValue={name} onChange={handleChange} />
      </label>
      <div>You typed: {name}</div>
    </>
  )
}
```

## 02. `useCallback`

- `useMemo` and `useCallback` receives a function as its first argument and a dependencies array as the second one. The hook will return a new value only when one of the dependencies value changes (referential equality). 
- The main difference is that `useMemo` will call the function and return its result while `useCallback` will return the function without calling it.


**This is the problem useCallback solves. And here's how you solve it:**

```js
const updateLocalStorage = React.useCallback(
  () => window.localStorage.setItem('count', count),
  [count], // <-- yup! That's a dependency list!
)
React.useEffect(() => {
  updateLocalStorage()
}, [updateLocalStorage])
```

**Real example I came across recently where `useCallback` helped.**
- On key up, `isShiftDown` was always false.I didn't pass `handleKeyUp` to the `useEffect` dependencies.
- Doing so would cause effect to run on every render. Solutions: Wrap in `useCallback`!

## 03. `useContext`

- Context in React is a way for a child component to access a value in a parent component.
- The `useContext()` function accepts a context object, which is initially returned from `createContext()`, and then returns the current context value. 

**How to use Context**

```js
import React from 'react'

const FooContext = React.createContext()

function FooDisplay() {
  const foo = React.useContext(FooContext)
  return <div>Foo is: {foo}</div>
}

ReactDOM.render(
  <FooContext.Provider value="I am foo">
    <FooDisplay />
  </FooContext.Provider>,
  document.getElementById('root'),
)
// renders <div>Foo is: I am foo</div>
```

`<FooDisplay />` could appear anywhere in the render tree, and it will have access to the value which is passed by the FooContext.Provider component.
  - Note that as a first argument to `createContext`, you can provide a default value which React will use in the event someone calls useContext with your context, when no value has been provided:

```
ReactDOM.render(<FooDisplay />, document.getElementById('root'))
```

## 04. `useLayoutEffect`
 
 - `useLayoutEffect` has the very same signature as `useEffect`.
 - Call signature: `useLayoutEffect(effectFunction, arrayDependencies)`
 - Read on to see the difference between `useLayoutEffect` and `useEffect`. 
 - View the [docs.](https://reactjs.org/docs/hooks-reference.html#uselayouteffect)

```js
// sample usage: 
 useLayoutEffect(() => {
     //do something
 }, [arrayDep])
```

**Similar Usage as useEffect**

```js
<Editor code={ArrayDep} />
```


## useLayoutEffect vs useEffect

- The function passed to `useEffect` fires after layout and paint. i.e after the render has been committed to the screen. 
- This is okay for most side effects that should NOT block the browser from updating the screen. 
  - There are cases where you may not want the behaviour `useEffect` provides. e.g. if you need to make a visual change to
the DOM as a side effect. To prevent the user from seeing flickers of changes, you may use `useLayoutEffect`. 

- The function passed to `useLayoutEffect` will be run before the browser updates the screen. 


## 05. `useImperativeHandle`

`useImperativeHandle` is used to customize what value is exposed to the parent when it uses ref. This should be used with `forwardRef`.

```js
import React, { useImperativeHandle } from 'react';

function Child(props, ref) {
    useImperativeHandle(ref, () => 'Some value');

    return <h1>Hello</h1>
}

export default React.forwardRef(Child);
```

```js
import React, { useRef, useEffect } from 'react';
import Child from './child';

function Parent() {
    const childRef = useRef();

    useEffect(() => {
        console.log(inputEl.current); 
        //output: 'Some value'
        //Not DOM element anymore
    }, []);

    return <Child ref={childRef}/>
}

export default Parent;
```

- `useImperativeHandle` can be used to expose only the input DOM element to the parent.


## 06. `useDebugValue`

[The React DevTools browser extension](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en)
is a must have for any React developer. When you start writing custom hooks, it
can be useful to give them a special label. This is especially useful to
differentiate different Apps of the same hook in a given component.

- `useDebugValue` can now be used to display a label for custom hooks in React DevTools. React Devtools will show if you have downloaded the browser extension (Chrome, Firefox) and opened the browser developer tools(hit F12).

We can now add a label, letting us know how many family members there are.

- This is where `useDebugValue` comes in. You use it in a custom hook, and you
call it like so:

```javascript
function useCount({initialCount = 0, step = 1} = {}) {
  React.useDebugValue({initialCount, step})
  const [count, setCount] = React.useState(0)
  const increment = () => setCount(c => c + 1)
  return [count, increment]
}
```

So now when people use the `useCount` hook, they'll see the `initialCount` and
`step` values for that particular hook.
