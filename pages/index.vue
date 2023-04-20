<template>
  <div class="relative">
    <mainGrid />
    <h1 class="text-6xl font-bold text-white absolute top-0 left-0 w-full h-full flex items-center justify-center z-10">Hello Test</h1>
    <div class="fixed bottom-0 right-0 bg-gray-900 text-white p-2">
      Mouse coordinates: {{ mouseX }}, {{ mouseY }}
    </div>
  </div>
</template>

<script>
import { useMouse } from '@vueuse/core';

export default {
  setup() {
    const { x: mouseX, y: mouseY } = useMouse();

    const updateMargins = () => {
      const range = 100;
      const maxMargin = 20;
      const minMargin = -20;

      const percentage = (mouseY / range) * 100;
      const margin = Math.round((percentage / 100) * (maxMargin - minMargin)) + minMargin;

      document.documentElement.style.setProperty('--even-margin', `calc(var(--row-height) * ${margin / 100})`);
      document.documentElement.style.setProperty('--odd-margin', `calc(var(--row-height) * ${margin / -100})`);
    };

    return {
      mouseX,
      mouseY,
      updateMargins,
    };
  },
  mounted() {
    window.addEventListener('mousemove', this.updateMargins);
  },
  unmounted() {
    window.removeEventListener('mousemove', this.updateMargins);
  },
};
</script>

<style scoped>
/* Set the position of the mainGrid component to fixed */
mainGrid {
  position: fixed;
}

/* apply a margin based on mouse coordinates to every even/odd row */
.grid > div:nth-child(even) {
  margin-top: var(--even-margin) !important;
}

.grid > div:nth-child(odd) {
  margin-top: var(--odd-margin) !important;
}

/* apply custom properties to set the margins */
.grid {
  --row-height: 50vh;
  --even-margin: calc(var(--row-height) * 0.5);
  --odd-margin: calc(var(--row-height) * -0.5);
}

@media (max-width: 640px) {
  .grid {
    --row-height: 30vh;
    --even-margin: calc(var(--row-height) * 0.25);
    --odd-margin: calc(var(--row-height) * -0.25);
  }
}
</style>
