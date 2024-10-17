<script setup>
import Todo from './components/Todo.vue';
import Logo from './components/Logo.vue';
import PointerXY from './components/PointerXY.vue';

import GiveMeText from './slot/GiveMeText.vue';
</script>

<template>
  <Logo />
  <PointerXY />
  <Todo />
  <GiveMeText>슬롯 테스트 원투원투</GiveMeText>
</template>
