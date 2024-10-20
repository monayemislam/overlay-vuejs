<template>
  <transition name="fade">
    <div v-if="opened" class="overlay" @click="onBackdropClick">
      <div class="popup" :class="[animateClass, sizeClass]" @click.stop>
        <header v-if="header" class="popup-header">
          <h2>{{ header }}</h2>
          <button v-if="closeable" @click="close" class="close-button" aria-label="Close">
            &times;
          </button>
        </header>
        <div class="popup-content">
          <slot></slot>
        </div>
        <footer v-if="$slots.footer" class="popup-footer">
          <slot name="footer"></slot>
        </footer>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: 'Overlay',
  props: {
    opened: { type: Boolean, required: true },
    visible: { type: Boolean, default: false },
    animate: { type: String, default: false },
    backdrop: { type: Boolean, default: true },
    closeOnEscape: { type: Boolean, default: true },
    closeByBackdropClick: { type: Boolean, default: true },
    closeable: { type: Boolean, default: true },
    header: { type: String, default: null },
    size: { type: String, default: 'medium', validator: value => ['small', 'medium', 'large'].includes(value) }
  },
  watch: {
    opened(newVal) {
      if (newVal) this.$emit('opened');
    }
  },
  mounted() {
    if (this.closeOnEscape) {
      document.addEventListener('keydown', this.onEscape);
    }
  },
  beforeDestroy() {
    document.removeEventListener('keydown', this.onEscape);
  },
  methods: {
    onEscape(e) {
      if (e.key === 'Escape' && this.opened) this.close();
    },
    onBackdropClick() {
      if (this.closeByBackdropClick) this.close();
    },
    close() {
      this.$emit('closed');
    }
  },
  computed: {
    animateClass() {
      return this.animate ? `animate-${this.animate}` : '';
    },
    sizeClass() {
      return `popup-${this.size}`;
    }
  }
};
</script>

<style scoped>
.overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.6);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
}

.popup {
  background: white;
  color: black;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1), 0 1px 3px rgba(0, 0, 0, 0.08);
  max-width: 90%;
  max-height: 90%;
  display: flex;
  flex-direction: column;
}

.popup-small { width: 300px; }
.popup-medium { width: 500px; }
.popup-large { width: 800px; }

.popup-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 8px 12px;
  border-bottom: 1px solid #e0e0e0;
}

.popup-header h2 {
  margin: 0;
  font-size: 1.25rem;
  color: #333;
}

.close-button {
  background: none;
  border: none;
  font-size: 1.5rem;
  cursor: pointer;
  color: #666;
  transition: color 0.2s;
}

.close-button:hover {
  color: #497a86;
}

.popup-content {
  padding: 24px;
  overflow-y: auto;
}

.popup-footer {
  padding: 16px 24px;
  border-top: 1px solid #e0e0e0;
}

.animate-bounce { animation: bounce 0.5s; }
.animate-fade { animation: fade 0.3s; }

@keyframes bounce {
  0% { transform: scale(0.9); opacity: 0; }
  70% { transform: scale(1.05); }
  100% { transform: scale(1); opacity: 1; }
}

@keyframes fade {
  from { opacity: 0; }
  to { opacity: 1; }
}

.fade-enter-active, .fade-leave-active {
  transition: opacity 0.3s;
}

.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>
