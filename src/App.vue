<template>
  <h1>Eiga</h1>
  <MovieSearcher
    :minYear="minYear"
    :maxYear="maxYear"
    @title-filter="onTitleFilterChange"
    @start-year="onStartYearChange"
    @end-year="onEndYearChange"
    />
  <MovieList :movieData="filterMovies()" />
  <button @click="showMore">Show more</button>
</template>

<script>
import MovieSearcher from './components/MovieSearcher.vue'
import MovieList from './components/MovieList.vue'
import MovieData from './assets/movie-data/movies.json'

let _ = require('underscore')

export default {
  name: 'App',
  components: {
    MovieSearcher,
    MovieList,
  },
  data() {
    return {
      movieData: MovieData,

      noOfVisible: 10,
      minNoOfVisible: 10,

      minYear: 1900,
      maxYear: 2024,

      titleFilter: '',
      startYear: 1900,
      endYear: 2024,
    }
  },
  methods: {
    showMore() {
      this.noOfVisible += this.minNoOfVisible
    },
    filterMovies() {
      let filteredMovieList = _.filter(this.movieData, (e) => {
        return e.year >= this.startYear && e.year <= this.endYear;
      });

      if (this.titleFilter !== '') {
        filteredMovieList = _.filter(filteredMovieList, (e) => {
          return e.title === this.titleFilter;
        })
      }

      return filteredMovieList.slice(0, this.noOfVisible);
    },
    onTitleFilterChange(msg) {
      this.titleFilter = msg;
      this.noOfVisible = this.minNoOfVisible;
    },
    onStartYearChange(msg) {
      this.startYear = msg;
      this.noOfVisible = this.minNoOfVisible;
    },
    onEndYearChange(msg) {
      this.endYear = msg;
      this.noOfVisible = this.minNoOfVisible;
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
