<template>
  <section class="todoapp">
    <Header v-on:add-todo="addTodo" />
    <section v-if="hasTodos" class="main">
      <ToggleAll :todos="todos" v-on:toggle-all="toggleAll" />
      <ul class="todo-list">
        <Todo
          v-for="todo in filteredTodos"
          :key="todo.id"
          :todo="todo"
          v-on:toggle="
            todos = todos.map((t) =>
              t.id === todo.id ? { ...t, completed: !t.completed } : t
            )
          "
          v-on:update="updateTodo"
          v-on:destroy="todos = todos.filter((t) => t.id !== todo.id)"
        />
      </ul>
    </section>
    <footer v-if="hasTodos" class="footer">
      <TodoCounter :todos="todos" />
      <Filters :filter="filter" />
      <ClearCompleted
        :todos="todos"
        v-on:clear="todos = todos.filter((todo) => !todo.completed)"
      />
    </footer>
  </section>
</template>

<script>
import { Router } from "director/build/director";
import { v4 as uuid } from "uuid";
import Header from "./Header";
import Todo from "./Todo";
import ToggleAll from "./ToggleAll";
import TodoCounter from "./TodoCounter";
import Filters from "./Filters";
import ClearCompleted from "./ClearCompleted";

export default {
  components: {
    ClearCompleted,
    Filters,
    TodoCounter,
    ToggleAll,
    Header,
    Todo,
  },
  data: () => {
    return {
      filter: null,
      todos: JSON.parse(localStorage.getItem("todos")) || [],
    };
  },
  beforeMount: function () {
    const router = new Router({
      "/active": () => (this.filter = "active"),
      "/completed": () => (this.filter = "completed"),
      "/": () => (this.filter = null),
    });
    router.init();
  },
  watch: {
    todos: function () {
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
  },
  methods: {
    addTodo: function (text) {
      this.todos.push({ id: uuid(), text: text, completed: false });
    },
    updateTodo: function (updatedTodo) {
      const todoItemIndex = this.todos.findIndex(
        (todo) => todo.id === updatedTodo.id
      );
      this.todos.splice(todoItemIndex, 1, updatedTodo);
    },
    toggleAll: function (completed) {
      this.todos = this.todos.map((todo) => ({ ...todo, completed }));
    },
  },
  computed: {
    filteredTodos: function () {
      return this.filter
        ? this.todos.filter((todo) =>
            this.filter === "completed" ? todo.completed : !todo.completed
          )
        : this.todos;
    },
    hasTodos: function () {
      return this.todos.length > 0;
    },
  },
};
</script>
