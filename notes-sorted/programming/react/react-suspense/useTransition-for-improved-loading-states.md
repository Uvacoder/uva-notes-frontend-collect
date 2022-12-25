## 3. useTransition for improved loading states

- When a component suspends, it's literally telling React: "Don't render any
updates at all from the suspense component on down until I'm ready to roll."

- And here's how it looks like: 

```javascript
const SUSPENSE_CONFIG = {timeoutMs: 4000}

function Component() {
  const [startTransition, isPending] = React.useTransition(SUSPENSE_CONFIG)
  // etc...

  function handleClick() {
    // do something that triggers some interum state change we want to
    // happen before suspending starts
    startTransition(() => {
      // do something that triggers a suspending component to render
    })
  }

  // if needed, you can use the `isPending` boolean to display a loading spinner
  // or similar
}
```
- React Suspense with Concurrent mode comes with a default optimization that is optimistic in that it waits a tiny bit for your suspending promise to resolve before making any DOM updates. But this can make the app feel unresponsive for some use cases. 

- The experimental useTransition hook from React gives us more fine-grained control over the timing as well as the ability to show a pending state. Let's try that out here.
