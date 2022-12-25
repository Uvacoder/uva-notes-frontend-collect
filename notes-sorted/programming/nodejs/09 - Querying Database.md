In our controller (storeController):
```js
const stores = await Store.find()
```
This will query db and return all stores

Because this is an async operation, wrap the route in our `catchErrors` middleware in the routes file:
```js
router.get("/stores", catchErrors(storeController.getStores))
```

[[10 - Creating Editorial Flow]]