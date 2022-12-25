Inside of `/routes/index.js`:
1. Import `express`
	```js
	const express = require('express')
	```
2. Grab `Router` off `express`
	```js
	const router = express.Router()
	```
3. Define routes
	- The routes look like this:
	```js
	router.get('/', (req, res, next) => {
		res.send('Test text')
	})
	```
	- req = request containing the information that is coming in
	- res = object full of methods for sending data back to user
	- next = method to pass the request off to another step/middleware
	- You can only send one response per route, or you'll get a 'headers have already been sent' error (or something like that)
	- URL parameters are available on the request object in the query object
		- `req.query.paramName`
5. The routes index file gets exported, then imported into our app file. Inside of the app file, we call `app.use('/', routes)` to tell express that anytime we hit a route that starts with `/`, use our routes index.
	- Could also add more paths to hit with different routes
		- `app.use('/admin', adminRoutes)`, for example

- Can use [route parameters](https://expressjs.com/en/guide/routing.html#route-parameters) to grab variable values off the URL query and put them on the request object
```js
router.get('/reverse/:name', (req, res) => {
	const reverse = [...req.params.name].reverse().join("")
	res.send(reverse)
})
```

- Can use `res.render()` to render out a response using a templating engine

[[02 - Pug Templating]]