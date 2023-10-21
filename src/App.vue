<template>
  <SimpleHeader />
  <MovieSearcher />
  <MovieList :movieData="movieData.slice(0, noOfVisible)" />
  <button @click="showMore">Show more</button>
</template>

<script>
import SimpleHeader from './components/SimpleHeader.vue'
import MovieSearcher from './components/MovieSearcher.vue'
import MovieList from './components/MovieList.vue'
import MovieData from './assets/movie-data/movies.json'

export default {
  name: 'App',
  components: {
    SimpleHeader,
    MovieSearcher,
    MovieList,
  },
  data() {
    return {
      noOfVisible: 10,
      movieData: MovieData
    }
  },
  methods: {
    showMore() {
      this.noOfVisible += 10
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
