<script setup lang ="ts">
const search = ref("Toronto")
const input = ref("");
const handleclick = () => {
const formatedsearch = input.value.trim().split(" ").join("+");
search.value = formatedsearch;
input.value = "";
}
const{data: city , error}= useFetch(
  () => `https://api.openweathermap.org/data/2.5/weather?q=${search.value}&appid=43f6ac9b093def3688b1a1cd8cb7c881`
);

// const{data:city , error} = useAsyncData ("city" , async() =>{
//   const response = await $fetch(
//     `https://api.openweathermap.org/data/2.5/weather?q=${search.value}&appid=43f6ac9b093def3688b1a1cd8cb7c881`
//     return response;
// );

</script>
<template>
<div class="h-screen relative overflow-hidden">
<img />
<div class ="absolute w-full h-full top-0 overlay" />
<div class = "absolute w-full h-full top-0 p-48">
<div class ="flex justify-between">
  <div>
  <h1 class ="text-7xl text-white">{{city.name}}</h1>
  <p class="font-extralight text-2xl mt-2 text-white">sunday dec 9th</p>
  <img :src="`https://openweathermap.org/img/wn/${city.weather[0].icon}@4x.png`"  class="w-56 icon"/>
</div>
<div>
<p class ="text-9xl text-white font-extralight">{{city.main.temp}}</p>
</div>
</div>
<div class="mt-20">
  <input type ="text" class="w-1/2 h-10" placeholder="find a city" v-model = "input" />
  <button class = "bg-sky-400 w-20 text-white h-10" @click="handleclick"> search</button>
</div>
</div>
</div>
</template>

<style scoped>
.overlay{
  background-color: rgba(0,0,0,0.5);
}
.icon{
  margin-left: -2.75rem;
  margin-top: -2.75rem;
}
</style>