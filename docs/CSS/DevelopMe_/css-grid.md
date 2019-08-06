# CSS Grid

## CSS Grid vs CSS Flexbox

Flexbox is intended to layout items on 1 axis. 

Grid is intended for 2D layout, both x and y axis. 

### Grids are not a new idea

The (BBC News)[https://bbc.co.uk/news] website is a great example of excellent grid layout. 

### Bootstrap is an example of a grid based CSS framework 

## Benefits

- Not tied into a system 
- No addons required
- No added classes

### Used for laying out a page

- Popping content in the right place - you can use grid on different parts of the page, and flexbox on other parts of the page. 
- It's pretty new - about 2 years old, but everyone should be using Grid now
- It's DOM (Document Object Model), or HTML dependent - Grid only affects the direct child of the HTML element.


## How to use

```css
.page_home {
    display: grid;
}
```

### Specify the amount of cols & rows

```scss
.page__home {
    display: grid;
    grid-template-rows: 20vh 1fr 1fr 16vh;
    grid-template-columns: repeat(3, 1fr); // shorthand way of writing ```1fr 1fr 1fr```
}
```

This is an explicit grid:

We specify the grid areas.

If we didn't set cols & rows the grid would do it for us and be an _implicit_ grid

### A couple of notes

The `fr` unit is only available for grid

(We are considering it as a global unit \o/)

There's also a minmax() function

And you can put a gap between these areas

```css
grid-template-rows: 20vh 1fr 1fr 16vh;
grid-template-columns: repeat(3, 1fr);
grid-gap: 1rem;
```

### How do we get things in places

We can name the areas we have created

```scss
.page__home {
    display: grid;
    grid-template-rows: 20vh 1fr 1fr 16vh;
    grid-template-columns: repeat(3, 1fr);
    grid-template-areas:
        "header header header"
        "main main aside"
        "main main ." // you can create a blank area (without a name) by using a . instead of an area name
        ". footer ."
    ;
}
```



### Then we can reference those names when we're styling the child sections

```css
.header-main {
    grid-area: header;
}
```

#### Using grid row & col numbers instead of names

Grids have number lines automatically. It's not necessary to name the grid areas. You can define them using grid numbers. 


```css
.header-main {
    grid-row: 1 / 2;
    grid-column: 1 / 4;
}
```

**Shorthand**

```css
.header-main {
    grid-area: 1 / 1 / 2 / 4;
}
```

Note there is more, you can name grid lines, there's a `span` keyword, and `minmax()` function

## CSS Grid Codepen Exercise

(https://codepen.io/Rumyra/pen/oymjxE)[https://codepen.io/Rumyra/pen/oymjxE]

### Setting size on implicit grid

Explicit is what you know, implicit is what you don't know

```css
.page__home {
    grid-auto-rows: 140px;
    grid-auto-flow: column;
}
```

### Aligning children

```scss
// on parent 
.page__home {
    justify-items: start;
    align-items: stretch;
}

// on individual child 
.header-main {
    justify-self: end;
    align-self: center;
}
```

### Support

Polyfills: (you don't need one)

[https://www.smashingmagazine.com/2017/11/css-grid-supporting-browsers-without-grid/](https://www.smashingmagazine.com/2017/11/css-grid-supporting-browsers-without-grid/)

[https://caniuse.com/#search=grid](https://caniuse.com/#search=grid)

## Resources

- [https://mozilladevelopers.github.io/playground/css-grid/02-first-grid/](https://mozilladevelopers.github.io/playground/css-grid/02-first-grid/)
- [https://learncssgrid.com/](https://learncssgrid.com/)



