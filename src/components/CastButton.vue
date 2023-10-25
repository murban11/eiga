<template>
  <button
      @click="onClick"
      :class="cast"
      class="btn btn-secondary m-1"
      type="button"
      >
    {{ cast }}
  </button>
</template>

<script>
export default {
  props: {
    cast: {
      type: String,
    },
  },
  emits: [
    'cast-unselect',
  ],
  methods: {
    onClick() {
      this.$emit('cast-unselect', this.cast);
    },
  },
}
</script>

<style>
.cast {
  background-color: #E0AF68;
}
</style>
