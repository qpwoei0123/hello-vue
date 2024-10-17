<script setup>
import { reactive, ref, watchEffect } from 'vue';

// 랜덤 숫자 생성 함수
const randomNumber = () => Math.floor(Math.random() * 100);

// 반응형 객체와 렌더링 카운터
let obj = reactive({});
let renderCount = ref(0); // 렌더링 횟수 추적용

// 객체 채우기 함수
const fillInObj = () => {
  for (let i = 0; i < 10; i++) {
    obj[i] = randomNumber();
  }
};

// 렌더링이 발생할 때마다 카운트 증가
watchEffect(() => {
  renderCount.value++; // 렌더링이 트리거될 때마다 증가
  console.log(`렌더링 횟수: ${renderCount.value}`);
});

// 초기 값 채우기
fillInObj();

// 짝수 여부 확인 함수
const isEven = (value) => value % 2 === 0;
</script>

<template>
  <ul>
    <p>렌더링 횟수: {{ renderCount }}</p>
    <button @click="fillInObj">리롤!</button>
    <li v-for="(value, key) in obj" :key="`${key}-${value}`" v-memo="[value]">
      {{ value }}
      <span v-if="isEven(value)">Even 하네</span>
    </li>
  </ul>
</template>

<style scoped>
ul {
  position: fixed;
  bottom: 0px;
  left: 0px;
}
</style>
