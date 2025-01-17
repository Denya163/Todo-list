<template>
    <div>
        <ul>
            <TodoItem 
              v-for="(todo, i) of todos"
              v-bind:todo="todo"
              v-bind:index="i"
              @rm-todo="removeTodo"
            />
        </ul>
    </div>
</template>

<script>
import TodoItem from '@/components/Todo/Item'
export default {
    props: ['todos'],
    components: {
        TodoItem
    },
    methods: {
        removeTodo(id) {
            this.$emit('rm-todo', id)
        }
    }
}
</script>

<style scoped>
  ul {
    list-style: none;
    margin: 0;
    padding: 0;
    width: 50%;
    padding-left: 25%;
  }
</style>