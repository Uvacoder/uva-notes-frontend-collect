---
path: "/svg"
title: "SVG"
description: ""
tags: ["svg"]
---

## Constraints

* Browser support
    * Inline SVG (IE9+)
    * SVG `uses` not supported in IE, polypill using [svg4everybody]
* Pixel alignment
* File Size
* Customisability
* Inheritance

## Structure

### Size

#### Artboard

Working with artboards that are multiples of 4px makes scaling SVGs to common sizes simple.

The icon glyph should be designed to the smallest size it will render at, commonly this is either an artboard size of 8px or 16px. 

By working at on icons at the smallest base size scaling up to larger sizes is easy, with multiples used to scale the icon where needed, for example:

* 16px &times; 1.5 24px
* 16px &times; 2 = 32px

### Shapes and Paths

To get the best results from SVG icons paths and shapes should be aligned to the pixel.

## Anatomy of a SVG

Lets examine a common SVG glyph, an arrow made from 3 `<path>` objects aligned to the centre of a 16px `viewBox`.

<svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 16 16">
  <g fill="none" fill-rule="evenodd" stroke="#000000" stroke-width="1" stroke-linecap="square" transform="translate(1 .5)">
    <path d="M0.5,7.5 L12.5,7.5"/>
    <path d="M13.5,7.5 L6.5,14.5"/>
    <path d="M13.5,7.5 L7,1"/>
  </g>
</svg>

This glyph is created with the following SVG markup:

```html
<svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 16 16">
  <g fill="none" fill-rule="evenodd" stroke="#000000" stroke-width="1" stroke-linecap="square" transform="translate(1 .5)">
    <path d="M0.5,7.5 L12.5,7.5"/>
    <path d="M13.5,7.5 L6.5,14.5"/>
    <path d="M13.5,7.5 L7,1"/>
  </g>
</svg>
```

Broken down into it's individual parts the glyph can be constructed with:

### The SVG tag

A doctype expressed by `xmlns="http://www.w3.org/2000/svg"`

A `viewBox` of 16px `viewBox="0 0 16 16"` which states the `viewBox` dartboard or canvas position as being
    4. x1 = 0
    5. y1 = 0
    6. x2 = 16px
    7. y2 = 16px

A `width` of `16px` set with the attribute `width="16"`

A `height` of `16px` set with the attribute `height="16"`

### The group tag

A group tag `<g>` wraps all required `<path>` tags and applies:

1. A `fill` of `none` with the attribute `fill="none"`
2. A `fill-rule` of `even-odd` with the attribute `fill-rule="evenodd"`
3. A `stroke` of `#000000` (or black) with the attribute `stroke="#000000"`
4. A `stroke-width` of `1px` with the attribute `stroke-width="1"`
5. A `stroke-linecap` of `square` with the attribute `stroke-linecap="square"`
6. A transform to centre the icon onto the artboard, moving the glyph to 1px in from the left and 0.5px in from the top with the attribute `transform="translate(1 .5)"`

### The path(s)

3 &times; `<path>` objects that specify the lines of the arrow

From [The SVG `path` Syntax: An Illustrated Guide]

> The `<path>` element in SVG is the ultimate drawing element. It can draw anything! I've heard that under the hood all the other drawing elements ultimately use path anyway. The path element takes a single attribute to describe what it draws: the d attribute. The value it has is a mini syntax all to itself. It can look pretty indecipherable. It's a ton of numbers and letters smashed together into a long string. Like anything computers, there is a reason to the rhyme.

`<path d="M0.5,7.5 L12.5,7.5"/>`

<svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 16 16">
  <g fill="none" fill-rule="evenodd" stroke="#000000" stroke-width="1" stroke-linecap="square" transform="translate(1 .5)">
    <path d="M0.5,7.5 L12.5,7.5"/>
  </g>
</svg>

`<path d="M13.5,7.5 L6.5,14.5"/>`

<svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 16 16">
  <g fill="none" fill-rule="evenodd" stroke="#000000" stroke-width="1" stroke-linecap="square" transform="translate(1 .5)">
    <path d="M13.5,7.5 L6.5,14.5"/>
  </g>
