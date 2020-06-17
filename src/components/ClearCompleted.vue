<template>
  <button
    class="clear-completed"
    v-show="todos.some((todo) => todo.completed)"
    v-on:click="$emit('clear')"
  >
    Clear completed
  </button>
</template>

<script>
export default {
  props: {
    todos: Array,
  },
};
</script>
