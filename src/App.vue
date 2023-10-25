<template>
  <h1>Eiga</h1>
  <MovieSearcher
    :minYear="minYear"
    :maxYear="maxYear"
    :genres="genres"
    :cast="cast"
    @search="search"
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
      genres: _.uniq(_.flatten(_.map(MovieData, (e) => {
        return e.genres;
      }), 1)),
      cast: _.uniq(_.flatten(_.map(MovieData, (e) => {
        return e.cast;
      }), 1)),

      noOfVisible: 10,
      minNoOfVisible: 10,

      minYear: 1900,
      maxYear: 2024,

      titleFilter: '',
      startYear: 1900,
      endYear: 2024,
      genresSelected: [],
      castSelected: [],
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
        });
      }

      if (this.genresSelected.length > 0) {
        filteredMovieList = _.filter(filteredMovieList, (e) => {
          return _.intersection(e.genres, this.genresSelected).length > 0;
        });
      }

      if (this.castSelected.length > 0) {
        filteredMovieList = _.filter(filteredMovieList, (e) => {
          return _.intersection(e.cast, this.castSelected).length > 0;
        });
      }

      return filteredMovieList.slice(0, this.noOfVisible);
    },
    search(msg) {
      this.titleFilter = msg.titleFilter
      this.startYear = msg.startYear
      this.endYear = msg.endYear
      this.genresSelected = msg.genresSelected.slice(0)
      this.castSelected = msg.castSelected.slice(0)
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
