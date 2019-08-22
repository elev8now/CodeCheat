# SCSS

## Mixins

Using **mixins** for vendor prefixes

```scss 
// At this point, the mixin function isn't doing anything. You have to call it when writing our SCSS, and pass a value to it.
@mixin border-radius($radius) {
  -webkit-border-radius: $radius;
     -moz-border-radius: $radius;
      -ms-border-radius: $radius;
          border-radius: $radius;
}

// We can now pass a value of 10px in place of the $radius variable.
.box {
    @include border-radius(10px);
}
```

Using **mixins** for media queries

```scss
$medium: 768px;
$wide: 1024px;

@mixin small {
    @media (max-width: #{$tablet-width - 1px}) {
        @content;
    }
}

@mixin medium {
    @media (min-width: #{$tablet-width}) and (max-width: #{$desktop-width - 1px}) {
        @content;
    }
}

@mixin small-medium {
    @media (min-width: 1px) and (max-width: #{$desktop-width - 1px}) {
        @content;
    }
}

@mixin wide {
    @media (min-width: #{$desktop-width}) {
        @content;
    }
}
```

When we come to use our mixins, we use `@include`

```scss
.gallery-section-1 {
	box-sizing: border-box;
	margin: 3rem 0.5rem 0 4rem;
	padding: 1rem;
	@include medium {
		margin: 3rem 0.5rem 0 2rem;
		padding: 0.3rem;
	}
	@include small {
		margin: auto 0;
		padding: 0 1rem 1rem;
	}
}

```

## Extends

## Variables

## Functions

```scss
lighten(green, 10%)
```
