<template>
  <div id="app">
    <TodoList /> 
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue'  // можно писать @/components/TodoList.vue

export default {
  name: 'App',
  components: { TodoList },
}
</script>

<style>
</style>