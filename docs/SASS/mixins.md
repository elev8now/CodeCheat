# Mixins

## Media Queries

```scss
$medium: 768px;
$wide: 1024px;

@mixin small {
    @media (max-width: #{$medium - 1px}) {
        @content;
    }
}

@mixin medium {
    @media (min-width: $medium) and (max-width: #{$wide - 1px}) {
        @content;
    }
}

@mixin small-medium {
    @media (max-width: #{$wide - 1px}) {
        @content;
    }
}

@mixin wide {
    @media (min-width: $wide) {
        @content;
    }
}
```
