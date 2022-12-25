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
