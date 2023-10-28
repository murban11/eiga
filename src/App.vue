<template>
  <h1>Eiga</h1>
  <MovieSearcher
    :minYear="minYear"
    :maxYear="maxYear"
    :genres="genres"
    :cast="cast"
    @search="search"
    />
  <MovieList
    :movieData="filterMovies()"
    :noOfEntries="noOfEntries"
    />
  <span v-if="noOfEntries == 0">No matching results found</span>
  <button
    @click="showMore"
    v-if="noOfVisible < noOfEntries"
    class="btn btn-primary"
    >
      Show more
  </button>
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
      genres: _.uniq(_.flatten(_.map(MovieData, _.property('genres')), 1)).sort(),
      cast: _.uniq(_.flatten(_.map(MovieData, _.property('cast')), 1)),

      noOfVisible: 10,
      minNoOfVisible: 10,
      noOfEntries: 0,

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
        return (e.year >= this.startYear && e.year <= this.endYear)
            && (this.titleFilter === ''
                || e.title.toLowerCase().includes(this.titleFilter.toLowerCase()))
            && (this.genresSelected.length == 0
                || _.intersection(e.genres, this.genresSelected).length > 0)
            && (this.castSelected.length == 0
                || _.intersection(e.cast, this.castSelected).length > 0)
      });

      this.noOfEntries = filteredMovieList.length

      return filteredMovieList.slice(0, this.noOfVisible);
    },
    search(msg) {
      this.noOfVisible = this.minNoOfVisible
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
  color: #C0CAF5;
  background-color: #1A1B26;
}

body {
    background-color: #F7768E;
}

input {
    color: #1A1B26;
    border-color: #A9B1D6;
    background-color: #A9B1D6;
}

.btn-primary {
  color: #1A1B26;
  border-color: #7AA2F7;
  background-color: #7AA2F7;
}
</style>
