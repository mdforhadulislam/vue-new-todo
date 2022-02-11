<template>
  <!-- Todo start -->
  <div
    class="todo"
    :class="{
      'todo--done': todo.status,
    }"
    @click="$emit('changStatus', todo)"
  >
    <div class="todo__status-dot"></div>
    <div>
      <p class="todo__content">{{ todo.task }}</p>
      <small class="todo__time">
        {{ new Date(todo.time).toLocaleTimeString() }}
        {{ new Date(todo.time).toLocaleDateString() }}
      </small>
    </div>
  </div>
  <!-- Todo end -->
</template>

<script>
export default {
  name: "Todo",
  props: ["todo"],
};
</script>
