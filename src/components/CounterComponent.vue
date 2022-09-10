<script setup lang="ts">
import { reactive } from 'vue'

const GOD_NUMBER = 0.5
const GOD_MULTIPLIER = 2

interface State {
  learnCount: number
  playCount: number
}

const state: State = reactive({
  learnCount: 0,
  playCount: 0,
})

function incrementLearnCount() {
  state.learnCount = state.learnCount + GOD_NUMBER
  incrementPlayCount()
}

function decrementLearnCount() {
  if (state.learnCount > 0) {
    state.learnCount = state.learnCount - GOD_NUMBER
    decrementPlayCount()
  }
}

function incrementPlayCount() {
  state.playCount = state.playCount + GOD_NUMBER * GOD_MULTIPLIER
}

function decrementPlayCount() {
  if (state.playCount > 0) {
    state.playCount = state.playCount - GOD_NUMBER * GOD_MULTIPLIER
  }
}
</script>

<template>
  <div>
    <div>learnCount: {{ state.learnCount }}h</div>
    <div>playCount: {{ state.playCount }}h</div>
    <div>
      <button @click="incrementLearnCount">increment learn</button>
      <button @click="decrementLearnCount">decrement learn</button>
    </div>
    <div>
      <button @click="incrementPlayCount">increment play</button>
      <button @click="decrementPlayCount">decrement play</button>
    </div>
  </div>
</template>
