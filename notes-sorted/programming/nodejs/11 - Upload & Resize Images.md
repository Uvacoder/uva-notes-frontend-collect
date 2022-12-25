Using [`jimp`](https://www.npmjs.com/package/jimp), [`multer`](https://www.npmjs.com/package/multer), and [`uuid`](https://www.npmjs.com/package/uuid)

- `uuid` generate universally unique identifiers, we're using uuid v4

- `multer`
	- deals with `enctype="multipart/form-data"`
	- is used in our `exports.upload` option in our controller
	- takes an options object
```js
const multerOptions = {
	storage: multer.memoryStorage(),
	fileFilter(req, file, next) {
		const isPhoto = file.mimetype.startsWith("image/");

		if (isPhoto) {
			next(null, true);
		} else {
			next({ message: "That filetype isn't allowed!" }, false);
		}
	},
};		
```

- `jimp`
	- deals with resizing images
		- read the file
		- call the resize method on the file
		- write the file to fs
```js
// image resize middleware with jimp
exports.resize = async (req, res, next) => {
	// check if there is no new file to resize
	if (!req.file) {
		next(); // skip to next middleware
		return;
	}

	// grab the file extension from the mimetype
	const extension = req.file.mimetype.split("/")[1];
	req.body.photo = `${uuid.v4()}.${extension}`;

	// resize the photo
	const photo = await jimp.read(req.file.buffer);
	// width 800 auto height
	await photo.resize(800, jimp.AUTO);
	await photo.write(`./public/uploads/${req.body.photo}`);

	// once photo is written to fs, continue
	next();
};
```

## Adding these middleware to router
```js
router.post(
	"/add",
	storeController.upload,
	catchErrors(storeController.resize),
	catchErrors(storeController.createStore)
);
router.post(
	`/add/:id`,
	storeController.upload,
	catchErrors(storeController.resize),
	catchErrors(storeController.updateStore)
);
```

[[12 - Routing & Templating Individual Pages]]