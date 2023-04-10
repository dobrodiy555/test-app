<!-- Первоначальное приложение из видео -->
<!-- App.vue -->
<template>
  <div id="app">
    <TodoList v-bind:todos="todos" @delete-todo="deleteTodo" /> <!-- слушаем событие от ребенка ToDoList -->
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue'

export default {
  name: 'App',
  data: function() { // data нужно в виде ф-ции
    return {
      todos: ['do homework', 'go to rztk', 'play fifa']
    }
  },
  components: {
    TodoList
  },
  methods: {
    deleteTodo(index) {
      this.todos.splice(index, 1);  // что будем делать с событием от ребенка
    }
  }
}
</script>
<style>
</style>

<!-- TodoList.vue -->
<template>
  <div>
    <ol>
      <li v-for="(todo, index) in todos" v-bind:key="index" v-on:click="deleteTodo(index)">{{ todo }}</li>
    </ol>
    
    <label for="input">New task:</label><br><br>
    <input id="input" type="text" v-model="newTask" /><br><br>
    <button @click="addTask">
      Add task
    </button>
    
    </div>
</template>

<script>
export default {
  name: 'TodoListComponent', 
  props: ['todos'],
  methods: { 
    deleteTodo(index) {
      this.$emit('delete-todo', index); // $emit - служебный метод для отлавливания событий
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  * {
    box-sizing: border-box;
  }

  body {
    font-family: 'Gloria Hallelujah', cursive;
    font-size: 1.4rem;
    background: whitesmoke;
    margin: 0;
    padding: 1rem;
    display: grid;
    place-items: center;
    min-height: 100vh;
  }

  ol {
    list-style-position: inside;
    width: 600px;
    max-width: 100%;
    background: white;
    box-shadow: 0.25rem 0.25rem 0.75rem rgb(0 0 0 / 0.15);
    padding: 0;
    margin: 0;
    border-radius: 0.1rem;
  }

  li {
    padding: 0 0 0 1rem;
    height: 50px;
  }

  li:not(:last-child) {
    border-bottom: 1px solid lightblue;
  }

  li:first-child {
    margin-top: 1rem;
  }

  li:last-child {
    margin-bottom: 1rem;
  }

  ::marker {
    --image: '📩 ';
    content: counter(list-item) ' ' var(--image);
  }

  li:nth-child(2)::marker {
    --image: '🐈 ';
  }

  li:nth-child(3)::marker {
    --image: '🗑 ';
  }

  li:nth-child(4)::marker {
    --image: '🪴 ';
  }

  li:nth-child(5)::marker {
    --image: '🔑 ';
  }
</style>
