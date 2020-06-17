<template>
  <span class="todo-count"
    ><strong>{{ activeTodoCount }}</strong>
    {{ activeTodoCount === 1 ? "item" : "items" }} left</span
  >
</template>
<script>
export default {
  props: {
    todos: Array,
  },
  computed: {
    activeTodoCount: function () {
      return this.todos.filter((todo) => !todo.completed).length;
    },
  },
};
</script>
