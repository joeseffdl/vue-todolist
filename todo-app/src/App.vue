<template>
  <div id="app">
  <b-img-lazy v-bind="vueImg" center src="./assets/logo.png" alt="Vue logo"></b-img-lazy>
    <todo-app></todo-app>
  </div>
</template>

<script>
import TodoApp from './components/TodoApp.vue'

export default {
  name: 'App',
  components: {
    TodoApp
  }
}
</script>

<style>
.vue-logo{
  display: flex;
  align-items: center;
  justify-content: center;
}

body {
  background: #35495E;
}
</style>
