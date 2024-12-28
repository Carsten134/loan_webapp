<script setup>
  const supabase = await useSupabaseClient()
  const {data, error} = await supabase.from("tracker_test").select()
</script>

<template>
  <div class="flex flex-col justify-center items-center w-screen h-screen">
    <div class="text-xl font-bold mb-10">Data Fetcher</div>
    <div>This data was fetched from a remote database</div>
    <!-- <button class="relative bg-slate-700 text-white transition-all hover:ease-in-out p-3 text-xl rounded-full duration-700 hover:shadow-md hover:shadow-orange-500 hover:text-black hover:border-1 hover:border-solid hover:border-orange-500 hover:bg-white"
      >
      Fetch data
    </button> -->
    <div class="text-green-500 font-bold" v-if="!error">Success!</div>
    
    <table class="table-auto border-solid border-2 border-black rounded-md" v-if="!error">
      <thead class="text-2xl border-solid border-2 border-black">
        <tr>
          <td>id</td>
          <td>mood</td>
          <td>weight</td>
        </tr>
      </thead>
      <tbody class="border-solid border-2">
        <tr v-for="row in data" class="p-2" :key="row.id">
          <td>{{ row.id }}</td>
          <td>{{ row.mood }}</td>
          <td>{{ row.weight }}</td>
        </tr>
      </tbody> 
    </table>

    <div v-if="error" class="text-red-600 font-bold text-3xl">Error occured during fetching the data: {{ error }}</div>
  </div>
</template>