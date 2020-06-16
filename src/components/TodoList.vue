<template>
  <section class="todoapp">
    <header class="header">
      <h1>todos</h1>
      <input
        ref="new-todo"
        v-model="todoText"
        v-on:keypress.enter="addTodo"
        v-on:blur="addTodo"
        class="new-todo"
        placeholder="What needs to be done?"
      />
    </header>
    <section v-if="hasTodos" class="main">
      <input id="toggle-all" class="toggle-all" type="checkbox" />
      <label for="toggle-all">Mark all as complete</label>
      <ul class="todo-list">
        <Todo v-for="todo in todos" :key="todo.id" v-bind:todo="todo" />
      </ul>
    </section>
    <footer v-if="hasTodos" class="footer">
      <span class="todo-count"><strong>0</strong> item left</span>
      <ul class="filters">
        <li>
          <a class="selected" href="#/">All</a>
        </li>
        <li>
          <a href="#/active">Active</a>
        </li>
        <li>
          <a href="#/completed">Completed</a>
        </li>
      </ul>
      <button class="clear-completed">Clear completed</button>
    </footer>
  </section>
</template>

<script>
import Todo from "./Todo";
export default {
  components: {
    Todo,
  },
  data: () => {
    return {
      todos: [],
      todoText: "",
    };
  },
  methods: {
    addTodo: function () {
      if (this.todoText.trim().length > 0) {
        this.todos.push({ text: this.todoText.trim(), completed: false });
        this.todoText = "";
      }
    },
  },
  computed: {
    hasTodos: function () {
      return this.todos.length > 0;
    },
  },
  created() {
    this.$nextTick(function () {
      this.$refs["new-todo"].focus();
    });
  },
};
</script>
