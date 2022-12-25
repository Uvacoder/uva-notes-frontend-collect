# Flow layout
- It's the default layout mode.
- All HTML elements have an intrinsic `display` of either `inline`, `block`, or `inline-block`

## Inline elements
- These are elements like `<strong>` that don't usually affect page layout
- Many CSS properties don't work on inline elements (height, width, etc). they tend to sit exactly where they're assigned
- Two exceptoins:
	- Replaced elements like `<img />`, `<video />`, and `<canvas />` can affect block layout and can be given explicit dimensions
	- `<button>` elements
- To get rid of "extra space" around an image in a bounding container (`div`, etc), either set the image to `display: block`, or set `line-height: 0` on the wrapping div. The gotcha here is that the browser treats inline elements as if they're typography, thus introducint the extra bit of space so that text isn't crammed together too tightly.
- Inline elements can break across multiple lines, but properties like padding don't get consistently applied to each "slice" of the line-broken element unless we use the `box-decoration-break: clone` property. [Relevant MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/box-decoration-break)

## Block elements
- Content box expands to fill entire available horizontal space
- Using `width: fit-content` shrinks a block element down to the minimum size required for the letters. See [this SO](https://stackoverflow.com/a/54123728/4552841)

## Inline-block elements
- Allows you to drop a block element into an inline context.
- They are elements that internally behave like block elements, but externally behave like inline elements.
- Inline-block elements don't line-wrap
