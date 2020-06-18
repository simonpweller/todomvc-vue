<template>
  <ul class="filters">
    <li>
      <a :class="{ selected: !filter }" href="#/">All</a>
    </li>
    <li>
      <a :class="{ selected: filter === 'active' }" href="#/active">Active</a>
    </li>
    <li>
      <a :class="{ selected: filter === 'completed' }" href="#/completed"
        >Completed</a
      >
    </li>
  </ul>
</template>

<script>
export default {
  props: {
    filter: String,
  },
};
</script>
