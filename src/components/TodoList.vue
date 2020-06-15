<template>
  <section class="todoapp">
    <header class="header">
      <h1>todos</h1>
      <input class="new-todo" placeholder="What needs to be done?" autofocus />
    </header>
    <section v-if="hasTodos" class="main">
      <input id="toggle-all" class="toggle-all" type="checkbox" />
      <label for="toggle-all">Mark all as complete</label>
      <ul class="todo-list">
        <Todo v-for="todo in todos" :key="todo.id" />
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
    };
  },
  computed: {
    hasTodos: function () {
      return this.todos.length > 0;
    },
  },
};
</script>
