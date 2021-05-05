<template>
  <div id="app">
    <CreateToDo></CreateToDo>
  </div>
</template>

<script>
import CreateToDo from './components/CreateToDo.vue'
export default {
  name: 'App',
  components: {
    CreateToDo
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>