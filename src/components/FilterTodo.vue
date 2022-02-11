<template>
  <div class="filter">
    <div class="filter__left">
      <button
        class="filter__button filter__button--active"
        @click="$emit('allTodo')"
      >
        All ({{ allTodosLength }})
      </button>
      <button
        class="filter__button"
        @click="filter__mode = $emit('pendingTodo')"
      >
        Pending ({{ allPendingTodos }})
      </button>
      <button class="filter__button" @click="filter__mode = $emit('doneTodo')">
        Done ({{ allDoneTodos }})
      </button>
    </div>
    <div>
      <button
        class="filter__button filter__button--danger"
        @click="$emit('clear')"
      >
        Clear
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Filter Todos",
  props: {
    allTodosLength: {
      type: Number,
    },
    allPendingTodos: {
      type: Number,
    },
    allDoneTodos: {
      type: Number,
    },
  },
};
</script>
