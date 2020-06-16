<template>
  <section class="todoapp">
    <Header v-on:add-todo="addTodo" />
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
import Header from "./Header";
import Todo from "./Todo";
export default {
  components: {
    Header,
    Todo,
  },
  data: () => {
    return {
      todos: [],
      todoText: "",
    };
  },
  methods: {
    addTodo: function (text) {
      this.todos.push({ text: text, completed: false });
    },
  },
  computed: {
    hasTodos: function () {
      return this.todos.length > 0;
    },
  },
};
</script>
