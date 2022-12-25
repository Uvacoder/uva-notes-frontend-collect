## 2. [Design and Implement Common Tailwind Components](https://egghead.io/playlists/design-and-implement-common-tailwind-components-8fbb9b19)

 **Playlist** **Description**

Now that we covered fundamentals, we're going to design and implement common components that you will see in the wild. We'll start with a basic Vue.js application and some hard-coded data that will be displayed within the application.

We'll cover styling: 

- Card components
- SVG Icons
- Badges
- Images

### 2.1 Structure a Basic Card in Tailwind

**Description**

Before styling, we'll check out what data we're dealing with by dumping it into the browser to see how it fits with some initial HTML structure.

Once the structure is in place we'll start applying style to the card at the root level. The way I like to think of the root level is the styles that affect the edges of the card and only apply those styles to it. For example, we'll add a background color and border radius to the card we are styling. If we want to add padding or style to the conent of the card, we will group that content and apply the necessary styling directly which won't affect the root level styles.

---

 We'll group the data within the card and apply the necessary padding 

structure card with H4, image, and divs

add background card

likes to design cards as thinking of the root level as thinking just of the edges of the card.

If you want padding within the card, you group data there and add it.

well see that adding rounded corners to the card will not style as we expect because the image is set to fill up to the edges of the card. `overflow-hidden` will take care of this so the corners that now protrude outside of the card will be hidden

### 2.2 Making Text Feel Designed

→ Make Text Feel Professionally Designed with Tailwind

→ Design Text in a Tailwind Card to Emphasize Important Content

**Description**

The content in our card is currently pretty bland with the browser defaults. In this lesson we'll work through how to apply style to the text content to make it catch the eye.

We'll start by adjusting the browser default color as well as the antialiasing (which will make our cards look better on high res displays). Then we'll work through the text content to highlight the important parts, with bold, dark text and de-emphasizing the less important content by making it lighter and smaller.

---

**Notes**

antialiased - Tells the browser to use regular antialiasing instead of sub-pixel antialiasing. Regular antialiasing will look alot crisper on Retina displays.

Modify the text color to be a very dark grey (`text-gray-900` ) which is a lot less harsher on the eyes than the default black that the browser sets

The title needs to stand out as the primary content of the card.

We'll make the font bolder. with font-semibold

play with the font size with text-lg

to make the title really pop, we need to de-emphasize the other content

Change the color to be lighter `text-gray-600` which is still clear to read

make the font size smaller - with text-xs

A trick to get away with smaller text is to make it uppercase and bold it a little so it's still very readable but clearly de-emphasized

Uppercase can be hard to ready because it looks cramped. You can adjust the letter spacing with `tracking-wide` 

The price looks really vanilla as it currently is. we'll de-emphasize the `/ wk` because it's a little less important than the actual price.

Things have a weird balance with the big title and small text then normal text. The way people fix this is to add an 'eye brow' to the title so in our case we'll add the bed and bath text up above the title to balance the proportions of all of the text.

Rating looks cramped next to the other content.

We'll add margin to the top of the content and de-emphasize the less important part of the text the same way we did with the price per week. We'll make the text smaller as well as lighter. `text-gray-600` and `text-sm`

Give the rating an accent color so that it stands out a bit more. with `text-teal-600` and make it easier to read with `font-semibold` because the color is harder to read 

`08:30` - Handle awkward sample data - in our case, a really long title string

The text wraps in the card and it looks off

equal space between the wrapped title text and price (other content)

 **The line height between wrapping text should always be smaller than the spacing between other content and text.**

Adam likes to use top margin than bottom margin. The top margin gives the feel that the element that you are styling moves where the bottom margin makes the element below it move. **The element that the class is added to should be the element that changes visually.**

Add's top-margin to price with `mt-1`

Makes the line spacing smaller with `leading-tight` 

Maybe consider truncating text instead of adjusting the styles. The adjusted height could look weird in a list

### 2.3 Working with SVG Icons

→ Style SVG Icons with Tailwind Utility Classes 

**Description**

In this lesson, we'll be replacing the text based rating in our card to use svg icons to signal how the property is rated.

