<template>
  <div class="filter">
    <div class="filter__left">
      <button
        class="filter__button"
        :class="{
          'filter__button--active': all,
        }"
        @click="
          $emit('allTodo');
          all = true;
          done = false;
          pending = false;
        "
      >
        All ({{ allTodosLength }})
      </button>
      <button
        class="filter__button"
        :class="{
          'filter__button--active': pending,
        }"
        @click="
          filter__mode = $emit('pendingTodo');
          all = false;
          done = false;
          pending = true;
        "
      >
        Pending ({{ allPendingTodos }})
      </button>
      <button
        class="filter__button"
        :class="{
          'filter__button--active': done,
        }"
        @click="
          filter__mode = $emit('doneTodo');
          all = false;
          done = true;
          pending = false;
        "
      >
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
  data() {
    return {
      all: true,
      pending: false,
      done: false,
    };
  },
};
</script>
