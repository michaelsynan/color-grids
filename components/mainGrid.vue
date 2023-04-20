<template>
  <div class="grid h-screen place-items-center">
    <div class="grid grid-cols-7 gap-5 max-w-6xl h-1/2">
      <div
        v-for="(color, index) in colorGrid"
        :style="{ backgroundColor: color }"
        class="col-span-1 h-full"
        :class="{ 'my-5': index % 2 === 0, '-my-5': index % 2 === 1 }"
      >
        {{ color }}
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue';

const colorGrid = ref([
  '#FF0000',
  '#FF7F00',
  '#FFFF00',
  '#00FF00',
  '#0000FF',
  '#4B0082',
  '#9400D3',
]);
</script>

<style scoped>
/* apply a 20px margin to every even row */
.grid > div:nth-child(even) {
  margin-top: 20px;
}

/* apply a -20px margin to every odd row */
.grid > div:nth-child(odd) {
  margin-top: -20px;
}
</style>
