# sass-converter
> sass module converter

### Setup
Install it in your project:

```bash
npm install sass sass-converter --save-dev
```

and add a script to your package.json like this:

```json
{
  "scripts": {
    "build": "sass --load-path=node_modules sass:css"
  }
}
```

### How to use
Populate ./sass/utilities/display.scss inside your project:

```scss
@use "sass-converter/module";

$props: (
  // add module name
  prefix: display,
  // add prefix of media query
  mediaprefix: false, // or true
  // No media query for `xs` since this is the default in Bootstrap
  // Add null for xs
  breakpoint: false // sm or (null, sm, md, lg, xl)
);

@function display() {
  @return(
    None: (
      display: none
    ),
    Block: (
      display: block
    )
  );
}

@include module.export(display(), $props);
```
and then just run:
```bash
npm run build
```

css output ./css/utilities/display.css

```css
.displayNone {
  display: none;
}

.displayBlock {
  display: block;
}
```