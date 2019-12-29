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

///////////////////////////////
$name: display;
$version: 1.0;
$author: erkanunluturk;
///////////////////////////////

$config: (
  // add class prefix
  prefix: $name,
  // add prefix of media query
  mediaprefix: false, // or true
  // no media query for `xs` since this is the default in Bootstrap
  // add null for xs
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

@include module.export(display(), $config);
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