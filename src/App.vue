<template>
  <AddComment />
</template>

<script>
import AddComment from './components/AddComment.vue'

export default {
  name: 'App',
  components: {
    AddComment
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
  /* margin-top: 60px; */
}
</style>
