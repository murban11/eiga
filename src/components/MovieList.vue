<template>
  <div>
    <h2>Movies</h2>
    <div class="my-4">
      <div v-for="(movie, i) in movieData" :key="i" class="container my-2">
        <div class="row">
          <div class="col-2 text-end">
            Title:
          </div>
          <div class="col-10 text-start">
            {{ movie.title }}
          </div>
        </div>
        <div class="row">
          <div class="col-2 text-end">
            Year:
          </div>
          <div class="col-10 text-start">
            {{ movie.year }}
          </div>
        </div>
        <div class="row">
          <div class="col-2 text-end">
            Genres:
          </div>
          <div class="col-10 text-start">
            {{ movie.genres.join(', ') }}
          </div>
        </div>
        <div class="row">
          <div class="col-2 text-end">
            Cast:
          </div>
          <div class="col-10 text-start">
            {{ movie.cast.join(', ') }}
          </div>
        </div>
      </div>
    </div>
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
