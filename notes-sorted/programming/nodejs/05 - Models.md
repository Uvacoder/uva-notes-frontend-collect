Models are where our data will be stored

It's helpful to do data normalization as close to the model as possible

We need to describe what the data will look like ahead of time

 1. `mongoose` package required to interface with `mongodb` in Node
 2. tell mongoose what promise type to use
	 - `mongoose.Promise = global.Promise;`
	 - [this isn't necessary with `mongoose` 5.0+](https://stackoverflow.com/questions/51862570/mongoose-why-we-make-mongoose-promise-global-promise-when-setting-a-mongoo)
3. bring in `slugs` package to help with url formation 
4. declare schema with `new mongoose.Schema({})`
	- Each key in the schema constructor will be a field on our store in the db
6. export model
	- `module.exports = mongoose.model("Store", storeSchema)`
7. import models into application (in this example we're using `start.js`, the file that deals with connecting to the db and starting the server)
8. we can add hooks to our model, such as `.pre('save')`, to do things before exporting the model
	- we are using a pre-save hook to generate a slug using the slug package and the name defined on `this.name`
	- because we want to access `this`, we can't use an arrow function here

[[06 - Mixins]]