- Why use MongoDB aggregations?
	- They allow us to take some of the collection-level logic away from Node-land and into the database

1. add routes to index file `routes/index.js`
```js
router.get('tags', catchErrors(storeController.getStoresByTag))
// tags/:tag*? would also work, but below is more explicit
router.get('tags/:tag', catchErrors(storeController.getStoresByTag))
```

2. add controller to `storeController`
	- `getTagsList()` will be a static method that we declare on the `Store` model
	- once we have the tags, render a tags template
```js
exports.getStoresByTag = async (req, res) => {
	const tags = await Store.getTagsList()
	res.render('tags', { tags, title: 'Tags' })
}
```

3. add static function to `Store` model
```js
storeSchema.statics.getTagsList = function() {
	return this.aggregate([
		{ $unwind: "$tags" },
		{ $group: { _id: "$tags", count: { $sum: 1 } } },
		{ $sort: { count: -1, _id: -1 } },
	])
}
```
- The aggregation pipeline (`this.aggregate`) is how we process data with mongodb
- [`$unwind`](https://docs.mongodb.com/manual/reference/operator/aggregation/unwind/) deconstructs the array field (`"$tags"`) and outputs a document for each element
	- So in this example, with tags, we'll get a copy of each store that has the value of each tag that was specified. If a specific store has 3 tags, `$unwind` will output 3 different documents for that store corresponding to each tag.
- [`$group`](https://docs.mongodb.com/manual/reference/operator/aggregation/group/) creates a document for each unique `_id` field, which here is `$tags`, and also creates a new field in each document called `count` that will be incremented by one each time another item is added to the document
	- `$sum` is the [*accumulator*](https://docs.mongodb.com/manual/reference/operator/aggregation/group/#accumulators-group)
	- `$group` **does not order the output documents**
- [`$sort`](https://docs.mongodb.com/manual/reference/operator/aggregation/sort/) sorts the resulting documents that the pipeline has created
	- -1 sorts descending
	- 1 sorts ascending
	- I also had to add the `_id: -1` field to get the documents to consistently come back in the same order
4. create template in `views` dir
```pug
extends layout

block content
  .inner
    h2 #{tag || "Tags"}
    ul.tags
      each t in tags
        li.tag
          a.tag__link(href=`/tags/${t._id}` class=(t._id === tag ? 'tag__link--active' : ''))
            span.tag__text= t._id
            span.tag__count= t.count
```

[[15 - Multiple Query Promises Async-Await]]