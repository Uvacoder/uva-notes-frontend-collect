[[01 - Routing]]
In our express app, we can add locals to the app environment with a call to `app.use()`:
- If we have a `helpers.js` file that defines a bunch of stuff/libraries that we want to include, we could do something like this:
```js
app.use((req, res, next) => {
	res.locals.helpers = helpers
})
```
- And then in our templates we can access the stuff in the helpers file by just using `#{h.helpers}`

Here, we will be using [pug](https://pugjs.org/api/getting-started.html) as our templating engine. Was formerly known as Jade.
- pug is indentation-based
- pug uses what emmet-style shortcuts for classes and ids
- [other attributes documentation](https://pugjs.org/language/attributes.html)
- pug uses `#{}` to interpolate values inside the template inside of text
	- use template literal interpolation to bring values into string literals
	- we can also directly set locals to tags in the template: `h2=title` (assuming we have a `title` value in our locals object)
- you can run JS inside of pug files, following a `-` or within an interpolated value
	
- `views` folder is where all of our `.pug` templates will live
	- in our express app file, we declare where our views are with:
	 ```js
	app.set("views", path.join(__dirname, "views"))
	```
	- [the `path` module is native to node](https://nodejs.org/api/path.html#path_path) and is used for working with file and directory paths
	- we declare our view/templating engine with:
	```js
	app.set('view engine', 'pug')
	```

- [We use `res.render()` to render out a template](https://expressjs.com/en/4x/api.html#res.render). It takes two things:
	1. The template to render
	2. Locals object

- To get data from our route to our template, we pass it in via the locals object
	- here our template is `hello.pug`
	- the cat value is coming from the query
```js
router.get('/', (req, res) => {
	res.render('hello', {
		name: "Test Name",
		cat: req.query.cat
	})
})
```

- we can set up a base layout template, representing the html document defaults, that can then be shadowed with other values (?)
	- to use the layout (or other) templates, we use `extends layout` at the top of the pug file
- we can use template **blocks** to essentially create template components that can be passed around
- `!=` is [unescaped buffered code](https://pugjs.org/language/code.html#unescaped-buffered-code)
	- This is dangerous because of the potential for cross-site-scripting. If using in a scenario with user-input **always** sanitize the inputs!

[[03 - MVC Pattern]]