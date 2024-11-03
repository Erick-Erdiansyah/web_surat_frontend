<script setup>
defineProps({
  msg: {
    type: String,
    required: true
  }
})
</script>

<template>
  <div class="greetings">
    <h1 class="text-gray-100 font-medium text-[2.6rem] relative text-center lg:text-left">{{ msg }}</h1>
  </div>
</template>