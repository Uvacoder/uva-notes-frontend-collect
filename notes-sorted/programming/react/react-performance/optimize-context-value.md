# 6. Optimize context value

This can be problematic in certain scenarios. You can read more about this here: https://github.com/kentcdodds/kentcdodds.com/blob/319db97260078ea4c263e75166f05e2cea21ccd1/content/blog/how-to-optimize-your-context-value/index.md

The quick and easy solution to this problem is to memoize the value that you provide to the context provider:

```jsx
const CountContext = React.createContext()

function CountProvider(props) {
  const [count, setCount] = React.useState(0)
  const value = React.useMemo([count, setCount], [count])
  return <CountContext.Provider value={value} {...props} />
}
```
