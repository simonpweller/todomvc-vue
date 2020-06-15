<template>
  <div id="app">
    <TodoList />
    <InfoFooter />
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue'
import InfoFooter from './components/InfoFooter'

export default {
  name: 'App',
  components: {
    TodoList: TodoList,
    InfoFooter: InfoFooter,
  }
}
</script>