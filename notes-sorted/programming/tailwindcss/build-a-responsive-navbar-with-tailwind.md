# 3. [Build a Responsive Navbar with Tailwind](https://egghead.io/playlists/build-a-responsive-navbar-with-tailwind-4d328a35) 

 **Playlist** **Description**

The Navbar is a common component you will find yourself styling in almost any application. In this collection, we'll style a Navbar for a mobile view with a logo and toggleable hamburger button that will contain nav links.

After building up the mobile view, we will refactor the navbar to be responsive by removing the hamburger menu from the navbar and replacing that with the links directly inline within the Navbar

---

The navbar is a common component that you'll find yourself styling in almost any application. In this lesson we'll start with the HTML structure of the navbar and end with styling it to look good.

We'll import an image to use as a logo in the navbar as well as a hamburger svg that we'll use for a menu button. Both these items need to be positioned within the navbar so we will add flexbox and see how easy it is to align these items vertically and horizontally 

---

Now that we have the navbar set up in a static fashion, we want to make the button that was added to drop down into a menu on click.

We'll start by adding the markup and then style that. The mark up will need to be refactored a bit so that flexbox is only affecting the navbar and not the menu that is generated. After the refactor, we'll color and size the menu with Tailwind Utility classes.

Finally, to get the menu to show and hide on click, we'll add a Vue `@click` directive that will toggle component state which in turn controls Tailwind classes that control whether the menu is hidden or shown.

---

We started by building just the mobile layout of the navbar which looks great but wont on larger screens. We'll want to handle each screen size and adjust the style on each breakpoint. When the navbar is big enough, we can fit the links within the navbar instead of dropping them down below.

In this lesson, we will use the `sm` breakpoint to start styling the navbar for screens that are larger than mobile.

### 3.1 Building a Navbar Layout with Flexbox

→ Build a Navbar Layout using Tailwind and Flexbox

**Description**

The navbar is a common component that you'll find yourself styling in almost any application. In this lesson we'll start with the HTML structure of the navbar and end with styling it to look good.

We'll import an image to use as a logo in the navbar as well as a hamburger svg that we'll use for a menu button. Both these items need to be positioned within the navbar so we will add flexbox and see how easy it is to align these items vertically and horizontally 

 

---

**Notes**

Build a responsive nav bar

we'll start with the mobile view because that's what Tailwind encourages 

start by putting the HTML structure together and then style the nav bar after

logo on left, links and hamburger menu on the right.

add background color for the nav bar.

`bg-gray-900`

a button wraps the svg to make it clickable 

add `text-white` so that `fill-current` will make the logo white

style the svg so we can see it `h-4` `w-4` `fill-current`

text-gray-500

focus:text-white

focus:outline-none

hover:text-white

`float-right` doesn't really work, we'll use flexbox

add flex to parent element so that it becomes a flex container

this will have everything stack in the container from left to right with no spacing

`align-items` adjusts the vertical positioning of the items in the container

`items-center` will center all the pieces in the container

`justify-between` to get the logo on the left and button on the right

style logo height `h-8` which the width will auto scale to the height

 

### 3.2 Toggling the Navbar Links on Mobile

→ Toggle Navar Menu Links in Tailwind with Vue

**Description**

Now that we have the navbar set up in a static fashion, we want to make the button that was added to drop down into a menu on click.

We'll start by adding the markup and then style that. The mark up will need to be refactored a bit so that flexbox is only affecting the navbar and not the menu that is generated. After the refactor, we'll color and size the menu with Tailwind Utility classes. 

Finally, to get the menu to show and hide on click, we'll add a Vue `@click` directive that will toggle component state which in turn controls Tailwind classes that control whether the menu is hidden or shown.

---

**Notes**

Now that we have the navbar set up in a static fashion, we want to make the button that was added to drop down into a menu on click.

We'll start by adding the markup and then style that.

add a div

then add a tags within

add wrapper header so that the new div will appear below the current navbar template.

make links display block so they stack

add `text-white` `font-semibold` 

add padding to the container with `px-4` `pt-2` `pb-4`

add hover state

`hover:bg-gray-800` 

add `rounded` `px-2` `py-1` as well as `mt-1` to add some vertical spacing 

Add the toggle feature which isn't really tailwind but will be useful to see what tailwind classes to toggle

add `isOpen` to vue component state

`:class="isOpen ? 'block' : 'hidden'`

`@click="isOpen = !isOpen"` to the button to actually toggle the value.

svg is just html so you can add a `v-if` to change the icon that is shown when the button is clicked.

### 3.3 Making the Navbar Responsive

→ Prefix Tailwind Utility Classes with Breakpoints to Make a Responsive Navbar 

**Description**

We started by building just the mobile layout of the navbar which looks great but wont on larger screens. We'll want to handle each screen size and adjust the style on each breakpoint. When the navbar is big enough, we can fit the links within the navbar instead of dropping them down below.

In this lesson, we will use the `sm` breakpoint to start styling the navbar for screens that are larger than mobile.

---

**Notes**

We started by building just the mobile layout of the navbar. We'll want to handle each screen size and adjust the style on each breakpoint. When the navbar is big enough, we can fit the links within the navbar instead of dropping them down below.

hide menu and dropdown links on all screens at or bigger than 'small' with `sm:hidden`

give the links display `sm:block`

want to use flexbox to position these items

`sm:flex` `sm:justify-between` 

make the link container a flex container as well

`sm:block`-> `sm:flex`

`sm:mt-0` to override the margin on the top and `sm:ml-2` for a little spacing

`sm:px-4` `sm:py-3` to override padding in heading contianer

`sm:items-center` to center the height
