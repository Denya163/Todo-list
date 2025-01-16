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
    <hr>
    <TodoList 
      v-bind:todos="todos"
      @rm-todo="removeTodo"
    />
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
      ]
    }
  },
  // mounted() {
  //   fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
  //     .then(response => response.json())
  //     .then(json => {
  //       this.todos = json
  //     })
  // },
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
