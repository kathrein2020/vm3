<script setup>
import {ref, onMounted, defineAsyncComponent } from "vue"
import Banner from "./components/Banner.vue";

const movies = ref([])
const bannerMovie = ref(null)

const AsyncBanner = defineAsyncComponent(() => {
  return import("./components/Banner.vue")
})
//получить через async данные из components/Banner.vue
//которая до этого сама импортировала через  :banner = "bannerMovie"  в template 
//


const getMovies = async () => {
  movies.value = await fetch("https://api.themoviedb.org/3/movie/popular?api_key=4e44d9029b1270a757cddc766a1bcb63&language=en-US")
  .then(res => res.json())
  .then(res => res.results)
}

//генер р чисел
const getRandomInt = (min, max)  => 
{
  return Math.floor(Math.random() * (max - min) + min)
}     

onMounted(async() => {
  await getMovies() 

  console.log(movies.value)

  //гл. баннер на основе генератора
  bannerMovie.value = movies.value[getRandomInt(0, movies.value.length - 1)]

})

//console.log(bannerMovie.value)
</script>


<template>


   <AsyncBanner
   :banner = "bannerMovie"   
   
   />



</template>


















<style>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
