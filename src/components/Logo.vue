<template>
  <header>
    <img
      alt="Vue logo"
      class="logo heartBeat"
      src="../assets/logo.svg"
      width="500"
      height="500"
    />
  </header>
</template>

<style scoped>
.logo {
  position: fixed;
  z-index: -1;
  opacity: 0.1;
  transition: 0.5s ease-in-out;
  top: 50%;
  left: 50%;
  translate: -50% -50%;
}

.heartBeat {
  animation: heartBeat 60s infinite;
}
@keyframes heartBeat {
  0% {
    transform: scale(1);
    rotate: 0deg;
  }
  50% {
    transform: scale(0.1);
  }
  100% {
    transform: scale(1);
    rotate: 360deg;
  }
}
</style>
