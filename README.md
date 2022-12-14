# nuxt3-svg-sprite-builder

Nitro plugin to inject SVG sprite from SVG files into your HTML

> ⚠️ This is experimental and currently only provided for testing and feedback. Use at your own risk!

From

```
📁 svg
├  📁 icons
│  └  📄 user.svg
├  📁 illustrations
│  └  📄 error.svg
└  📄 logo.svg
```

To
```html
<body>
  <svg xmlns="http://www.w3.org/2000/svg" style="position: absolute; width: 0; height: 0;" aria-hidden="true">
    <symbol id="icons/user" ...>...</symbol>
    <symbol id="illustrations/error" ...>...</symbol>
    <symbol id="logo" ...>...</symbol>
  </svg>
  ...
</body>
```

## Table of contents
- [Why it was made](#why-it-was-made)
- [Installation](#installation)
- [Usage](#usage)
  - [Rendering an SVG](#rendering-an-svg)
  - [Creating a dynamic SVG component](#creating-a-dynamic-svg-component)
- [Credits](#credits)
- [License](#license)

## Why it was made

- Popular modules like [JetBrains/svg-sprite-loader](https://github.com/JetBrains/svg-sprite-loader) do not support Vite as they are made for Webpack only.
- Vite modules based on Vite's `transformIndexHtml` hook do not work as it is not supported in Nuxt 3 ([Issue #1711](https://github.com/nuxt/framework/pull/1711))
- Most of modules bake in unwanted global components and require you to use them in order to use their module.

## Installation

Install module via npm or yarn:
```bash
# npm
npm install nuxt3-svg-sprite-builder

# yarn
yarn add nuxt3-svg-sprite-builder
```

Create `svgSpriteBuilder.js` into `/server/plugins` and add the following code:

```js
import { svgSpriteBuilder } from 'nuxt3-svg-sprite-builder';

export default svgSpriteBuilder('./path/to/svg/folder');
```

Edit `./path/to/svg/folder` to match your SVG folder, default is `./assets/svg` if omitted.

## Usage

### Rendering an SVG

Render `/svgDirectory/logo.svg`
```vue
<svg>
  <use href="#logo" />
</svg>
```
Render `/svgDirectory/icons/user.svg`
```vue
<svg>
  <use href="#icons/user" />
</svg>
```

### Creating a dynamic SVG component

`/components/SvgComponent.vue`
```vue
<template>
  <svg>
    <use :href="`#{href}`" />
  </svg>
</template>

<script setup>
defineProps({
  href: {
    type: String,
    required: true,
  },
});
</script>
```
Dynamic SVG component usage
```vue
<SvgComponent :href="dynamicValue" />
```

## Credits

- [@Lstmxx](https://github.com/Lstmxx) for creating [vite-svg-plugin](https://github.com/Lstmxx/vite-svg-plugin) on which this module is based.

## License

[MIT License](https://github.com/njsen/nuxt3-svg-sprite-builder/blob/main/LICENSE.md)
