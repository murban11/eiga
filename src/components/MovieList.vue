<template>
  <div>
    <h2>Movies</h2>
    <div v-if="noOfEntries > 10">
      {{ movieData.length }} of {{ noOfEntries }} results
    </div>
    <div class="my-4">
      <div
          v-for="(movie, i) in movieData"
          :key="i"
          class="movie my-2 p-2 container">
        <div class="row">
          <div class="col-1">
            <span class="align-middle">
              {{ i + 1 }}
            </span>
          </div>
          <div class="col-11 container">
            <div class="row">
              <div class="col-2 text-end">
                Title:
              </div>
              <div class="col-9 text-start">
                {{ movie.title }}
              </div>
            </div>
            <div class="row">
              <div class="col-2 text-end">
                Year:
              </div>
              <div class="col-9 text-start">
                {{ movie.year }}
              </div>
            </div>
            <div class="row">
              <div class="col-2 text-end">
                Genres:
              </div>
              <div class="col-9 text-start">
                {{ movie.genres.join(', ') }}
              </div>
            </div>
            <div class="row">
              <div class="col-2 text-end">
                Cast:
              </div>
              <div class="col-9 text-start">
                {{ movie.cast.join(', ') }}
              </div>
            </div>
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
    noOfEntries: {
      type: Number,
    },
  }
}
</script>

<style>
.movie {
  border-color: #A9B1D6;
  border-style: solid;
  border-radius: 1em;
}
</style>
