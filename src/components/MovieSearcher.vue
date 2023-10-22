<template>
  <div>
    <form>
      <fieldset>
        <legend>Title</legend>
        <input type="text" @input="onTitleInputChange" />
      </fieldset>
      <fieldset>
        <legend>Release Year</legend>
        <label for="startYear">from:</label>
        <select id="startYear" @input="onStartYearInput"> 
          <option v-for="i in getYears()" :key="i">
              {{ i }}
          </option>
        </select>
        <label for="endYear">to:</label>
        <select id="endYear" @input="onEndYearInput">
          <option v-for="i in getYears().reverse()" :key="i">
              {{ i }}
          </option>
        </select>
      </fieldset>
      <fieldset>
        <legend>Genres</legend>
        <GenreButton
          v-for="(genre, i) in genres"
          :key="i"
          :genre="genre"
          @select-toggle="onGenreToggle"
          />
      </fieldset>
      <fieldset>
        <legend>Cast (not implemented yet)</legend>
      </fieldset>
    </form>
  </div>
</template>

<script>
import GenreButton from './GenreButton.vue'

let _ = require('underscore')

export default {
  data() {
    return {
      genresSelected: [],
    }
  },
  components: {
    GenreButton,
  },
  props: {
    minYear: {
      type: Number,
    },
    maxYear: {
      type: Number,
    },
    genres: {
      type: Array,
    },
  },
  emits: [
    'title-filter',
    'start-year',
    'end-year',
    'genres-selected',
  ],
  methods: {
    onTitleInputChange(e) {
      this.$emit('title-filter', e.target.value)
    },
    onStartYearInput(e) {
      this.$emit('start-year', e.target.value)
    },
    onEndYearInput(e) {
      this.$emit('end-year', e.target.value)
    },
    onGenreToggle(genre) {
      if (_.contains(this.genresSelected, genre)) {
        this.genresSelected = _.filter(this.genresSelected, (e) => {
          return e !== genre;
        });
      } else {
        this.genresSelected.push(genre)
      }
      this.$emit('genres-selected', this.genresSelected)
    },
    getYears() {
      return _.range(this.minYear, this.maxYear);
    },
  },
}
</script>
