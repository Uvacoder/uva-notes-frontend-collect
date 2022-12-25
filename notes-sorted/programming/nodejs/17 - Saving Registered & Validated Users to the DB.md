1. We need to import our User model in our `start.js` file
```js
require('./models/User')
```
2. Create `userController.register` method to deal with creating the user and registering it to DB
```js
exports.register = async (req, res, next) => {
	const user = new User({ email: req.body.email, name: req.body.name });
	// .register is on the User schema because we included the passportLocalMongoose plugin in the model
	await User.register(user, req.body.password);
	next();
};

```
3. Create `controllers/authController`
```js
const passport = require("passport");

exports.login = passport.authenticate("local", {
	failureRedirect: "/login",
	failureFlash: "Login Failed!",
	successRedirect: "/",
	successFlash: "You are now logged in!",
});
```
4. Add login middleware to '/register' route
```js
router.post(
	"/register",
	usersController.validateRegister,
	usersController.register,
	authController.login
);
```
5. Configure passport to use local strategy