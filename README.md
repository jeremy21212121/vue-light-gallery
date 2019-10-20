# vue-light-gallery
VueJS lightweight image gallery for both mobile and desktop browsers. Forked to add srcset and alt attributes to images.

- Standalone: Zero-dependencies.
- Fully responsive.
- Keyboard and Touch support.
- Multiple galleries on one page.
- Lazy & smart image preloading.
- Color customization.

## Demo

[View Demo](https://peremp.github.io/vue-light-gallery/index.html)

## License

MIT License

## install

```bash
// Yarn
yarn add vue-light-gallery

// NPM
npm install vue-light-gallery
```

## Usage
### As a local component
```html
<template>
  <div>
    <LightGallery
      :images="images"
      :index="index"
      :disable-scroll="true"
      @close="index = null"
    />
    <ul>
      <li
        v-for="(image, thumbIndex) in images"
        :key="'thumb' + thumbIndex"
        @click="index = thumbIndex"
      >
        <img
          :src="image.thumb.src"
          :srcset="image.thumb.srcset"
          :alt="image.alt"
        >
      </li>
    </ul>
  </div>
</template>

<script>
  import Vue from 'vue';
  import { LightGallery } from 'vue-light-gallery';

  export default {
    components: {
      LightGallery,
    },
    data() {
      return {
        images: [
          {
            title:'img 1',
            url: 'path/to/image_1.jpg or require() if using nuxt',
            srcset: 'optional',
            alt: 'optional',
            thumb: {
              srcset: '/path/to/thumb 1x, /other/path 2x'
            }
          }
        ],
        index: null,
      };
    },
  };
</script>
```

### As a Global component
```js
// Your APP entry point.
// F.E: index.js
import Vue from 'vue';
import LightGallery from 'vue-light-gallery';

Vue.use(LightGallery);

new Vue(/* ... */);
```
```html
<!-- Component.vue -->
<template>
  ...
    <LightGallery ...props />
  ...
</template>
```
Or if you want to change the component id:
```js
// Your APP entry point.
// F.E: index.js
import Vue from 'vue';
import LightGallery from 'vue-light-gallery';

Vue.use(VueLightGallery, { componentId: 'custom-gallery' });

new Vue(/* ... */);
```

```html
<!-- Component.vue -->
<template>
  ...
    <custom-gallery ...props />
  ...
</template>
```

## Props

| Props               | Type      | Default                                         | Description                   |
| --------------------|:----------| ------------------------------------------------|-------------------------------|
| images              | Array     | []                                              | List of Images                |
| index               | Number    | null                                            | index of the displayed image  |
| disableScroll       | Boolean   | false                                           | Disable the scroll            |
| background          | String    | rgba(0, 0, 0, 0.8)                              | Main container background     |
| interfaceColor      | String    | rgba(255, 255, 255, 0.8)                        | Icons color                   |


### Images definition

Without title: `Array<string>`
```js
  const images = [
    'http://url.com/img1.jpg',
    'http://url.com/img2.jpg',
  ];
```

With title: `Array<Object>`
```js
  const images = [
    { title: 'image 1', url: 'http://url.com/img1.jpg' },
    { title: 'image 2', url: 'http://url.com/img2.jpg' },
  ];
```

The title will only appear if `Object.title` property is defined.

## Events

| Name                | Params              | Description                                     |
| --------------------|:--------------------| ------------------------------------------------|
| close               |                     | Triggered when the lightbox is closed           |
| slide               | { index: Number }   | Triggered when the image change (next or prev)  |


## Usage with Nuxt

Create the plugin `lightGallery.client.js`:

```js
import Vue from 'vue';
import VueLightGallery from 'vue-light-gallery';

Vue.use(VueLightGallery);
```

Add the plugin to `nuxt.config.js`:

```
plugins: [
  '~/plugins/lightGallery.client.js',
],
```

Wrap the component in Nuxt's [`no-ssr` component](https://nuxtjs.org/api/components-no-ssr/).
```html
<no-ssr>
  <LightGallery ... />
</no-ssr>
```

## Allusions
- Inspired by [BaguetteBox](https://github.com/feimosi/baguetteBox.js)
- Spinner extracted from  [epic-spinners](https://github.com/epicmaxco/epic-spinners)
