<template>
  <div>
    <ul>
      <ToDoItem
      v-for="(todo, index) of todos"
      v-bind:todo="todo"
      v-bind:index="index"
      v-on:removeTodo="removeTodo"
      />
    </ul>
  </div>
</template>

<script>
import ToDoItem from '@/components/ToDoItem'

export default {
  props: ['todos'],
  components: {
    ToDoItem,
  },
  methods: {
    removeTodo(id) {
      this.$emit('removeTodo', id)
    }
  }
}
</script>

<style scoped>
  ul {
    list-style: none;
    margin: 0;
    padding: 0;
  }
</style>