To do this, we'll start with a custom, raw SVG icon that was exported from sketch (best to export as square for easier styling). One thing to note is that this file is much bigger than you need it to be when it's exported. To clean it up, you can run it through a service like [SVGOMG]([https://jakearchibald.github.io/svgomg/](https://jakearchibald.github.io/svgomg/)) that will reduce the file size drastically. After this, we'll remove the SVG color and sizing and use Tailwind utilities classes to style these icons how we'd like them, with `h-` / `w-` utilities for size and `fill-current` for color. 

Lastly, the icons positioning will be adjusted with Tailwinds flexbox utility classes.

---

**Notes**

svg-icons is my go-to when I want to import icons into a tailwind project because there is a lot of cool ways you can apply styles to an SVG

Tailwind docs has an icons section for free icon sets.

there is another step in the workflow to add icons to your tailwind project if it a custom icon that you a receiving from a designer

This lesson use a raw SVG icon that was exported from sketch. These raw icons come with a lot of data that isn't necessary for showing on your site.

SVGOMG [https://jakearchibald.github.io/svgomg/](https://jakearchibald.github.io/svgomg/) will remove that extra data that you don't need. just copy past it in and the service will trim the svg for you.

remove any in-line svg height and start styling with tailwind classes

removes and adds tailwind `h-4` `w-4` to it to adjust height

Working with a square svg is much easier to deal with.

the svg will have a baked in `fill` that colors the svg.

`fill-current` tells the svg to fill with the current text color and then apply our own text color, in this case `text-red-500` 

We'll dynamically add the text color based on whether it's filled or not.

To get the stars rendering next to eachother (instead of stacked) we can just add `flex` to it 

Adds a dynamic vue class to correctly fill the colors. If current index is ≤ currentRating in data, fill with a teal text color, otherwise color it grey.

centers all of the items in the flex container with `items-center`

adjust margin

key takeaways: always try to export your icons as squares so it's easier to size them, use tailwinds height and width properties when you want to size the svg, control the collor with `fill-current` and text color utilities, and then tailwinds flexbox utilities can control the positioning of the svgs 

### 2.4 Designing a Badge

→ Use Tailwind to Design a span that Looks like a Badge

**Description**

In this lesson, we'd like to highlight that this listing is new. To do this we'll need to build a badge that will do just that.

The badge will be an inline element with the text right above the title as a span. We'll see how to color, position, and size it with Tailwind utility classes. 

Some classes we will use: 

- `inline-block` for correct padding behavior in the span
- `bg-teal-200` and `text-teal-800` to adjust color
- `uppercase` `font-semibold` `tracking-wide` to adjust the look of the badge text
- `flex` and`items-baseline` to adjust the positioning

---

**Notes**

create a span because the badge is an inline thing

Badges usually have a background color.

adds `bg-teal-500`

adjust the text color to white for better readability

Adjust the text to match the content that it will appear right next to. with `text-xs`

Adjust the padding of the badge so that the text isn't butting up next to the edge of the badge

This reveals another problem though, the padding doesn't move any other content around it so it will barge into other content on the screen if it's too big or is placed poorly.  which is because the span is set to `inline` - we'll set it to `inline-block` so it behaves how we want it to.

Round the corners with `rounded-full` 

Adds `uppercase` `font-semibold` `tracking-wide` to give it a more emphasized look

Will add flexbox to the div that the span and text content is in so that we can properly aline the badge horizontally with the text content.

Design components in the most flexible and adaptable way possible to that captures you intention with the design as much as possible even when something doesn't necessarily need the design. That way when it's repurposed, your intention is still captured in another context. adds `items-baseline` which aligns the bottom of the text content in the div to be even regardless of the size of each piece of text.

**As a general rule, try to align different font sizes by their baseline which is the most readable.**

In our case, the alignment issue doesn't really matter because both text is xs but it would be more flexible if someone in the future adjusted the font size of one of the two items.

A lot of the time, having a badge that has a dark background will steal the attention from the rest of the content (which isn't always bad) but if you don't want that to happen, you can reverse the text and background colors. set the background color (in this case `bg-teal-200`) to a light color and the text color to the dark (`text-teal-800`).

### 2.5 Cropping and Positioning Images

→ Crop and Position Images with Tailwind object-fit Utilities

**Description**

The intrinsic aspect ratio has been controlling the look of the image in our card. If we wanted to adjust the styling of the image it could scale and distort in ways that wouldn't look good.

We need to tell the browser how to render the object regardless of the size. In Tailwind, we use the `object-fit` utilities which will let us crop and size an image in a way that works for our use-case. 

Note: IE11 doesn't support this feature so we'll see how we can get around this with setting the image as a backgroundImage style. This accessible so should be avoided whenever possible.

---

**Notes**

start by forcing the image to a different size with `h-` that shows that image does distort at different sizes.

**We need to tell the browser how to render the object regardless of the size**. In Tailwind, we use the `object-fit` utilities

`object-contain` which will show the the full image without any scaling

`object-cover` will fill the whole area we have specified but not distort them image. This is the one that gets used quite a bit.

default positioning is `object-center` which centers the image in the frame. `-top` `-right` `-left` will move the image around depending on how it got cropped.

set's image height to `h-48`

IE11 doesn't support `object-fit` so you'll have to handle this case differently

To handle it, we'll assign the image as a backgroundImage style. then we can use utilities like `bg-cover` and `bg-center` 

use an img tag whenever possible because things like screenreaders won't know of the image when it's set to the background.

### 2.6 Locking an Image to a Fixed Aspect Ratio

→ Lock an Image to a Fixed Aspect Ratio with Percentage-based Padding in Tailwind

**Description**

Right now the card looks great at this screensize but when that is adjusted (and gets larger) you'll notice that the image resolution will stretch to fit the screen. We will want to respect the original aspect ratio of the image so as the image gets wider, it gets proportionally taller.

To respect the original aspect ratio of the image, we'll need to position the image `absolute`ly in a containing div that has its bottom padding set to a percentage. This will fix that div's aspect ratio which in turn will keep the images aspect ratio fixed as well.

---

**Notes**

**CSS doesn't allow you to control the aspect ratio of an image**

we can create a box in the browser with a fixed aspect ratio in a div. There's a weird quirk in CSS where if you set padding to a % value, that % is always based on the width of the element.

We'll use this quirk to extend tailwinds design system and introduce some % base padding in some utility classes.

This will be done in the tailwind.config.js file and extend the spacing with percentages.

so now you can use `pb-2/3` but the padding will be added to the bottom of the div in addition to the space that the image is taking. 

To fix that, the give the image the `absolute` positioning which will take the image out of the regular document flow and not affect the size of the div that is containing it or anything around it.

Then we can use utilities to position the element which it will find the 'nearest positioned element' which by default is the view port or body element.

to make the containing div a positioned element we'll add `relative` - this makes the element position itself exactly the way it would by default but can now be used as a reference for any nested absolute positioned elements.

give the image a `h-full` and `w-full` to fill that div all the way.

### 2.7 Creating Depth with Shadows and Layers

→ Create Depth in a Tailwind Component with Shadows and Layers

**Description**

The card is designed with a pretty flat. We can add depth through shadows and layers to make it look even better. This will make it look like some elements are closer and some farther away.

To do this, we'll make the images containing div `relative` so that we can pull the text content on top of the image with a negative margin (`-mt-4`). We'll adjust the style of the image and content to look great in a layered fashion with adjusting the shadow of each section of the component.

---

**Notes**

add a `shadow` class around the card instead of a border.

this can add a lot of polish.

You can overlap elements to make it look like theres layers on the page.

We'll set the content of the card to look like it's floating a little on top of the image.

give the content a white background.

create a container div with `px-4` which will make the content width a little smaller than the image

negative margins allow us to pull elements into space that they wouldn't normally be able to with `-mt-4`. but right now the image is positioned on top of other divs that are not positioned which is default `static` 

z index doesn't affect elements that are unpositioned

We'll add position `relative` so that the z index will take effect but we don't even need the z index because both of these elements are positioned.

change aspect ratio of the image to be a bit taller now that the content is floating on top with `pb-5/6` (this is a custom extension for % based padding in tailwind)

You can combine the layering with a shadow to make the style look really good. Make sure to give the top layer a bigger shadow than the bottom layer.

Use different sizes of shadows to change how close or far away you want the element to feel.
