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
