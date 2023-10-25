<template>
  <div class="my-4">
    <form class="form">
      <fieldset class="mb-4">
        <legend>Title</legend>
        <input type="text" @input="onTitleInputChange" />
      </fieldset>
      <fieldset class="container mb-4">
        <legend>Release Year</legend>
        <div class="row">
          <div class="form-group col">
            <label for="startYear" class="form-label">from:</label>
            <select
                id="startYear"
                @input="onStartYearInput"
                class="form-select ms-2 me-4 text-center"
                >
              <option v-for="i in getYears()" :key="i">
                  {{ i }}
              </option>
            </select>
          </div>
          <div class="form-group col">
            <label for="endYear" class="form-label">to:</label>
            <select
                id="endYear"
                @input="onEndYearInput"
                class="form-select ms-2 text-center"
                >
              <option v-for="i in getYears().reverse()" :key="i">
                  {{ i }}
              </option>
            </select>
          </div>
        </div>
      </fieldset>
      <fieldset class="mb-4">
        <legend>Genres</legend>
        <GenreButton
          v-for="(genre, i) in genres"
          :key="i"
          :genre="genre"
          @select-toggle="onGenreToggle"
          />
      </fieldset>
      <fieldset class="mb-4">
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
        <button @click="onCastSelect" type="button" id="castAdd">+</button>
        <datalist id="castList">
          <option v-for="(c, i) in cast" :key="i">
            {{ c }}
          </option>
        </datalist>
      </fieldset>
      <button
        @click="onSearchButtonClick"
        type="button"
        class="btn btn-primary"
        >
          Search
      </button>
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
      titleFilter: "",
      startYear: this.minYear,
      endYear: this.maxYear,
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
    'search',
  ],
  methods: {
    onTitleInputChange(e) {
      this.titleFilter = e.target.value
    },
    onStartYearInput(e) {
      this.startYear = e.target.value
    },
    onEndYearInput(e) {
      this.endYear = e.target.value
    },
    onGenreToggle(genre) {
      if (_.contains(this.genresSelected, genre)) {
        this.genresSelected = _.filter(this.genresSelected, (e) => {
          return e !== genre;
        });
      } else {
        this.genresSelected.push(genre)
      }
    },
    onCastSelect() {
      if (!_.contains(this.castSelected, this.castInput)) {
        this.castSelected.push(this.castInput);
      }
    },
    onCastUnselect(cast) {
      this.castSelected = _.filter(this.castSelected, (e) => {
        return e !== cast;
      });
    },
    getYears() {
      return _.range(this.minYear, this.maxYear);
    },
    onSearchButtonClick() {
      this.$emit('search', {
        titleFilter: this.titleFilter,
        startYear: this.startYear,
        endYear: this.endYear,
        genresSelected: this.genresSelected,
        castSelected: this.castSelected,
      })
    }
  },
}
</script>

<style>
.form-select {
  background-color: #A9B1D6;
}

#castAdd {
  background-color: #7AA2F7;
}

.btn-primary {
  color: #1A1B26;
  border-color: #7AA2F7;
  background-color: #7AA2F7;
}
</style>
