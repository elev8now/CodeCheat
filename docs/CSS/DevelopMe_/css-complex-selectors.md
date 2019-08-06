# CSS Complex Selectors


### More than just simple selectors

```css
element {}
.class {}
#id {}
```


### Child & Sibling

```css
/* direct child */
parentEl > childEl  {}

/* sibling */
a ~ img  {}

/* ajacent sibling */
a + img  {}
```


### Attribute

```css
/* given attr is present */
section[class] {}

/* attribute */
input[type=”submit”]  {}

/* any part of attr */
a[href*=”http”]  {}

/* begins with */
a[href^=”https”]  {}

/* ends with */
a[href$=”pdf”]  {}

/* space separated */
a[class~="btn"] {}

/* hyphen separated */
[class|="page"] {}
```

### Pseudo classes

```scss
a:link
a:visited
a:hover
a:active
a:focus // really helpful for accessibility - see BBC website for good use of focus pseudo class

input:enabled
input:disabled
input:checked
input:indeterminate
```

Learn more about Indeterminate [https://css-tricks.com/indeterminate-checkboxes/](https://css-tricks.com/indeterminate-checkboxes/)


### Targeting children

```scss
el:first-child {} // first element of multiple identical sibling elements
el:last-child {} // last element of multiple identical sibling elements
el:only-child {} // only use if element has no identical siblings

el:first-of-type {} // first element of multiple sibling elements when elements are not the same
el:last-of-type {} // last element of multiple sibling elements when elements are not the same
el:only-of-type {} // only use if element has no siblings

el:nth-child(1) {} // like first child, but can target specific child e.g. el:nth-child(4);
el:nth-last-child(2n) {}

el:nth-of-type(2n) {} // add styling to recurring elements, in this case every second element (2n)
el:nth-last-of-type(3) {}

/* Has id which is linked to via <a> with # */
section:target {}

/* no children */
div:empty {}

/* does not have */
article:not(.about) {}
```


### Pseudo elements

```scss
div::before
// Example
.promo-card::before {
    content: "";
    top: 0;
    left: 0;
    border-top: 10px;
}
section::after

p::first-letter
p::first-line
p::selection
```


## Resources

- Article about Complex Selectors [https://learn.shayhowe.com/advanced-html-css/complex-selectors/](https://learn.shayhowe.com/advanced-html-css/complex-selectors/)
- Codepen with examples of Complex Selectors [https://codepen.io/elev8now/pen/dBrGxQ?editors=0100](https://codepen.io/elev8now/pen/dBrGxQ?editors=0100)
