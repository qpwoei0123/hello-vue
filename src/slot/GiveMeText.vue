<script setup>
import { ref } from 'vue';
let isOpen = ref(false);

const modalToggle = () => {
  isOpen.value = !isOpen.value;
};
</script>

<template>
  <button @click="modalToggle">모달</button>
  <div @click.self="modalToggle" class="modalWrapper" v-if="isOpen">
    <div class="modal"><slot></slot></div>
  </div>
</template>

<style scoped>
button {
  background: none;
  padding: 10px;
  color: hsla(160, 100%, 37%, 0.5);
}

.modalWrapper {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal {
  position: fixed;
  width: 500px;
  height: 500px;
  border: 2px solid hsla(160, 100%, 37%, 0.5);
  background-color: hsla(160, 100%, 37%, 0.05);
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 3rem;
}
</style>
