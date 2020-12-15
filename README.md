# Sassy-lib

A minimalistic `sass` breakpoint library for your next project.

## Installation

The default `breakpoints` are:

```sass
$breakpoints: (
  xs: 0,
  sm: 640px,
  md: 768px,
  lg: 1024px,
  xl: 1280px,
);
```

> If you need to overwrite the values just define the breakpoint in your `.scss` file and `import` the library after declaring the breakpoint.

```sass
$breakpoints: (
  xs: 0,
  sm: 640px,
  md: 768px,
  lg: 1024px,
  xl: 1280px,
);

@import 'node_modules/sassy-lib/main.scss';
```

## Usage

The library provides a breakpoint `mixin` which accepts 3 `args`:

- breakpoint name, for example: `sm`, `md`, etc. This is same as your `$breakpoints` `map` key.
- direction, for example: `up`, `down`, `only`. Further explanation provided below.
- `$breakpoints` map. The default value is mention on the top of the page. Even if you need to overwrite the default value, consider creating a separate file for your breakpoints as mentioned above.

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
