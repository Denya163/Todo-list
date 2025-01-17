<template>
  <div id="app">
    <nav>
      <router-link to="/">Home</router-link>
      <router-link to="/about">About</router-link>
    </nav>
    <router-view />
    
    <h1>Todo app</h1>
    <AddTodo 
        @add-todo="addTodo"
    />
    <select v-model="filter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="not-completed">Not completed</option>
    </select>
    <hr>
    <TodoList 
      v-if="filteredTodos.length"
      v-bind:todos="filteredTodos"
      @rm-todo="removeTodo"
    />
    <p v-else>No todos.</p>
  </div>
</template>

<script>
import TodoList from '@/components/TodoList'
import AddTodo from '@/components/AddTodo'
export default {
  name: 'App',
  data() {
    return {
      todos: [
        {id: 1, title: 'Завтрак', completed: false},
        {id: 2, title: 'Обед', completed: false},
        {id: 3, title: 'Ужин', completed: false},
      ],
      filter: 'all'
    }
  },
  // mounted() {
  //   fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
  //     .then(response => response.json())
  //     .then(json => {
  //       this.todos = json
  //     })
  // },
  // watch: {
  //   filter(value) {
  //     console.log(value)
  //   }
  // },
  computed: {
    filteredTodos() {
      if (this.filter === 'all') {
        return this.todos
      }

      if (this.filter === 'completed') {
        return this.todos.filter( t => t.completed)
      }

      if (this.filter === 'not-completed') {
        return this.todos.filter( t => !t.completed)
      }
    }
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(t => t.id !== id)
    },
    addTodo(todo) {
      this.todos.push(todo)
    }
  },
  components: {
    TodoList, AddTodo,
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
