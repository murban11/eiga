<template>
  <div>
    <h2>Movies</h2>
    <ul>
      <li v-for="(movie, i) in movieData" :key="i">
        Title: {{ movie.title }}<br>
        Year: {{ movie.year }}<br>
        Cast: {{ movie.cast }}<br>
        Genres: {{ movie.genres }}<br>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    movieData: {
      type: Array,
    },
  }
}
</script>
