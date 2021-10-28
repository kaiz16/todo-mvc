<template>
  <p
    v-on:dblclick="$emit('editTodo')"
    v-bind:class="{ 'is-completed': todo.is_completed === true }"
  >
    {{ todo.content }}
  </p>
  <button v-if="todo.is_completed === false" @click="$emit('completeTodo')">
    Completed
  </button>
  <button v-else @click="$emit('unmarkTodo')">Undo</button>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style>
.is-completed {
  text-decoration: line-through;
  color: green;
}
</style>
