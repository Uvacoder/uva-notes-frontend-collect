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
