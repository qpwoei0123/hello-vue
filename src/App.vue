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
  inputValue.value = '';
};
</script>

<template>
  <header>
    <img
      alt="Vue logo"
      class="logo heartBeat"
      src="./assets/logo.svg"
      width="125"
      height="125"
    />
  </header>

  <main>
    <input
      v-model="inputValue"
      @keyup.enter="handleClick"
      placeholder="새로운 할 일"
    />
    <button @click="handleClick">클릭</button>
    <button @click="handleDeleteLocalStorage">로컬 데이터 삭제</button>
    <ul>
      <div class="todoWrapper" v-for="(todo, index) of todos" :key="index">
        <li>{{ todo }}</li>
        <button @click="todos.splice(index, 1)">X</button>
      </div>
    </ul>
  </main>
</template>

<style scoped>
ul {
  display: flex;
  flex-direction: column;
  padding: 0;
  width: 200px;
}

.todoWrapper {
  color: hsla(160, 100%, 37%, 1);
  border: 1px dashed hsla(160, 100%, 37%, 0.5);
  margin: 10px 0px;
  padding: 10px;
  display: flex;
  align-items: center;
  li {
    list-style: none;
    flex-grow: 1;
  }
  button {
  }
}

input {
  background: none;
  color: hsla(160, 100%, 37%, 0.5);
  padding: 5px;
  outline: none;
}

button {
  background: none;
  color: hsla(160, 100%, 37%, 0.5);
  font-weight: bold;
  outline: none;
}

.logo {
  position: fixed;
  z-index: -1;
  opacity: 0.1;
  translate: 50% -50%;
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
