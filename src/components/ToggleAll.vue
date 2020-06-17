<template>
  <div>
    <input
      id="toggle-all"
      class="toggle-all"
      type="checkbox"
      v-on:change="$emit('toggle-all', !allCompleted)"
      :checked="allCompleted"
    />
    <label for="toggle-all">
      Mark all as complete
    </label>
  </div>
</template>

<script>
export default {
  props: {
    todos: Array,
  },
  computed: {
    allCompleted: function () {
      return this.todos.every((todo) => todo.completed);
    },
  },
};
</script>
