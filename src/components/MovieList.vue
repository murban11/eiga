<template>
  <div>
    <h2>Movies</h2>
    <ul>
      <li v-for="(movie, i) in movieData" :key="i">
        {{ movie.title }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    movieData: {
      type: Array,
    }
  },
}
</script>
