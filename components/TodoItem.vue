<template>
  <li>
    {{ todo.text }}
    <button @click="deleteTodo">Delete</button>
  </li>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { Todo } from '~/types/todo';

export default defineComponent({
  props: {
    todo: {
      type: Object as () => Todo,
      required: true,
    },
  },
  methods: {
    deleteTodo(): void {
      this.$emit('delete', this.todo.id);
    },
  },
});
</script>
