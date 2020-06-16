<template>
  <li>
    <div class="view">
      <input class="toggle" type="checkbox" />
      <label>{{ todo.text }}</label>
      <button class="destroy"></button>
    </div>
    <input class="edit" :value="todo.text" />
  </li>
</template>

<script>
export default {
  props: {
    todo: {
      text: String,
    },
  },
};
</script>