</svg>

`<path d="M13.5,7.5 L7,1"/>`

<svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 16 16">
  <g fill="none" fill-rule="evenodd" stroke="#000000" stroke-width="1" stroke-linecap="square" transform="translate(1 .5)">
    <path d="M13.5,7.5 L7,1"/>
  </g>
</svg>


## Scale

The scale of the glyph is updated by increasing the `width` and `height` attributes on the `<svg>` tag, this scales the `viewBox` to the new width and height.

The `width` and `height` attributes can take any CSS property value, for example, `1em` or `1rem` for relative scaling to font size. 

<svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 16 16">
  <g fill="none" fill-rule="evenodd" stroke="#000000" stroke-width="1" stroke-linecap="square" transform="translate(1 .5)">
    <path d="M0.5,7.5 L12.5,7.5"/>
    <path d="M13.5,7.5 L6.5,14.5"/>
    <path d="M13.5,7.5 L7,1"/>
  </g>
</svg>

```html
<svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 16 16">
  <g fill="none" fill-rule="evenodd" stroke="#000000" stroke-width="1" stroke-linecap="square" transform="translate(1 .5)">
    <path d="M0.5,7.5 L12.5,7.5"/>
    <path d="M13.5,7.5 L6.5,14.5"/>
    <path d="M13.5,7.5 L7,1"/>
  </g>
</svg>
```

## Style

The attributes set on the group tag `<g>` that wraps the individual `<path>` objects can be used to change the style of the glyph, for example:

Updating the `stroke` attribute:

<svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 16 16">
  <g fill="none" fill-rule="evenodd" stroke="red" stroke-width="1" stroke-linecap="square" transform="translate(1 .5)">
    <path d="M0.5,7.5 L12.5,7.5"/>
    <path d="M13.5,7.5 L6.5,14.5"/>
    <path d="M13.5,7.5 L7,1"/>
  </g>
</svg>

Updating the `stroke-width` attribute for a bolder glyph

<svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 16 16">
  <g fill="none" fill-rule="evenodd" stroke="#000000" stroke-width="2" stroke-linecap="square" transform="translate(1 .5)">
    <path d="M0.5,7.5 L12.5,7.5"/>
    <path d="M13.5,7.5 L6.5,14.5"/>
    <path d="M13.5,7.5 L7,1"/>
  </g>
</svg>

Updating the `stroke-width` `stroke-linecap` attribute for a bolder rounded glyph

<svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 16 16">
  <g fill="none" fill-rule="evenodd" stroke="#000000" stroke-width="2" stroke-linecap="round" transform="translate(1 .5)">
    <path d="M0.5,7.5 L12.5,7.5"/>
    <path d="M13.5,7.5 L6.5,14.5"/>
    <path d="M13.5,7.5 L7,1"/>
  </g>
</svg>

## Meaning

Providing meaning to an icon glyph is done through the SVG `<title>` and `<desc>` tags, these can be used by screen readers through the `aria-labeledby` attribute and parsing in the values, for example, `aria-labelledby="title desc"`.

```html
<svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 16 16" aria-labelledby="title desc">
<title id="title">Arrow Right</title>
<desc id="desc">A black arrow pointing to the right</desc>
...
</svg>
```

## Preparation

### Individual artboards



### Naming convention



### Organisation



## Export

### Illustrator

### Sketch



#### Sketch SVGO Plugin



## Optimisation

From [SVGO]

> SVG files, especially exported from various editors, usually contain a lot of redundant and useless information such as editor metadata, comments, hidden elements, default or non-optimal values and other stuff that can be safely removed or converted without affecting SVG rendering result.

## Usage

### Inline

#### Pros

* Customisability

#### Cons

* Caching

### Uses



### Spritesheets


[svg4everybody]: (https://github.com/jonathantneal/svg4everybody)
[The SVG `path` Syntax: An Illustrated Guide]: (https://css-tricks.com/svg-path-syntax-illustrated-guide/)
[svgo]: (https://github.com/svg/svgo)
[svg-sprite-generator]: (https://github.com/frexy/svg-sprite-generator)
[svgontheweb]: (https://svgontheweb.com/)
