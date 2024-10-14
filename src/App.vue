<script setup>
import { ref, reactive, watch, onMounted } from 'vue';
import EcosystemIcon from './components/icons/IconEcosystem.vue';
import CommunityIcon from './components/icons/IconCommunity.vue';
import SupportIcon from './components/icons/IconSupport.vue';

let inputValue = ref('');
const todos = ref(['뷰 이해하기']);
const animationState = ref('');

const handleClick = () => {
  const trimmedValue = inputValue.value.trim();
  if (trimmedValue) {
    todos.value.push(trimmedValue);
    inputValue.value = '';
  }
};

const saveTodosOnLocalStorage = () =>
  localStorage.setItem('todos', JSON.stringify(todos.value));

watch(todos, saveTodosOnLocalStorage, { deep: true });

const loadTodosFromLocalStorage = () =>
  JSON.parse(localStorage.getItem('todos')).length === 0
    ? console.log('로컬에 데이터 없음')
    : (todos.value = JSON.parse(localStorage.getItem('todos')));

onMounted(loadTodosFromLocalStorage);

const handleDeleteLocalStorage = () => {
  localStorage.removeItem('todos');
  todos.value = [];
};
</script>

<template>
  <header>
    <img
      alt="Vue logo"
      class="logo"
      src="./assets/logo.svg"
      width="125"
      height="125"
      :class="{ heartBeat: true }"
    />
  </header>

  <main>
    <input
      v-model="inputValue"
      @keyup.enter="handleClick"
      placeholder="새로운 할 일을 입력하세요"
    />
    <button @click="handleClick">클릭</button>
    <button @click="handleDeleteLocalStorage">로컬 데이터 삭제</button>
    <ul>
      <div v-for="(todo, index) of todos" :key="index">
        <li>{{ todo }}</li>
        <button @click="todos.splice(index, 1)">삭제</button>
      </div>
    </ul>
  </main>
</template>

<style scoped>
.spin {
  animation: spin 1s infinite linear;
}
@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

.heartBeat {
  animation: heartBeat 10s infinite;
}
@keyframes heartBeat {
  0% {
    transform: scale(1);
    rotate: 0deg;
  }
  50% {
    transform: scale(0.5);
  }
  100% {
    transform: scale(1);
    rotate: 360deg;
  }
}
</style>
