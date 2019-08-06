# CSS - Day 2

## HELPFUL RESOURCES
[https://github.com/develop-me/all-your-links-are-belong-to-us](https://github.com/develop-me/all-your-links-are-belong-to-us)

## Box Model
```css
display: block; /* has vertical flow */
display: inline; /* has horizontal flow, left-to-right */
```

All HTML elements have a default display type.

- `p` element is `display: block;` by default
- `em`, `strong`, `span`, `b`, `i` elements are `display: inline;` by default
- `li` elements are `display: list-item;` by default
- `td` elements are `display: table-cell;` by default

Any CSS styling that comes from the 'user agent stylesheet' in Chrome or Firefox are the browser default styling.

## Box Sizing
Use `box-sizing: border-box;` to include `padding` in width and height of element.

## Height - AVOID
Best practice: DO NOT use the height property. Let the content be the height.

## Images
`Img` elements are `display: inline;` by default. Most often they should be display: block;
Take note of this because you will often have to change it.

## Position

`position: static;` - This is the default value for all html elements which keeps the element in normal flow.

`position: relative;` - This keeps the element in normal flow, and allows you to use the top or bottom, left or right properties to shift the element.

`position: fixed;` - This pulls the element out of normal flow and allows you to position it using co-ordinates (top or bottom, left or right). Remember the parent element must have a `position: relative;` for this to work correctly.

`position: absolute;` - This allows for scroll, position: fixed; does not.

See this codepen for more information and demo: [https://codepen.io/elev8now/pen/EBLaYj](https://codepen.io/elev8now/pen/EBLaYj)

## Floats

If you have an image with a paragraph text underneath, you don't float the paragraph right, you float the image left.

In order to prevent elements below your floated elements from wrapping, there is a simple hack you can use. If you have 3 floated left paragraph elements inside a div, the content underneath the div will wrap itself around the paragraph elements. In order to escape the content around the paragraph elements, you can do the following:

```css
div.float {
	overflow: auto;
}
```

This hack will escape the content around that div and force the content further down the page to display below it.

The NEW way to solve this problem is

```css
div.float {
	display: flow-root;
}
```

Using `display: flow-root` always invokes a new block formatting context for its contents.

See this codepen for how it works: [https://codepen.io/elev8now/pen/vqjNpX](https://codepen.io/elev8now/pen/vqjNpX)

## CSS Sizing Units

### Pixels (px)
An exact measurement - width 1px == 1px

### Percentage (%)
Relative to width of container. Bear in mind padding and margin counts as width, 50% + 50% + 20px will break your layout.

### Em
Font measurment, relative to parent
```css
body {font-size: 16px;} /* default */
p {font-size: 1.2em;} /* 16 x 1.2 */
p a {font-size: 1.2em;} /* 16 x 1.2 x 1.2 */
```

### Rem
Like em but always relative to root
```css
body {font-size: 1rem;}
p {font-size: 1.2rem;}
p a {font-size: 1.2rem;}
```

### Viewport
- 1vw = 1% of viewport width
- 1vh = 1% of viewport height
- 1vmin = 1vw or 1vh, whichever is larger
- 1vmax = 1vw or 1vh, whichever is larger

Example use:
```css
section {height: 100vh;}
```

Other Measurements

`ex` height of 'x'

`ch` width of '0'

`lh` equal to the line-height

`pt` 1/72"

`mm`

`cm`

## Responsive & Adaptive Design

### Responsive
- Responding to the environment
- Making the webpage/app resize to it's device for instance

### Adaptive
- Adapting to the device
- Serving a different set of files for different set of devices or connections
- Designs that work in all environments
	- Screens
	- Inside/Outside e.g. dark mode
	- Noisy/quiet
	- Fibre/2G - load speeds and data consumption considerations

### How to create responsive layout?

- Use relative not absolute CSS units
- CSS Media Queries @media
- JavaScript feature and device detection
- Speedtesting is hard - bear in mind the data speed of audience

## Case Study - The Guardian

The Guardian website is a great example of incredibly fast load speeds, specifically the 'first paint'.

## Media Queries

Used to control styles for different types of media e.g. screen and print

Example:
```css
@media print {
	* {
		background-color: transparent;
	}
}
```

## Breakpoints (Viewport Width)
```css
/* phone */
@media only screen and (max-width: 500px) {
	#left-column {
		display: none;
	}
}
```

```css
/* Extra small devices (phones, less than 768px) */
@media (max-width: 767px) {}
/* Small devices (tablets, 768px and up) */
@media (min-width: 768px) and (max-width: 991px) {}
/* Medium devices (desktops, 992px and up) */
@media (min-width: 992px) and (max-width: 1199px) {}
/* Large devices (large desktops, 1200px and up) */
@media (min-width: 1200px) {}
```

## JavaScript Libraries
There are JavaScript libraries capable of detecting:
- device type
- touchscreen or desktop
- operating system
- browser

You can add a class to the body element with Javascript:

```html
<body class="touchscreen tablet windows8 w1024">
```

You can even detect the device orientation:

```html
<body class="dim-short-600 dim-long-1024 portrait">
<body class="dim-short-600 dim-long-1024 landscape">
```

A good resource for JavaScript feature detection is: [https://modernizr.com/](https://modernizr.com/)

Use CSS where possible. Responsive design is cleaner, faster and easier to maintain using a CSS-only approach and media queries. New devices come out all the time, and with 1000's of devices out there, it's unlikely you will be able to accurately determine all the types.

## Hierarchy and Navigation
- What content is most important?
- What should come first?
- How can we navigate?
- Is some content worth losing for a simplified mobile experience? E.g. video, slidehow.
