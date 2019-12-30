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
For simple module:

```scss
// sass/utilities/display.scss
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
css output: css/utilities/display.css

```css
.displayNone {
  display: none;
}

.displayBlock {
  display: block;
}
```
For multiple module:

```scss
// sass/utilities/flex.scss
@use "sass-converter/module";

///////////////////////////////
$name: flex;
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

@function flex() {
  // flex-wrap
  $wrap: (
    NoWrap: (
      flex-wrap: nowrap
    ),
    Wrap: (
      flex-wrap: wrap
    )
  );
  // flex-direction
  $direction: (
    Row: (
      flex-direction: row
    ),
    Col: (
      flex-direction: column
    )
  );
  // align-items
  $align-items: (
    AlignItemsStart: (
      align-items: flex-start
    ),
    AlignItemsEnd: (
      align-items: flex-end
    )
  );
  @return module.collect($wrap, $direction, $align-items);
}

@include module.export(flex(), $config);
```
css output: css/utilities/flex.css

```css
.flexNoWrap {
  flex-wrap: nowrap;
}

.flexWrap {
  flex-wrap: wrap;
}

.flexRow {
  flex-direction: row;
}

.flexCol {
  flex-direction: column;
}

.flexAlignItemsStart {
  align-items: flex-start;
}

.flexAlignItemsEnd {
  align-items: flex-end;
}
```

### Thanks
Thanks to [Jessica Biggs](https://gist.github.com/bigglesrocks/d75091700f8f2be5abfe) for more than two maps in one module