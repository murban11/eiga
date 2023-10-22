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
          <option
            v-for="i in [...Array(2025-1900).keys()].map(j => j + 1900)"
            :key="i"
            >
              {{ i }}
          </option>
        </select>
        <label for="endYear">to:</label>
        <select id="endYear" @input="onEndYearInput">
          <option
            v-for="i in [...Array(2025-1900).keys()].map(j => j + 1900).reverse()"
            :key="i"
            >
              {{ i }}
          </option>
        </select>
      </fieldset>
      <fieldset>
        <legend>Genres (not implemented yet)</legend>
      </fieldset>
      <fieldset>
        <legend>Cast (not implemented yet)</legend>
      </fieldset>
    </form>
  </div>
</template>

<script>
export default {
  emits: [
    'title-filter',
    'start-year',
    'end-year',
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
  },
}
</script>
