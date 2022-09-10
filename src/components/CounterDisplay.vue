<script setup lang="ts">
interface Props {
  title: string
  count: number
  isDisabled: boolean
}

defineProps<Props>()
defineEmits(['incrementCount', 'decrementCount'])

const numberFormatter = new Intl.NumberFormat('en-US', {
  style: 'decimal',
  minimumFractionDigits: 1,
})
</script>

<template>
  <div id="main">
    <span id="title">{{ title }}</span>
    <div class="wrapper">
      <button class="decrease" :disabled="isDisabled" @click="$emit('decrementCount')">-</button>

      <span id="count">{{ numberFormatter.format(count) }} h</span>

      <button class="increase" :disabled="isDisabled" @click="$emit('incrementCount')">+</button>
    </div>
  </div>
</template>

<style scoped>
#main {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.wrapper {
  display: flex;
  align-items: center;
}

#title {
  font-size: 1.2em;
}

#count {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 160px;
  font-size: 4em;
}

.wrapper button {
  margin: 0 1rem;
  height: 40px;
  width: 40px;
  font-size: 2em;
  border-radius: 50%;
  border: 3px solid;
  background-color: whitesmoke;
  transition-duration: 0.4s;
}

.wrapper button:hover {
  cursor: pointer;
  opacity: 0.8;
}

.increase {
  border-color: rgb(9, 175, 9) !important;
}

.decrease {
  border-color: rgb(220, 21, 21) !important;
}
</style>
