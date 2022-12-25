## 4. [Build and Style a Dropdown in Tailwind](https://egghead.io/playlists/build-and-style-a-dropdown-in-tailwind-7f34fead)

 **Playlist** **Description**

A menu dropdown is a common component that you will build and style in any application. In this collection we'll start from scratch, build and style a static dropdown menu and then add functionality to the component so you can open and close the dropdown. There are some keyboard accessibility topics we'll cover when adding interactivity to the dropdown. We'll use Vue in this example but these concepts will apply to any framework. 

After the drop down is fully functional and styled properly, we'll see how sometimes you need to rethink the design of a component when considering the mobile view. For this case, the dropdown is removed entirely and the links shown inline underneath the navbar content.

### 4.1 Styling the Basic Dropdown Elements

→ Style the Basic Dropdown Elements with Tailwind

**Description**

A menu dropdown is a common component that you will build and style in any application. In this lesson, we'll start by building a dropdown defining the HTML structure with a profile picture image as a button and links that one would likely find in a dropdown.

After the structure is defined, we'll style the the image to be a round button with a nice border outline. The links will be displayed below stacked atop eachother with a fixed width and nice hover effect.

---

**Notes**

simple drop down in a navbar like a menu or account drop down.

create the html structure 

style dropdown button

display `block`

adjust size `h-8` `w-8`

have a rect image with a square space so `h-full` `w-full` `object-cover`

`rounded-full` to make the button rounded and `overflow-hidden` to hide the square corners of the image

fix the focus

add border with border-gray-600

focuse:border-white

now focus on the content

white background with `bg-white`

add rounded edges with `rounded-lg`

each item 

is display `block`

`px-4` and `py-4` so that when hovered, can highlight to the edge 

`text-gray-800` `hover:bg-indigo-500` `hover:text-white`

`w-48` to make the width a fixed size instead of readjusting to the full width

`shadow-xl` to give it an elevated effect.

### 4.2 Positioning the Dropdown Area

→ Use Absolute Positioning to Position a Tailwind Styled Dropdown Area in a Navbar

**Description**

In [Build a Responsive Navbar with Tailwind]([https://egghead.io/playlists/build-a-responsive-navbar-with-tailwind-4d328a35](https://egghead.io/playlists/build-a-responsive-navbar-with-tailwind-4d328a35)), we built a Navbar that we'll use to start out this lesson and drop our account info button and dropdown.

We'll see that adding the dropdown to the navbar won't just work - the positioning is a little off and the navbar is expanding to contain the dropdown as well. We'll see how `absolute` positioning solves this issue for us when we anchor it's position to the button it's associated with (by making that button a "positioned" element with `relative`)

---

**Notes**

In [Build a Responsive Navbar with Tailwind]([https://egghead.io/playlists/build-a-responsive-navbar-with-tailwind-4d328a35](https://egghead.io/playlists/build-a-responsive-navbar-with-tailwind-4d328a35)), we built a Navbar that we'll use to start out this lesson and drop our account info button and dropdown

import AccountDropdown in vue and add it to the nav

Even though the dropdown looks like it's floating, it's actually not. The navbar has to grow vertically to accommodate the size of the dropdown itself

need to take the dropdown out of the normal flow

`absolute` positioning will be needed

taken out of the flow, but is still rendered in the place the browser thinks it should be

`right-0` will have the very right of the drop down position itself at the edge of the viewport

is placed according to the nearest positioned element which right now is only the body document. so `right-0` is 0 px right of the body, not the nav or drop down

add `relative` to the div containing the dropdown. This will act mostly the same as it did before but now it is a positioned element so now the dropdown will attatch itself to the dropdown container div

we are only positioning it according to the x axis and letting the browser figure out where to place it on the y axis. This makes it so that if we increase the size of the button, the dropdown will adjust where it renders automatically because of the browser behavior

### 4.3 Making the Dropdown Interactive

→ Make a Tailwind Styled Dropdown Interactive

**Description**

The dropdown looks great but right now it's completely static - it's stuck in an open position. For it to be complete, we'll want to be able to toggle it open and closed.

To do that, we'll add some Vue specific that will track an `isOpen` variable in the component state that we'll use to open and close the dropdown. After that we'll hook up a click handler to the button to do just that, close and open the dropdown. 

Once that is done, we'll handle the case where a user clicks outside of the dropdown to close it as well as add a keyboard accessible variant to close the dropdown

---

**Notes**

Dropdown looks great but right now it's completely static - it's stuck in an open position.

We'll start with vue

add some state `isOpen` and default that to `false`

`v-if="isOpen"` on the dropdown div will hide/show the dropdown when it's false/true

add click handler to button `@click="isOpen = !isOpen"` 

Now it toggles if you click the dropdown button

but we also want it to hide if we click outside of the dropdown.

need a click handler on an element that will handle that

add button `@click=isOpen=false`

we'll make the button position `absolute` and stretch it from top to bottom, ,left to right `top-0` `right-0` `bottom-0` `left-0`

add `h-full` `w-full`

but this button is only covering the positioned button - not the body

we'll add position `fixed` which will make it relative to the body 

add `v-if="isOpen"` so the button only show when the dropdown is open

add `bg-black` `opacity-50` to make it visual

`cursor-default` so the cursor style isn't affected by this page level button

Add a z index to the button so that it will show on top of the global page button

the z index doesn't apply to the button because it isn't a positioned element

add `relative` so it can be affected by `z-10` (the first z index step in tailwind

add `tabindex="-1"` so that the page button isn't accessible from the keyboard which would be unexpected behavior

replace `top-0` `right-0` `bottom-0` `left-0` with `inset-0` which will be the same behavior

add keyboard accessible way to escape the dropdown.

this is totally JS driven 

create a function called `handleEscape` which will look for the `esc` press and set `isOpen` to false

add the eventListener to the dom 

### 4.4 Adapting the Dropdown for Mobile

→ Redesign a Dropdown List for Mobile with Tailwind

**Description**

The dropdown looks great on desktop sized screens but is kind of a mess on mobile. To fix that we'll need to rethink the design of the drop down for the mobile space.

In this lesson, we'll create a duplicate acount link list and remove the dropdown functionality in preference of showing the account links inline with the other navbar links on mobile with clear separation between the two lists.

---

**Notes**

instead of having a dropdown in a dropdown, we should look at how to display these links in a separate list than the links in the navbar.

recommends duplicating this content and toggling between the two whenever you want instead of adding responsive breakpoints all over the place

copy/pastes the dropdown content

removes all the classes from that dup content

Add a class `hidden` `sm:block` `sm:ml-6` so that the original dropdown only shows on small screens and above

add a top border `border-t` and `border-gray-800`

create container div for links to move top level padding into that container so the padding doesn't affect the border

add `px-4` to match the links and dropdown above and `py-5` to match the padding of the bottom link to the image

add margin to links to space things correctly

add `hover:text-white` to links

add user name 

`font-semibold` and `text-white` `ml-3`
