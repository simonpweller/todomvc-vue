<template>
  <header class="header">
    <h1>todos</h1>
    <input
      ref="new-todo"
      v-model="todoText"
      v-on:keypress.enter="handleSubmit"
      v-on:blur="handleSubmit"
      class="new-todo"
      placeholder="What needs to be done?"
    />
  </header>
</template>

<script>
export default {
  data: () => {
    return {
      todoText: "",
    };
  },
  methods: {
    handleSubmit() {
      if (this.todoText.trim().length > 0) {
        this.$emit("add-todo", this.todoText.trim());
        this.todoText = "";
      }
    },
  },
  created() {
    this.$nextTick(function () {
      this.$refs["new-todo"].focus();
    });
  },
};
</script>
