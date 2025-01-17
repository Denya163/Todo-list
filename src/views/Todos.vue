<template>
  <div>
    <AddTodo 
        @add-todo="addTodo"
    />
    
    <div>
      <select v-model="filter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="not-completed">Not completed</option>
    </select>
    </div>
    
    <Loader v-if="loading" />
    <TodoList 
      v-else-if="filteredTodos.length"
      v-bind:todos="filteredTodos"
      @rm-todo="removeTodo"
    />
    <p v-else>No todos.</p>

    <div>
      <router-link to="/">Home</router-link>
    </div>
  </div>
</template>



<script>
import TodoList from '@/components/Todo/List'
import AddTodo from '@/components/Todo/Add'
import Loader from '@/components/Loader/Loader'
export default {
  name: 'App',
  data() {
    return {
      todos: [],
      loading: true,
      filter: 'all'
    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
      .then(response => response.json())
      .then(json => {
          this.todos = json
          this.loading = false
      })
  },
  watch: {
    filter(value) {
      console.log(value)
    }
  },
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
    TodoList, AddTodo, Loader
  }
}
</script>



<style>
select {
  margin: 10px;
}
</style>