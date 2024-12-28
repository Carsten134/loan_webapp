<script setup>
  // const {data, error} = await useAsyncData("api-fetch", () => $fetch("https://carstenstahl.us-east-1.aws.modelbit.com/v1/predict_weather/latest", {
  //   method: 'POST',
  //   body: {data: 2}
  // }))

  async function submitDay() {
    const {data} = await $fetch("https://carstenstahl.us-east-1.aws.modelbit.com/v1/predict_weather/latest", {
      method: 'POST',
      body: {data: day.value}
    })
    console.log(data)
    weather.value = data.weather
  }

  const day = ref(1)
  const weather = ref("")
</script>

<template>
  <div class="flex flex-col justify-center items-center w-screen h-screen">
    <div class="font-bold text-2xl">Call model api</div>
    <p>This component will call an api to return the weather: {{ weather}}</p>
    <input class="font-mono border-solid shadow-md rounded-md border-2" type="number" v-model="day">
    <button class="border-solid border-2 rounded-full shadow-sm p-2 mt-2 hover:font-bold transition-all ease-in-out"
      @click="submitDay">Predict</button>
  </div>
</template>