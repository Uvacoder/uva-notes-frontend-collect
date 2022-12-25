Basic middleware definition: **work to be done in between the request coming in and the response going out**

Chain middleware using the `next()` method, which is the third argument of each controller function, building up the request object before the response

Express has [router-level middleware](http://expressjs.com/en/guide/using-middleware.html#middleware.router) which is bound to an instance of `express.Router()`

Express also has [application-level middleware](http://expressjs.com/en/guide/using-middleware.html#middleware.application) which is bound to an instance of the [app object](http://expressjs.com/en/4x/api.html#app)

The bottom of the app file is where we catch errors and handle them with error-handling middleware

[[05 - Models]]