<script setup lang="ts">
import { reactive, onMounted, watch } from 'vue'
import CounterDisplay from './CounterDisplay.vue'

const GOD_NUMBER = 0.5
const GOD_MULTIPLIER = 2
const GOD_KEY = 'GOD_COUNTERS'

type CounterData = {
  learnCount: number
  playCount: number
  date: string
}

function isCounterData(o: any): o is CounterData {
  return 'date' in o && 'learnCount' in o && 'playCount' in o
}

interface State {
  learnCount: number
  playCount: number
  isLoading: boolean
}

const state: State = reactive({
  learnCount: 0,
  playCount: 0,
  isLoading: true,
})

onMounted(() => {
  const dataString = localStorage.getItem(GOD_KEY)
  if (!dataString) {
    state.isLoading = false
    return
  }

  try {
    const data = JSON.parse(dataString)
    if (isCounterData(data)) {
      if (isToday(new Date(data.date))) {
        state.learnCount = data.learnCount
        state.playCount = data.playCount
      }
    }
  } catch (e) {
    localStorage.removeItem(GOD_KEY)
  } finally {
    state.isLoading = false
  }
})

watch(state, (newState) => {
  const dataString = JSON.stringify({
    learnCount: newState.learnCount,
    playCount: newState.playCount,
    date: new Date().toJSON(),
  } as CounterData)
  localStorage.setItem(GOD_KEY, dataString)
})

function isToday(date: Date) {
  const today = new Date()
  return (
    date.getDate() === today.getDate() &&
    date.getMonth() === today.getMonth() &&
    date.getFullYear() === today.getFullYear()
  )
}

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
  <CounterDisplay
    title="Learn Count"
    :is-disabled="state.isLoading"
    :count="state.learnCount"
    @increment-count="incrementLearnCount"
    @decrement-count="decrementLearnCount"
  />

  <CounterDisplay
    title="Play Count"
    :is-disabled="state.isLoading"
    :count="state.playCount"
    @increment-count="incrementPlayCount"
    @decrement-count="decrementPlayCount"
    class="counter"
  />
</template>

<style scoped>
.counter {
  margin-top: 4rem;
}
</style>
