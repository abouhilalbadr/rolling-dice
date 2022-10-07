<script setup>
  import { ref } from 'vue'
  import Dice from './components/Dice.vue'

  const numberDice = ref(1)
  const dicesGenerated = ref([1, 2, 3, 4, 5, 6])

  // Generate Random Number
  const randomIntFromInterval = (min, max) => {
    return Math.floor(Math.random() * (max - min + 1) + min)
  }

  const roleDice = () => {
    // Reset Generated Dices
    dicesGenerated.value = []
    // Generate number of dices by @numberDice
    for (let i = 0; i < numberDice.value; i++) {
      const randomNumber = randomIntFromInterval(1, 6)
      dicesGenerated.value.push(randomNumber)
    }
    // TODO: Role the dices
  }
</script>

<template>
  <div class="flex flex-col gap-8 min-h-screen justify-center items-center p-6">
    <form
      @submit.prevent="roleDice"
      class="w-1/2 lg:w-1/4 relative"
    >
      <div class="flex flex-col items-center justify-center gap-4">
        <label for="number" class="text-2xl">Number of dice</label>
        <input
          type="number" id="number" min="1" max="99"
          class="w-full border border-gray-300 px-4 py-2 rounded-md focus:outline-none"
          v-model="numberDice"
        />
        <button type="submit" class="w-full bg-blue-400 text-white flex justify-center items-center h-12 rounded-md">Roll</button>
      </div>
    </form>
    <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
      <div
        v-for="(item, i) in dicesGenerated"
        :key="i"
        class="border border-gray-400 w-24 h-24 rounded-md px-2 py-1"
      >
        <Dice :number="item" />
      </div>
    </div>
  </div>
</template>
