<template>
  <div>
    <form>
      <fieldset>
        <legend>Title</legend>
        <input type="text" @input="titleInputChanged" />
      </fieldset>
      <fieldset>
        <legend>Release Year (not implemented yet)</legend>
        <label for="startYear">from:</label>
        <select id="startYear">
          <option
            v-for="i in [...Array(2025-1900).keys()].map(j => j + 1900)"
            :key="i"
            >
              {{ i }}
          </option>
        </select>
        <label for="endYear">to:</label>
        <select id="endYear">
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
  ],
  methods: {
    titleInputChanged(e) {
      this.$emit('title-filter', e.target.value)
    }
  },
}
</script>
