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

To use the `<Overlay>` component in your `App.vue` file, you can follow this example:

```vue
<template>
  <div id="app">
    <h1>Overlay Component Test</h1>
    
    <button @click="openBasicOverlay">Open Basic Overlay</button>
    <button @click="openLargeOverlay">Open Large Overlay</button>
    <button @click="openAnimatedOverlay">Open Animated Overlay</button>
    
    <Overlay 
      :opened="basicOverlayOpened" 
      :visible="basicOverlayVisible" 
      header="Basic Overlay"
      @closed="closeBasicOverlay"
    >
      <p>This is a basic overlay with default settings.</p>
    </Overlay>
    
    <Overlay 
      :opened="largeOverlayOpened" 
      :visible="largeOverlayVisible" 
      header="Large Overlay"
      size="large"
      @closed="closeLargeOverlay"
    >
      <p>This is a large overlay with custom content.</p>
      <p>It demonstrates the use of the size prop.</p>
    </Overlay>
    
    <Overlay 
      :opened="animatedOverlayOpened" 
      :visible="animatedOverlayVisible" 
      header="Animated Overlay"
      animate="bounce"
      @closed="closeAnimatedOverlay"
    >
      <p>This overlay uses the bounce animation.</p>
      <template #footer>
        <button @click="closeAnimatedOverlay">Close</button>
      </template>
    </Overlay>
  </div>
</template>

<script>
import { Overlay } from 'overlay-vuejs';

export default {
  name: 'App',
  components: {
    Overlay
  },
  data() {
    return {
      basicOverlayOpened: false,
      basicOverlayVisible: false,
      largeOverlayOpened: false,
      largeOverlayVisible: false,
      animatedOverlayOpened: false,
      animatedOverlayVisible: false
    };
  },
  methods: {
    openBasicOverlay() {
      this.basicOverlayOpened = this.basicOverlayVisible = true;
    },
    closeBasicOverlay() {
      this.basicOverlayOpened = this.basicOverlayVisible = false;
    },
    openLargeOverlay() {
      this.largeOverlayOpened = this.largeOverlayVisible = true;
    },
    closeLargeOverlay() {
      this.largeOverlayOpened = this.largeOverlayVisible = false;
    },
    openAnimatedOverlay() {
      this.animatedOverlayOpened = this.animatedOverlayVisible = true;
    },
    closeAnimatedOverlay() {
      this.animatedOverlayOpened = this.animatedOverlayVisible = false;
    }
  }
};
</script>

<style>
#app {
  font-family: Arial, sans-serif;
  text-align: center;
  margin-top: 60px;
}

button {
  margin: 10px;
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
}
</style>
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
