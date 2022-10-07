<script setup>
defineProps(['number'])

const flexClasses = (number) => {
  switch (number) {
    case 1:
      return 'justify-center items-center'
      break;
    case 2:
      return 'justify-between second-face'
      break
    case 3:
      return 'justify-between third-face'
      break
    case 4:
      return 'justify-between grid grid-cols-2 fourth-face'
      break
    case 5:
      return 'justify-between grid grid-cols-2 fifth-face'
      break
    case 6:
      return 'justify-between grid grid-cols-2 sixth-face'
      break
    default:
      break;
  }
}

</script>
<template>
  <div
    class="flex h-full relative"
    :class="flexClasses(number)"
  >
    <div
      v-for="i in number"
      :key="i"
      class="dot"
    >
      <div class="w-6 h-6 bg-black rounded-full"></div>
  </div>
  </div>
</template>