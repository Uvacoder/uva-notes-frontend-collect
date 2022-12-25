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
