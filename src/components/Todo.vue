<template>
  <li :class="{ completed: todo.completed, editing }">
    <div class="view">
      <input
        class="toggle"
        type="checkbox"
        :checked="todo.completed"
        v-on:change="$emit('toggle')"
      />
      <label v-on:dblclick="startEditing">{{ todo.text }}</label>
      <button class="destroy" v-on:click="$emit('destroy')"></button>
    </div>
    <input class="edit" :value="todo.text" ref="input" />
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
  data: () => {
    return {
      editing: false,
    };
  },
  methods: {
    startEditing: function () {
      this.editing = true;
      this.$nextTick(() => {
        this.$refs.input.focus();
      });
    },
  },
};
</script>
