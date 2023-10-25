<template>
  <button
      @click="onClick"
      :class="{ selected: isSelected }"
      class="btn btn-secondary m-1"
      type="button"
      >
    {{ genre }}
  </button>
</template>

<script>
export default {
  data() {
    return {
      isSelected: false,
    }
  },
  props: {
    genre: {
      type: String,
    },
  },
  emits: [
    'select-toggle',
  ],
  methods: {
    onClick() {
      this.isSelected = !this.isSelected;
      this.$emit('select-toggle', this.genre);
    },
  },
}
</script>

<style>
.selected {
  background-color: #E0AF68;
}
.selected:hover {
  background-color: #E0AF68;
}
</style>
