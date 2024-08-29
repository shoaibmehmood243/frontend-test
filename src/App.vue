<template>
  <div id="app">
    <PageSelector />
  </div>
</template>

<script>
import PageSelector from './components/PageSelector.vue'

export default {
  name: 'App',
  components: {
    PageSelector
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #1F2128;
  margin-top: 60px;
}
</style>
