  <!-- удаление заданий работает прямо здесь, а как передать в родительский через props, хуй знает -->

  <template>
    <div> <!-- должен быть только один элемент первого уровня -->
      <ol>
        <li v-bind:key="item" 
        @click="deleteTodo(index)" v-for="item in items">{{ item }}</li>
      </ol>
      
      <label>New task:</label><br><br>
      <input type="text" v-model="newTask" /><br><br>
      <button @click="addTask">Add task</button>
      
      </div>
  </template>

  <script>
  export default {
    name: 'TodoListComponent', 
    // props: ['todos'],
    data() { return {
            items: [],
      }
    },
    methods: { 
      deleteTodo(index) {
        this.items.splice(index, 1);
        // this.$emit('delete-todo', index); // $emit - служебный метод для отлавливания событий и передачи в родитель
      },
      
      addTask() {
        if (this.newTask) {
          this.items.push(this.newTask); 
          this.newTask = '';
        } 
      }
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
