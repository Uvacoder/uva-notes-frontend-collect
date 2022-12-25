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
