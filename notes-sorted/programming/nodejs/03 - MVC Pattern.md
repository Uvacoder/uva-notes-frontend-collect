View = pug templates
Model = code that deals with accessing data in db
Controller = code that deals with requesting data and passing it to the view

One approach is to create a controller for each functional 'section' of the site

Each controller will export a named function that deals with rendering each route

```js
exports.homePage = (req, res) => {
	res.render('index')
}
```

[[04 - Middleware & Error Handling]]