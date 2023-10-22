<template>
  <SimpleHeader />
  <MovieSearcher @title-filter="onTitleFilterChange" />
  <MovieList :movieData="filterMovies()" />
  <button @click="showMore">Show more</button>
</template>

<script>
import SimpleHeader from './components/SimpleHeader.vue'
import MovieSearcher from './components/MovieSearcher.vue'
import MovieList from './components/MovieList.vue'
import MovieData from './assets/movie-data/movies.json'

let _ = require('underscore')

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
      movieData: MovieData,

      titleFilter: '',
    }
  },
  methods: {
    showMore() {
      this.noOfVisible += 10
    },
    filterMovies() {
      let filteredMovieList = this.movieData;

      if (this.titleFilter !== '') {
        filteredMovieList = _.filter(this.movieData, (e) => {
          return e.title === this.titleFilter;
        })
      }

      return filteredMovieList.slice(0, this.noOfVisible);
    },
    onTitleFilterChange(msg) {
      this.titleFilter = msg;
      this.noOfVisible = 10;
    },
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
