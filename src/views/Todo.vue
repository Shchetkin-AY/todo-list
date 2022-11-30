<template>
  <div>
    <h2>Todo application</h2>
    <router-link to="/">Home</router-link>
    <hr>
    <AddToDo
        @add-todo="addTodo"
    />

    <select v-model="filter">
      <option value="all">All</option>
      <option value="complited">Complited</option>
      <option value="not-complited">Not complited</option>
    </select>
    <hr>
    <Loader v-if="loading"/>
    <TodoList
        v-else-if="filteredTodo.length"
        v-bind:todos="filteredTodo"
        @removeTodo="removeTodo"
    />
    <p v-else>No todos</p>
  </div>
</template>

<script>

import TodoList from '@/components/ToDoList'
import AddToDo from '@/components/AddToDo'
import Loader from '@/components/Loader'

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
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=5')
        .then(response => response.json())
        .then(json => {
          setTimeout(() => {
            this.todos = json
            this.loading = false
          }, 1000)
        })
  },
  components: {
    TodoList,
    AddToDo,
    Loader,
  },
  computed: {
    filteredTodo() {
      if (this.filter ===  'all') {
        return this.todos
      }
      if (this.filter ===  'complited') {
        return this.todos.filter(t => t.completed)
      }
      if (this.filter ===  'Not complited') {
        return this.todos.filter(t => !t.completed)
      }
    }
  },
  // watch: {
  //   filter(value) {
  //     console.log(value)
  //   }
  // },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(t => t.id !== id)
    },
    addTodo(todo) {
      this.todos.push(todo);
    }
  }
}
</script>
