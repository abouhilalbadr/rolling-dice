<script setup>
  import { ref } from 'vue'
import Dice from './components/Dice.vue'

  const numberDice = ref(1)
  const dicesGenerated = ref([])
  const savedGenerated = ref([])

  // Generate Random Number
  const randomIntFromInterval = (min, max) => {
    return Math.floor(Math.random() * (max - min + 1) + min)
  }

  // Roll the dices
  const rollDice = () => {
    let intervalId = setInterval(generateDice, 200)
    setTimeout(() => clearInterval(intervalId), 2000);
    // Save previous Roll
    savedGenerated.value = [...savedGenerated.value, ...dicesGenerated.value]
  }

  // Generate Dices
  const generateDice = () => {
    // Reset Generated Dices
    dicesGenerated.value = []
    // Generate number of dices by @numberDice
    for (let i = 0; i < numberDice.value; i++) {
      const randomNumber = randomIntFromInterval(1, 6)
      dicesGenerated.value.push(randomNumber)
    }
  }
</script>

<template>
  <div class="flex flex-col gap-8 min-h-screen justify-center items-center p-6">
    <form
      @submit.prevent="rollDice"
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
    <section class="grid grid-cols-3 gap-6">
      <div
        v-for="(item, i) in dicesGenerated"
        :key="i"
        class="border border-gray-400 w-24 h-24 rounded-md px-2 py-1"
      >
        <Dice :number="item" />
      </div>
    </section>
    <section v-if="savedGenerated.length > 0" class="mt-12 w-1/2 opacity-50">
      <h2 class="text-2xl text-left mb-4">Previous rolls</h2>
      <div class="border border-gray-300 p-4 rounded-md">
        <div class="grid grid-cols-5 gap-6">
          <div
            v-for="(item, i) in savedGenerated"
            :key="i"
            class="border border-gray-400 w-24 h-24 rounded-md px-2 py-1"
          >
            <Dice :number="item" />
          </div>
        </div>
      </div>
    </section>
  </div>
</template>
