In `models/Store.js` in our `storeSchema.pre` hook call, we don't check if the slug that is being created is a duplicate of a previously created slug. We need to do this to avoid creating entries in the db that don't have a reachable slug

**Note: make sure to make the `pre` hook's callback function async** 

1. Create a regex to check if the slug already exists in the db
```js
const slugRegEx = new RegExp(`^(${this.slug})((-[0-9]*$)?)$`, 'i')
```
2. Query db to see if any entries already exist for that slug
	- `this.constructor.find()` gives us access to the model from inside the model's hook
```js
const storesWithSlug = await this.constructor.find({ slug: slugRegEx })
```
3. If there are any matches for the previously run query, create a new slug that is incremented by 1
```js
if (storesWithSlug.length) {
	this.slug = `${this.slug}-${storesWithSlug.length + 1}`
}
```

[[14 - Custom MongoDB Aggregations]]