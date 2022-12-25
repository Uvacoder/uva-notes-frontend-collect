1. Add route to router index file `routes/index.js`
```js
router.get('/store/:slug', catchErrors(storeController.getStoreBySlug))
```
2. Add controller to `controllers/storeController.js`
```js
exports.getStoreBySlug = async (req, res, next) => {
	const store = await Store.findOne({ slug: req.params.slug });

	// 404 if the slug / page doesn't exist
	if (!store) return next();

	res.render("store", { store, title: store.name });
};
```
3. Add template to `views` directory
```pug
extends layout

block content
  .single
    .single__hero
      img.single__image(src=`/uploads/${store.photo || 'store.png'}`)
      h2.title.title--single
        a(href=`/stores/${store.slug}`) #{store.name}
    
  .single__details.inner
    img.single__map(src= h.staticMap(store.location.coordinates))
    p.single__location= store.location.address
    p.store.description

    if store.tags
      ul.tags
        each tag in store.tags
          li.tag
            a.tag__link(href=`/tags/${tag}`)
              span.tag__text #{tag}
```

[[13 - Use Pre-Save Hooks to Create Unique Slugs]]