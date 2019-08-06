# More Advanced CSS

---

### Cursor

```css
/* little hand 👆 */
button {
	cursor: pointer;
}
```

There a quite a few different ones [https://developer.mozilla.org/en-US/docs/Web/CSS/cursor](https://developer.mozilla.org/en-US/docs/Web/CSS/cursor)

You can even use a custom image instead of a pointer.

---

### List style

Shorthand 🤗

```css
ul {
	list-style: none;
}
```

For
- `list-style-type`
- `list-style-position`
- `list-style-image`

Easier to use a background image on list items for bullets

---

## Some Cool CSS

---

### Transforms

```css
transform: translate(10px,10px);
transform: translateX(10px);
transform: scale(x,y);
transform: rotate(30deg) skewX(25deg);
```

---

## Transitions & Animations

---

### Transitions

```css
a {
	color: white;
	transition: color 0.2s ease;
}
a:hover {
	color: grey;
}
```

Further reading CSS Tricks: [https://css-tricks.com/almanac/properties/t/transition/](https://css-tricks.com/almanac/properties/t/transition/)

---

### Animations

Declare your animation (can be done anywhere in a CSS file)

```css
@keyframes move {
	0% {
		transform: translate(0px, 0px);
	}
	100% {
		transform: translate(50px, 50px);
	}
}
```

Use anywhere

```css
button {
	animation: move 1s ease-in-out infinite;
}
```

---

### Blend modes

Background images

```css
section {
	background-color: purple;
	background-image: url(image.jpg);
	background-blend-mode: multiply;
}
```

Elements

```css
h1 {
	mix-blend-mode: screen;
}
```

Further reading CSS Tricks: [https://css-tricks.com/basics-css-blend-modes/](https://css-tricks.com/basics-css-blend-modes/)

---

### Filters

For media (images & video)

```css
/* can be blur, brightness, contrast, drop-shadow, grayscale, hue-rotate, invert, opacity, saturate, sepia */

image {
	filter: blur(1px) hue-rotate(90deg);
}
```

---

### CSS Shapes

![CSS shape example](day08/02coolCSS/cssShape.png)

---

I want to mention them but not well supported yet.

[https://www.html5rocks.com/en/tutorials/shapes/getting-started/](https://www.html5rocks.com/en/tutorials/shapes/getting-started/)

[https://www.sarasoueidan.com/blog/css-shapes/](https://www.sarasoueidan.com/blog/css-shapes/)


---

### Custom properties

(Sort of) variables in CSS - the spec is just about to expand...

```css
:root {
	--brandCol: red;
}

p {
	color: var(--brandCol);
}
```

More to be said [https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_variables](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_variables)

---

### Maths

```css
body {
	padding: 20px;
}
section {
	width: calc(100vw - 40px);
}
```

---

## Cool CSS Further Reading

---

### Cursor

There a quite a few different ones [https://developer.mozilla.org/en-US/docs/Web/CSS/cursor](https://developer.mozilla.org/en-US/docs/Web/CSS/cursor)

---

### List style

[https://developer.mozilla.org/en-US/docs/Web/CSS/list-style](https://developer.mozilla.org/en-US/docs/Web/CSS/list-style)

---

### Transforms

Further reading:
David DeSandro's transforms examples: [http://desandro.github.io/3dtransforms/](http://desandro.github.io/3dtransforms/)

CSS Transforms on CSS Tricks: [https://css-tricks.com/almanac/properties/t/transform/](https://css-tricks.com/almanac/properties/t/transform/)

---

### Transitions

Further reading CSS Tricks: [https://css-tricks.com/almanac/properties/t/transition/](https://css-tricks.com/almanac/properties/t/transition/)

---

### Animations

CSS Animations for beginners [https://robots.thoughtbot.com/css-animation-for-beginners](https://robots.thoughtbot.com/css-animation-for-beginners)

---

### Blend Modes

Further reading CSS Tricks: [https://css-tricks.com/basics-css-blend-modes/](https://css-tricks.com/basics-css-blend-modes/)

---

### Filters

Cool playground (just omit the -webkit- prefix) [http://html5-demos.appspot.com/static/css/filters/index.html](http://html5-demos.appspot.com/static/css/filters/index.html)

---

### CSS Shapes

[https://www.html5rocks.com/en/tutorials/shapes/getting-started/](https://www.html5rocks.com/en/tutorials/shapes/getting-started/)

[https://www.sarasoueidan.com/blog/css-shapes/](https://www.sarasoueidan.com/blog/css-shapes/)

---

### Custom Properties

More to be said [https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_variables](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_variables)

---

### Codepen

[https://codepen.io/Rumyra/pen/rGoabq?editors=0100](https://codepen.io/Rumyra/pen/rGoabq?editors=0100)

---

### Ruth John's **impressive** use of CSS

[https://mdn.github.io/webaudio-examples/spacialization/](https://mdn.github.io/webaudio-examples/spacialization/)

---

### YouTube video about cool CSS
[https://www.youtube.com/watch?v=IRI1H5tyEAo](https://www.youtube.com/watch?v=IRI1H5tyEAo)
