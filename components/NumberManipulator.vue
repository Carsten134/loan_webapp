<script setup>
  const count = ref(0);

  function increment() {
    count.value = count.value + 1;
  }
  function decrement() {
    count.value = count.value -1;
  }
</script>
<template>
  <div class="flex flex-col justify-center items-center w-screen h-screen">
    <span class="text-xl font-bold">Number incrementor</span>
    <div class="flex flex-col justify-center items-center">
      <span class="font-mono text-2xl">{{ count }}</span>
      <br>
      <button @click="increment" class="bg-black text-white p-2 rounded-full mb-2">Increment</button>
      <button @click="decrement" class="bg-black text-white p-2 rounded-full">decrement</button>
    </div>
  </div>
</template>