<template>
  <form @submit="$emit('addTask', $event)">
    <input
      type="text"
      placeholder="Type and hit enter..."
      class="composer__input"
      :value="modelValue"
      @change="$emit('typeing', $event)"
    />
  </form>
</template>

<script>
export default {
  name: "Todo From",
  props: ["modelValue"],
};
</script>
