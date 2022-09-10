<script setup lang="ts">
import CounterComponent from './components/CounterComponent.vue'
</script>

<template>
  <header>
    <img
      alt="Vue logo"
      class="logo"
      src="./assets/logo.svg"
      width="125"
      height="125"
    />
  </header>

  <main>
    <CounterComponent />
  </main>
</template>

<style scoped>
main {
  margin-top: 2rem;
}
</style>
