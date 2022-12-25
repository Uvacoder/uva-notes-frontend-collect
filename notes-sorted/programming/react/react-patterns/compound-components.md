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
