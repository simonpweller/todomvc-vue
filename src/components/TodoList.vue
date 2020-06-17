<template>
  <section class="todoapp">
    <Header v-on:add-todo="addTodo" />
    <section v-if="hasTodos" class="main">
      <ToggleAll :todos="todos" v-on:toggle-all="toggleAll" />
      <ul class="todo-list">
        <Todo
          v-for="todo in todos"
          :key="todo.id"
          :todo="todo"
          v-on:toggle="todo.completed = !todo.completed"
          v-on:destroy="todos = todos.filter((t) => t.id !== todo.id)"
        />
      </ul>
    </section>
    <footer v-if="hasTodos" class="footer">
      <TodoCounter :todos="todos" />
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
import ToggleAll from "./ToggleAll";
import TodoCounter from "./TodoCounter";

export default {
  components: {
    TodoCounter,
    ToggleAll,
    Header,
    Todo,
  },
  data: () => {
    return {
      todos: [],
    };
  },
  methods: {
    addTodo: function (text) {
      this.todos.push({ id: uuid(), text: text, completed: false });
    },
    toggleAll: function (completed) {
      this.todos = this.todos.map((todo) => ({ ...todo, completed }));
    },
  },
  computed: {
    hasTodos: function () {
      return this.todos.length > 0;
    },
  },
};
</script>
