<template>
  <li :class="{ completed: todo.completed }">
    <div class="view">
      <input
        class="toggle"
        type="checkbox"
        :checked="todo.completed"
        v-on:change="$emit('toggle')"
      />
      <label>{{ todo.text }}</label>
      <button class="destroy" v-on:click="$emit('destroy')"></button>
    </div>
    <input class="edit" :value="todo.text" />
  </li>
</template>

<script>
export default {
  props: {
    todo: {
      text: String,
      completed: Boolean,
    },
  },
};
</script>
