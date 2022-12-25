## 1. [Introduction to Tailwind and the Utility first workflow](https://egghead.io/playlists/introduction-to-tailwind-and-the-utility-first-workflow-0b697b10/edit)

---

**Playlist Description**

Everything you need to know about how to design beautiful custom designs from scratch with Tailwind.

You'll learn how to:

- install tailwind in your project
- design with the utility first workflow
- use tailwind for responsive design
- Extract Tailwind component classes

post-css plugin might already be built in the environment you are using. 

### 1.1 Setting up Tailwind and PostCSS

**Description**

In this lesson we'll introduce Tailwind to a basic HTML project and see how it compiles into CSS with PostCSS. Tailwind can be configured in the `tailwind.config.js` file where you will define plugins for PostCSS to compile.

After that, we'll spin the project up with `live-server` and introduce styling with Tailwind utility classes

---

**Notes**

`START` - `01:34` **introduction and can be cut and added as it's own lesson**

`01:34` **Set up Tailwind and PostCSS in a HTML project**

postcss-cli processes tailwind 

autoprefixer will add vender prefixes to your css

npx tailwind init - creates tailwind.config.js which is where you config tailwind

postcss.config.js is where you define what plugins you want to use with tailwind - the first being tailwind itself. Then autoprefixer so you can automatically create vender-prefixes

Start using with `@tailwind base` `components` and `utilities` 

need a build script that uses postcss with the input file of tailwind.css and an output file which will generate a new css file that will be used in your project

`06:13` - starts using tailwind

preview in the browser with `live-server` 

demonstrates using utility classes

### 1.2 The Utility-First Workflow

**Description**

Learn how to style HTML elements with Tailwinds utility classes.

We'll adjust size and positioning with padding, margin, and height as well as style text elements color, weight, and spacing through more utility classes

---

**Notes**

`START` - `03:23` **Style a logo image with Tailwind Utility padding and height Classes**

Adjust the size of the logo with px-8 and py-12. You can just use p-1 if the padding is consistent all the way around the div. The height of the image is adjusted with h-10 class.

`03:23` - `04:55` - **Size and Style a splash image**

margin with mt-x

rounding corners with rounded-lg

shadow the image with shadow-xl

`04:55`-`07:55` **Header style with Tailwind**

position the text with margin mt-6

font size is `text-2xl` weight is `font-bold` color is `text-gray-900` and space between lines is `leading-tight`

you can further customize text by adding a span so in this instance coloring part of the header with `text-indigo-500`

`07:55` - `09:00` **p tag header**

margin with mt-2

text-gray-600 - adjust the coloring

`09:00`- `END` **Style a Button**

mt-4

inline-block - links are inline elements by default so you can't add padding to a tags right away, inline-block lets you do this

add's color with bg-indigo-500 

rounded corners with rounded-lg

padding with px-5 and py-3

add shadow with shadow-lg

text-white for white text

uppercase to make 

tracking is the term for letter spacing so `tracking-wider`

font-semibold

and then font size g

### 1.3 Making things responsive

**Description**

Tailwind has a set of Responsive breakpoints that you can add to any utility class. We'll see in this lesson how to apply `sm`, `md`, `lg`, and `xl` breakpoints to style according to the screen that you are targetting.

---

**Notes**

`START`-`02:51` **Understand Tailwind Responsive Breakpoints**

Constrain the width of the design

max-w-md - clamped down to 25 rem wide

Tailwind has responsive utility classes

tailwind ships with 4 default breakpoints

sm - 640

md - 768

lg - 1024

xl - 1280

All you need to do is pre-fix utilities with the size of the breakpoint that you want

e.g. sm:bg-green-500 md:bg-red-500

styles will cascade from the smallest to the largest until it runs into another breakpoint

`02:51`- `05:31` **Adjust Styles on a Small Screen with Tailwinds sm Breakpoint**

we know we're on a small screen no so we'll need to style accordingly.

Make the image smaller with sm:h-64 and stretch the image to the max width with sm:w-full. This distorts the image so we use sm:object-cover to make sure the image isn't distorted and sm:object-center to make sure the image loads in the center.

Style adjustments are made to the header, text, and button to fit the small screen better

`05:31` - `11:24` **Adjust Styles for a Large Screen in Tailwind**

There is alot more room to work with in the large screen so we will want to utilize that. to do so, we'll create a second container for the image when the screen size is large.

