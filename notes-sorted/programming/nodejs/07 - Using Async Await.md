****In the controller bring in mongoose and a ref to our schema:
```js
const mongoose = require('mongoose')
const Store = mongoose.model('Store')
```

To create a store, in our `createStore` method in `storeController`:
```js
exports.createStore = async (req, res) => {
	const store = new Store(req.body)
}
```

Because we are using a strict schema, only the fields that we've defined will be picked up by the db

To save the newly created store:
```js
await store.save()
```
Passes off request to db to save the store, comes back with a promise with either the store instance or an error

We can condense this operation onto one line:
```js
const store = await new Store(req.body).save()
```

---

Because we're using `async / await` we can either wrap the `store.save()` call in a `try / catch`, or define some error handlers that will come after our routes in the express app 

```js
app.use(errorHandlers.catchErrors)
```

Which is a higher-order function that essentially just catches errors: 

```js
exports.catchErrors = (fn) => {
  return function(req, res, next) {
    return fn(req, res, next).catch(next);
  };
};
```


Then in our routes file, we wrap the async functions with our `catchErrors` higher-order function
```js
router.post("/add", catchErrors(storeController.createStore));
```

[[08 - Flash Messages]]