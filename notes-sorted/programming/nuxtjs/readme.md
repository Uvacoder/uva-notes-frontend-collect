# Nuxt.js

## Auth Notes

`nuxt-identity-demo` is best working example I think so far

### Part 1 - Handling Already Logged In Users

You need a client-init plugin that checks for a user that has already logged in.

With using Netlify's gotrue-js library, it's as simple as getting the `currentUser` via a method.
If you weren't using something that provided this built-in functionality, you'd do something like checking in `localStorage`

Either way, once we get the result of whether there is an already logged-in user, we update our `state`.

### Part 2 - Handling Protected Routes

Need to log issue with dev not working exacftly right but works perfectly in production once the site has been statically generated.

### Part 3 - The NEW Solution Of Dynamically Setting The **Admin** To SPA

Implemented with `serverMiddleware`. Apparently this still works for SSites.

---

## Plugins

```js
export default (ctx, inject) => {
  ctx.fdbClient = fdbClient;
  inject("fdbClient", fdbClient);
};
```

This allows you to access the plugin within `asyncData` as shown below.

```js
  async asyncData({ fdbClient }) {
      return {}
  })
```

If I just `inject` then I would access it as follows

```js
  async asyncData({ app }) {
      const { fdbClient } = app
    return {}
  })
```
