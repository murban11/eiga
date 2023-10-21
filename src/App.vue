<template>
  <SimpleHeader />
</template>

<script>
import SimpleHeader from './components/SimpleHeader.vue'

export default {
  name: 'App',
  components: {
    SimpleHeader
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
