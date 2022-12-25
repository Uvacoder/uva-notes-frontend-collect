We need to perform multiple asynchronous requests in the `getStoresByTag` method. Rather than `await `ing each promise individually, which will cause synchronous behavior, we use `await Promise.all()` to allow the requests to be fired off simultaneously, and to be resolved as they come back.

Here we define`tagQuery` as either the value that is coming in on `tag` or all of the documents that have the `tags` field using the [`$exists` operator](https://docs.mongodb.com/manual/reference/operator/query/exists/)
```js
const tag = req.params.tag
const tagQuery = tag || {$exists: true}

const tagsPromise = Store.getTagsList()
const storesPromise = Store.find({tags: tagQuery})

const [tags, stores] = await Promise.all([tagsPromise, storesPromise])

res.render("tag", {tags, title: "Tags", tag, stores})
```

Now that we have the stores associated with the tag being passed to our template, we just need to display that data in the template

```pug
extends layout

include mixins/_storeCard

block content
  .inner
    h2 #{tag || "Tags"}
    ul.tags
      each t in tags
        li.tag
          a.tag__link(href=`/tags/${t._id}` class=(t._id === tag ? 'tag__link--active' : ''))
            span.tag__text= t._id
            span.tag__count= t.count
    .stores
      each store in stores
        +storeCard(store)
```