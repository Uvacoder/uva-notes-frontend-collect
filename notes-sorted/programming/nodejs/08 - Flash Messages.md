Flash messages are just divs showing messages on the page

We're using the [`connect-flash`](https://www.npmjs.com/package/connect-flash) npm package as our middleware to create flash messages

we are using 'success', 'warning', and 'error' values as the first argument to flash

we add the flashes to the locals object in our express app

then in our `layout.pug`, we have a messages block

[[09 - Querying Database]]