<template>
  <section class="todoapp">
    <Header v-on:add-todo="addTodo" />
    <section v-if="hasTodos" class="main">
      <input
        id="toggle-all"
        class="toggle-all"
        type="checkbox"
        v-on:change="toggleAll"
        :checked="allCompleted"
      />
      <label for="toggle-all">Mark all as complete</label>
      <ul class="todo-list">
        <Todo
          v-for="todo in todos"
          :key="todo.id"
          :todo="todo"
          v-on:toggle="todo.completed = !todo.completed"
        />
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
import { v4 as uuid } from "uuid";
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
      this.todos.push({ id: uuid(), text: text, completed: false });
    },
    toggleAll: function () {
      this.todos = this.todos.map((todo) => ({
        ...todo,
        completed: !this.allCompleted,
      }));
    },
  },
  computed: {
    hasTodos: function () {
      return this.todos.length > 0;
    },
    allCompleted: function () {
      return this.todos.every((todo) => todo.completed);
    },
  },
};
</script>
