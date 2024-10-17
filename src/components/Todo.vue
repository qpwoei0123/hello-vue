<script setup>
import { ref, watch, onMounted } from 'vue';

let inputValue = ref('');
const todos = ref(['뷰 이해하기']);

// 입력값 저장
const handleClick = () => {
  const trimmedValue = inputValue.value.trim();
  if (trimmedValue) {
    todos.value.push(trimmedValue);
    inputValue.value = '';
  }
};

// 로컬 스토리지에 저장
const saveTodosOnLocalStorage = () =>
  localStorage.setItem('todos', JSON.stringify(todos.value));
watch(todos, saveTodosOnLocalStorage, { deep: true });

// 마운트 시 로컬 스토리지에서 데이터 가쟈오기
const loadTodosFromLocalStorage = () =>
  JSON.parse(localStorage.getItem('todos')).length === 0
    ? console.log('로컬에 데이터 없음')
    : (todos.value = JSON.parse(localStorage.getItem('todos')));
onMounted(loadTodosFromLocalStorage);

// 로컬 스토리지 삭제
const handleDeleteLocalStorage = () => {
  localStorage.removeItem('todos');
  todos.value = [];
  inputValue.value = '';
};
</script>

<template>
  <section @keyup.enter="handleClick">
    <input v-model="inputValue" placeholder="새로운 할 일" />
    <button @click="handleClick">Enter</button>
    <button @click="handleDeleteLocalStorage">로컬 데이터 삭제</button>
    <button @click="() => (inputValue += '!')">input += !</button>
    <ul>
      <div class="todoWrapper" v-for="(todo, index) of todos" :key="index">
        <li>
          {{ todo }}
        </li>
        <button @click="todos.splice(index, 1)">X</button>
      </div>
    </ul>
  </section>
</template>

<style scoped>
section {
  top: 10px;
  right: 10px;
  position: absolute;
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
</style>