use flex to get both containers side-by-side

Hide new container with `hidden` and `lg:block` which will show the image when the screen is large

make each sides equal width with lg:w-1/2

set lg:max-w-full so it takes up the full half of the screen.

new image container gets an lg:relative so it is a positioning reference

image itself will get absolute and inset-0 which stretches it to the full size as well as h-full w-full and use object-cover object-center to not distort image

vertical and horizontal padding for the left container

`11:24` - `END` - **Apply Tailwind Utility Class Styles for Extra Large Screens**

for XL screens - set a max width so text doesn't fill container and stretch allll the way out

and the set left margin auto so text stays close to image

### 1.4 Style with on Hover and Focus with Variants

**Description**

Tailwind has variants that you can use when you want to apply styles conditionally to elements. We will start off with the `hover` and `focus` variants.

One thing to note is that not all variants are available to you out of the box (e.g. the `active` variant) to save on file size when you get started with Tailwind. Additional variants can be configured to add functionality.

We'll finish the lesson by combining and adding custom Tailwind Variants.

---

**Notes**

prefix a regular background color utility with `hover` so in this case we'll apply `hover:bg-indigo-400` 

focus works the same `focus:outline-none` and then `focus:shadow-outline` which will apply a nice focus outline to the button

`01:41` - `04:26` active button styling is disabled out of the box for tailwind to save on file size.

you'll need to adjust the config with Variants. Referes to things like hover focus active and sm or lg.

to add a variant in variants: backgroundColor: ['active']

when you explicitly add a variant, you'll need to add all the other variants that were included by default

the order you include in the variants array matters. when hover styles are defined at the end, they'll over ride active styles

`04:26` - `END` **Combine and Add Custom Tailwind Variants**

Variants can be chained e.g. `md:hover:bg-green-400`

Variants aren't available for every utitlity class but only the common ones. You can enable this in the config by adding the specific class to the variants object and apply the variants you want.

### 1.5 Composing Utilities with @apply

**Description**

The @apply directive lets you compose utility classes so you can re-use common styles and not litter your html with a ton of repetitive styles.

Even when using @apply directives, it's still easy to start repeating yourself in your code. We'll use the multi-class component pattern to extract the common styles into a base class and then styling (e.g. color) can be additionally applied as another class.

---

**Notes**

`START`-`05:52`

The @apply directive lets you compose utility classes so you can re-use common styles and not litter your html with a ton of repetitive styles.

go to your tailwind.css file and add a css class. e.g. `.btn` and inside prefix @apply and all the styles you want.

this needs to be in-between the `@include components` and `@include utilities` 

You can still layer utility classes on it because the `btn` is declared before

use a —watch flag on the build script so tailwind will re-build the file when we edit it.

variants don't currently work with the directive.

in tailwind.css you have to @apply the directives like you would 'normal' css.

@screen sm will reference tailwinds breakpoints variants for your responsive styles

some styles you don't want make global so you can add those back to the specific use-cases that need the styles

`05:52` - `END`- **Avoid Style Duplication in Tailwind @apply Directives with Multi-Class Component Pattern**

Even when using @apply directives, it's still easy to start repeating yourself in your code. We'll use the multi-class component pattern to extract the common styles into a base class and then styling (e.g. color) can be additionally applied as another class.

### 1.6 Extract Reusable Components in Tailwind

**Description**

The styles aren't the only thing that can be duplicated - often times HTML structure is repeated in our applications. You don't want to just pull out the styles in a @apply directive.

This is where JavaScript comes in handy. We have the data available to us so we'll loop through that data and build repeated card components with Tailwind

### 1.7 Customize the Tailwind Design System

**Description**

Sometimes you'll need to customize things for the exact look and feel you need within your application. This can range from any number of things like: breakpoints, color palette, and custom fonts.

The tailwind config file, you can customize all the values that tailwind uses for it's utility classes so that Tailwind works for you and your needs.

### 1.8 Remove unused CSS with Purgecss

**Description**

Out of the box, tailwind generates a lot of css. For example, every background color, text color, and border color needs an object generated for it with each gradient available. In addition, more classes need to be generated for each breakpoint defined within tailwind as well as any variant that is available. Thousands and thousands of utility classes are generated.

Learn how Purgecss can remove all unused classes in your project.
