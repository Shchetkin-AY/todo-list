<template>
    <li>
      <span v-bind:class="{done: todo.complited}">
        <input type="checkbox"
               v-on:change="todo.complited = !todo.complited">
        <strong>{{index + 1}}</strong>
        {{todo.title | upperCase}}
      </span>
      <button class="remove"
              v-on:click="$emit('removeTodo', todo.id)"
      >&times;</button>
    </li>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true,
    },
    index: Number
  },
  filters: {
    upperCase(value) {
      return value.toUpperCase();
    }
  }
}

</script>

<style scoped>
  li {
    border: 1px solid #ccc;
    display: flex;
    justify-content: space-between;
    padding: .5rem 2rem;
    margin-bottom: 1rem;

  }

  .remove {
    background: red;
    color: #fff;
    border-radius: 50%;
    font-weight: bold;
  }

  input{
    margin-right: 1rem;
  }

  .done {
    text-decoration: line-through;
  }

</style>
