## Edit Store
In our storeCard template, we set up a link on a button in the header that will take us to 
```js
`/stores/${store._id}/edit`
```

`_id` is the field mongodb uses to store its unique identifier for each entry

---
In the route file, we create a GET request to
```js
router.get('stores/:id/edit')
```
`:id` is a variable available on the request object that will contain the id for the route
- it will be on `req.params.id`

---
In our controller, we create an `editStore` action
```js
exports.editStore = async (req, res) => {
	// find the store given the id
	const store = await Store.findOne({ _id: req.params.id })
	
	// TODO confirm user is owner of store
	
	// render edit form for user to update store
	res.render('editStore', { title: `Edit ${store.name}`, store })
}
```

## Update Store
In the _storeForm template:

Need to edit form action so that on a new store, we POST to `/add`, and on a store that already exists we POST to `/add/:id`
```pug
form(action=`/add/${store._id || ''}`)
```

Update input to take current store value if it exists
```pug
input(type="text" name="name" id="name" value=store.name)
```

Update textarea to take current value if it exists
```pug
textarea(name="description" id="description")= store.description
```

Update tags to take currently selected tags from the params if they exist, or empty array so that `tags.includes` doesn't throw
```pug
- const tags = store.tags || []
ul.tags
      each tag in tagChoices
        .tag.tag__choice
          input(type="checkbox" id=tag value=tag name="tags" checked=(tags.includes(tag)))
          label(for=tag) #{tag}
```

---
In the router:
```js
router.post(`/add/:id`, catchErrors(storeController.updateStore));
```

---

In the controller:

```js
exports.updateStore = async (req, res) => {
	// set location data to be of type 'Point'
	req.body.location.type = "Point"
	// find and update the store
	const store = await Store.findOneAndUpdate({ _id: req.params.id }, req.body, {
		new: true, // return new store instead of old one
		runValidators: true, // force model to run validators against the store
	}).exec();
	// redirect to the store and flash that it worked
	req.flash(
		"success",
		`Successfully updated <strong>${store.name}</strong>. <a href="/stores/${store.slug}">View Store</a>`
	);
	res.redirect(`/stores/${store._id}/edit`);
};
```

We have to set the body.location.type to "Point" because `findOneAndUpdate()` apparently doens't trigger the defaults from the schema

[[11 - Upload & Resize Images]]