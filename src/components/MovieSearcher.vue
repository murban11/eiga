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
        <legend>Cast</legend>
        <div>
          <CastButton
            v-for="(c, i) in castSelected"
            :key="i"
            :cast="c"
            @cast-unselect="onCastUnselect"
            />
        </div>
        <input v-model="castInput" type="search" list="castList" />
        <button @click="onCastSelect" type="button">+</button>
        <datalist id="castList">
          <option v-for="(c, i) in cast" :key="i">
            {{ c }}
          </option>
        </datalist>
      </fieldset>
    </form>
  </div>
</template>

<script>
import GenreButton from './GenreButton.vue'
import CastButton from './CastButton.vue'

let _ = require('underscore')

export default {
  data() {
    return {
      genresSelected: [],
      castSelected: [],
      castInput: "",
    }
  },
  components: {
    GenreButton,
    CastButton,
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
    cast: {
      type: Array,
    },
  },
  emits: [
    'title-filter',
    'start-year',
    'end-year',
    'genres-selected',
    'cast-selected',
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
    onCastSelect() {
      if (!_.contains(this.castSelected, this.castInput)) {
        this.castSelected.push(this.castInput);
        this.$emit('cast-selected', this.castSelected);
      }
    },
    onCastUnselect(cast) {
      this.castSelected = _.filter(this.castSelected, (e) => {
        return e !== cast;
      });
      this.$emit('cast-selected', this.castSelected);
    },
    getYears() {
      return _.range(this.minYear, this.maxYear);
    },
  },
}
</script>
