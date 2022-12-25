This function uses `readFileSync` from Node's `fs` module to read the image file into a `Buffer`
```
import {readFileSync} from 'fs'

export const returnBase64ImageSrc = (relativePath: string): string => {
	const buffer = readFileSync(relativePath);
	const base64ImageString = buffer.toString("base64");

	return `data:image/png;base64, ${base64ImageString}`;

};
```

We needed to use the `resolve` method from Node's `path` module to use relative paths from whatever file we're working in. Pretty sure that otherwise the relative paths will be fron the `node_modules` folder. At this point we have the base64 string that represents the image.
```
const logo = returnBase64ImageSrc(
	resolve(__dirname, "../assets/reviewpoint-logo-full.png")
);
```

Then we take the string and pass it to an `img` element like so:
```
<img src={logo} />
```

Which after Babel is (or without Babel it would be)
```
<img src="data:image/png;base64; [the base64 string]" />
```

---
https://stackoverflow.com/questions/8499633/how-to-display-base64-images-in-html
