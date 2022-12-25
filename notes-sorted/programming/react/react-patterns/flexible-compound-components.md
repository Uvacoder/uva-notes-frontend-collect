## 3. Flexible Compound Components

Right now our component can only clone and pass props to immediate children. So
we need some way for our compound components to implicitly accept the on state
and toggle method regardless of where they're rendered within the Toggle
component's "posterity" :)

The way we do this is through context. `React.createContext` is the API we want.

**Real World Projects that use this pattern:**

- [`@reach/accordion`](https://reacttraining.com/reach-ui/accordion)
