# Bulma and Prismjs

This is a workaround solution for using both [bulma](https://github.com/jgthms/bulma) and [prism](https://github.com/PrismJS/prism) stylesheets.

There are collisions in global selectors between the two libraries, see https://github.com/jgthms/bulma/issues/1708 and https://github.com/PrismJS/prism/issues/1324

## Variant A: Configuring prismjs

You can simply change the prism classes for the two problematic cases:

```javascript
import Prism from "prismjs";
import "prismjs/plugins/custom-class/prism-custom-class";
Prism.plugins.customClass.map({ number: "prism-number", tag: "prism-tag" });
```
This is the simpler, recommended workaround.

## Variant B: Overriding Bulma in sass/scss

This is a patch over the sass version of bulma. It's only available when you use the npm package.

Use the bulma folder of this repo.

It changes two selectors: 
- `.number` becomes `.number:not(.token)`
- `tag:not(body)` becomes `tag:not(body):not(.token)`

### Usage

Copy this folder to your project and import bulma from there.

Instead of this:
```scss
@import "~bulma/bulma.sass";
```

You do something like this:
```scss
@import "./bulma/bulma.sass";
```
