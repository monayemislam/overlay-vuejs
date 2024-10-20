# Overlay Vue.js

A stylish, animated, and customizable overlay (popup) component for Vue.js.

## Table of Contents

- [Installation](#installation)
- [Usage](#usage)
- [Props](#props)
- [Slots](#slots)
- [Events](#events)
- [License](#license)

## Installation

To install the package, use npm:

```bash
npm install overlay-vuejs
```

## Usage

First, import and register the component in your Vue application:

```javascript
import { createApp } from 'vue';
import App from './App.vue';
import Overlay from 'overlay-vuejs';

const app = createApp(App);
app.use(Overlay);
app.mount('#app');
```

Then, use the `<Overlay>` component in your templates:

```vue
<template>
  <Overlay
    :opened="isOverlayOpen"
    header="My Overlay"
    @closed="handleClose"
  >
    <p>This is the content of the overlay.</p>
  </Overlay>
</template>

<script>
export default {
  data() {
    return {
      isOverlayOpen: false
    };
  },
  methods: {
    handleClose() {
      this.isOverlayOpen = false;
    }
  }
};
</script>
```

## Props

- **opened** (Boolean, required): Controls the visibility of the overlay.
- **visible** (Boolean, default: `false`): Alias for `opened`.
- **animate** (String, default: `false`): Animation type for the overlay. Options: `bounce`, `fade`.
- **backdrop** (Boolean, default: `true`): Whether to show a backdrop.
- **closeOnEscape** (Boolean, default: `true`): Close the overlay when the Escape key is pressed.
- **closeByBackdropClick** (Boolean, default: `true`): Close the overlay when the backdrop is clicked.
- **closeable** (Boolean, default: `true`): Show a close button in the header.
- **header** (String, default: `null`): Text for the overlay header.
- **size** (String, default: `medium`): Size of the overlay. Options: `small`, `medium`, `large`.

## Slots

- **default**: Content of the overlay.
- **footer**: Content for the footer section of the overlay.

## Events

- **opened**: Emitted when the overlay is opened.
- **closed**: Emitted when the overlay is closed.

## License

MIT © [Md Monayem Islam](mailto:contact@monayemislam.me)
