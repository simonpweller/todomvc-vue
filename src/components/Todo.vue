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
    <input
      class="edit"
      v-model="editedText"
      ref="input"
      v-on:blur="finishEditing"
      v-on:keypress.enter="finishEditing"
      v-on:keyup.esc="cancelEditing"
    />
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
  data: function () {
    return {
      editedText: this.todo.text,
      editing: false,
    };
  },
  methods: {
    finishEditing: function () {
      const trimmedText = this.editedText.trim();
      if (trimmedText.length > 0) {
        this.todo.text = trimmedText;
        this.editedText = trimmedText;
        this.editing = false;
      } else {
        this.$emit("destroy");
      }
    },
    cancelEditing: function () {
      this.editedText = this.todo.text;
      this.editing = false;
    },
    startEditing: function () {
      this.editing = true;
      this.$nextTick(() => {
        this.$refs.input.focus();
      });
    },
  },
};
</script>
