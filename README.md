# vue-xml-tree
Vue.js 3.0 XML tree viewer component

[![GitHub release](https://img.shields.io/github/release/mikemenaker/vue-xml-tree.svg)]() [![license](https://img.shields.io/github/license/mikemenaker/vue-xml-tree.svg)]()

# vue-xml-tree
Vue.js 3.0 XML tree viewer

## Installation
### With npm:
```bash
npm i v-xml-tree --save
```

### With a CDN:
```html
<!-- In <body>, after Vue import -->
<script type="text/javascript" src="https://unpkg.com/v-xml-tree/dist/vXmlTree.umd.js"></script>
```

## Usage
### With an ES6 bundler (via npm)
In your component file
```js
import vXmlTree from "v-xml-tree";
```

Then register:
```
components: {
    vXmlTree
  },
```

### With a CDN
```html
<script>
    Vue.component("v-xml-tree", vXmlTree);

    new Vue({
        // ...
    })
</script>
```

## Props:
 - data <Object/Array> - Data to format into tree
 - filterKey <String> - String to filter data
 - fullMarkup <Boolean> - If full mark up is need (quotes and commas)

## Slots:
 - hide - What should be used for the hide button
 - expand - What should be used for the expand button
 - more - What should be used for the elipsis when an object/array is hidden

