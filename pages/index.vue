<template>
  <div class="home">
<Hero/>
  </div>
</template>

<script>
// import axios from 'axios'
export default {
  name: 'index',
  data() {
    return {
      movies: [],
    }
  },
async fetch() {
const data = await fetch('https://api.themoviedb.org/3/movie/now_playing?api_key=&language=en-US&page=1')
const response = await data.json()
// console.log(response, "RESULT")

response.results.forEach((movie) =>{
  this.movies.push(movie)
})

console.log(this.movies)

}
}
</script>
