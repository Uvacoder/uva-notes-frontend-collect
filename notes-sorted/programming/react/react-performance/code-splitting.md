# 1. Code splitting

Code splitting acts on the principle that loading less code will speed up your app.

```jsx
import('/some-module.js').then(
  (module) => {
    // do stuff with the module's exports
  },
  (error) => {
    // there was some error loading the module...
  }
)
```

```jsx
// Code splitting solution
import React from 'react'

const loadTilt = () => import('../tilt')
// Calling React.lazy, it needs to be use with React.Suspense
const Tilt = React.lazy(loadTilt)
function App() {
  const [showTilt, setShowTilt] = React.useState(false)

  React.useEffect(() => {
    loadTilt()
  }, [])

  return (
    <div>
      <label>
        <input
          type="checkbox"
          checked={showTilt}
          onChange={(e) => setShowTilt(e.target.checked)}
        />
        {' show tilt'}
      </label>
      <React.Suspense fallback={<div>loading titl...</div>}>
        {showTilt ? <Tilt>This is tilted!</Tilt> : null}
      </React.Suspense>
    </div>
  )
}
// 🦉 Note that in this app, we actually already have a React.Suspense
// component higher up in the tree where this component is rendered
// (see app.js), so you *could* just rely on that one. Why would you not want
// to do that do you think?

////////////////////////////////////////////////////////////////////
//                                                                //
//                 Don't make changes below here.                 //
// But do look at it to see how your code is intended to be used. //
//                                                                //
////////////////////////////////////////////////////////////////////

function Usage() {
  return <App />
}

export default Usage
```

React has built-in support for loading modules as React components. The module must have a React component as the default export, and you have to use the <React.Suspense /> component to render a fallback value while the user waits for the module to be loaded.

If you're using webpack to bundle your application, then you can use webpack
[magic comments](https://webpack.js.org/api/module-methods/#magic-comments) to
have webpack instruct the browser to prefetch dynamic imports:
