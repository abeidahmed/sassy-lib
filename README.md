# Sassy-lib

A minimalistic `Sass` breakpoint library for your next project.

## Installation

`npm i sassy-lib`

After installation, import the library in your `.scss` file.

`@import './node_modules/sassy-lib/main.scss';`

> Absolute `import`s do not work. You need to `import` it manually.

## Library defaults

Default breakpoints:

```sass
$breakpoints: (
  xs: 0,
  sm: 640px,
  md: 768px,
  lg: 1024px,
  xl: 1280px,
);
```

Default `infix` separator (more info at the bottom of the page):

```sass
$breakpoint-infix-separator: "-";
```

> If you need to overwrite the values, just define the breakpoint in your `.scss` file and `import` the library after declaring the breakpoint. Any overwrites must come before importing the library.

```sass
$breakpoints: (
  xs: 0,
  sm: 640px,
  md: 768px,
  lg: 1024px,
  xl: 1280px,
);

@import './node_modules/sassy-lib/main.scss';

// Note: The first value in the $breakpoints map should be 0.
```

## Usage

The library provides a breakpoint `mixin` which accepts 3 `args`:

- breakpoint name, for example: `sm`, `md`, etc. This is same as your `$breakpoints` `map` key.
- direction, for example: `up`, `down`, `only`. Further explanation provided below.
- `$breakpoints` map. The default value is mentioned on top of the page. Even if you need to overwrite the default value, consider creating a separate file for your breakpoints as mentioned above.

The library handles 3 directions, namely:

- `up` (min-width)
- `down` (max-width)
- `only` (min-width and max-width)

To use any of these directions (default is `up`), you need to `include` the breakpoint `mixin`.

```sass
@include breakpoint(sm) {
  // your styles
}
// Same as @media (min-width: 640px) {}

@include breakpoint(sm, down) {
  // your styles
}
// Same as @media (max-width: 639.98px) {}

@include breakpoint(sm, only) {
  // your styles
}
// Same as @media (min-width: 640px and max-width: 767.98px) {}
```

## Creating utility classes

Sassy-lib also provides a powerful `api` called `breakpoint-infix` that you can use to create your utility classes.

```sass
$displays: (
  flex: flex,
  block: block,
);

// $breakpoints is your key-value pair of breakpoint map

@each $breakpoint in map-keys($breakpoints) {
  // provided by the library
  $bp-sort: breakpoint-infix($breakpoint);

  @include breakpoint($breakpoint) {
    @each $prop, $value in $displays {
      .#{$bp-sort}#{$prop} {
        display: $value;
      }
    }
  }
}

// creates
.flex {
  display: flex;
}

@media (min-width: 640px) {
  .sm-flex {
    display: flex;
  }
}

// etc
// Note: Please use $bp-sort before declaring your class name.
```

The default `infix` separator is "-", but you can overwrite by overwriting the `$breakpoint-infix-separator` variable.

## Tip

You can also create [Tailwind CSS](https://tailwindcss.com/) like `classes` by overwriting the `$breakpoint-infix-separator` value to `$breakpoint-infix-separator: "\\:"`, which will generate similar `classes`.
