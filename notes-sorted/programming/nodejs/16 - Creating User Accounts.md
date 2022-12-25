1. Add login route to router file
```js
router.get('/login', userController.loginForm)
```
2. Create `controllers/userController` file & require in `routes/index.js`
```js
const mongoose = require("mongoose");

exports.loginForm = (req, res) => {
	res.render("login", { title: "Login" });
};

```
3. Create `login.pug` template in `views` dir and `_loginForm` mixin in `views/mixins`
```pug
//- login.pug
extends layout

include mixins/_loginForm

block content
  .inner
    +loginForm()
```

```pug
//- mixins/_loginForm.pug
mixin loginForm()
  form.form(action="/login" method="POST")
    h2 Login
    label(for="email") Email Address
    input(type="email" name="email")
    label(for="password") Password
    input(type="password" name="password")
    input.button(type="submit" value="Log In ->")
```
4. Create User model
```js
const mongoose = require("mongoose");
const Schema = mongoose.Schema;
const md5 = require("md5");
const validator = require("validator");
const mongodbErrorHandler = require("mongoose-mongodb-errors");
const passportLocalMongoose = require("passport-local-mongoose");

const userSchema = new Schema({
	email: {
		type: String,
		unique: true,
		lowercase: true,
		trim: true,
		validate: [validator.isEmail, "Invalid Email Address"],
		required: "Please supply an email address",
	},
	name: {
		type: String,
		required: "Please supply a name",
		trim: true,
	},
});

userSchema.plugin(passportLocalMongoose, { usernameField: "email" });
userSchema.plugin(mongodbErrorHandler);

module.exports = mongoose.model("User", userSchema);

```
- For server-side email validation we're using [validator](https://www.npmjs.com/package/validator)
	- Note that validator is only used for validating and sanitizing strings
- For the password, we're using [Passport](http://www.passportjs.org/) as a plugin on `userSchema`
- We're using [mongoose-mongodb-errors](https://www.npmjs.com/package/mongoose-mongodb-errors) to create better server error messages

5. Add register routes to router file
```js
router.get("/register", userController.registerForm);
```
6. Add register controller to controllers file
```js
exports.registerForm = (req, res) => {
	res.render('register', {title: Register})
}
```
7. Create `register` template and `_registerForm` mixin
```pug
//- register.pug
extends layout

include mixins/_registerForm

block content
  .inner
    +registerForm()
```

```pug
//- _registerForm.pug
mixin registerForm()
  form.form(action="/register" method="POST")
      h2 Register
      label(for='name') Name
      input(type="text" name="name" required)
      label(for="email") Email
      input(type="email" name="email" required)
      label(for="password") Password
      input(type="password", name="password")
      label(for="password-confirm") Confirm Password
      input(type="password", name="password-confirm")
      input.button(type="submit" value="Register →")
```
8. We also need to be able to post to the `/register` route, in order for users to be able to create an account that persists on our server
```js
router.post('/register', userController.validateRegister)
```
- In order to do this safely, we also need to validate the request before sending it to the server
- We do this by defining a `validateRegister` method in our `userController`
- We use [express validator](https://express-validator.github.io/docs/)to do this in a `validateRegister` method in our `userController`
	- express validator provides us with the methods `sanitizeBody`, `checkBody`, `notEmpty`, `normalizeEmail`
	- If there are errors, they are added to the `req.validationErrors` object, which we can check at the end to see if we are good to send the request along to the next step
```js
const {check, validationResult} = require('express-validator')

exports.validateRegister = (req, res, next) => {
	check("email")
		.notEmpty()
		.isEmail()
		.normalizeEmail({
			gmail_remove_dots: false,
			gmail_remove_subaddress: false,
		})
		.withMessage("That is not a valid email");
	check("name")
		.notEmpty()
		.trim()
		.escape()
		.withMessage("You must supply a name");
	check("password", "Password must be at least 8 characters")
		.notEmpty()
		.isLength({
			min: 8,
		})
		.withMessage("Password must be at least 8 characters");
	check("passwordConfirm")
		.notEmpty()
		.isLength({ min: 8 })
		.withMessage("Confirmed password cannot be blank");

	const errors = validationResult(req);

	if (!errors.isEmpty()) {
		req.flash(
			"error",
			errors.mapped((err) => err.msg)
		);
		res.send({
			title: "Register",
			body: req.body,
			flashes: req.flash(),
		});
		return;
	}
	return next();
};
```

[[17 - Saving Registered & Validated Users to the DB]]