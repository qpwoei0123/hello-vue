<script setup>
import { useMouse } from '../hooks/mouse.js';

const { x, y } = useMouse();
setInterval(() => {
  y.value++;
}, 1 * 1000);
</script>

<template>
  <button class="corner">{{ x }}-{{ y }}</button>
</template>

<style scoped>
.corner {
  position: fixed;
  z-index: 1;
  top: 10px;
  left: 10px;
  background: none;
  color: hsla(160, 100%, 37%, 1);
  font-weight: bold;
  outline: none;
  padding: 20px;
  font-size: 2rem;
  min-width: 200px;
}
</style>
