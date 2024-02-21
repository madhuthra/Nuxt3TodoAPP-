<template>
  <div class="todo-list">
    <h1>TODO List</h1>
    <input class="new-task-input" v-model="newTask" @keyup.enter="addTask" placeholder="Enter a new task">
    <ul class="task-list">
      <TodoItem
        v-for="todo in todos"
        :key="todo.id"
        :todo="todo"
        @delete="deleteTask"
      />
    </ul>
  </div>
</template>

<style >
.todo-list {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  background-color:skyblue;
}

.new-task-input {
  width: 90%;
  padding: 10px;
  margin-bottom: 10px;
}

.task-list {
  list-style-type: none;
  padding: 0;
}

.task-list li {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px;
  background-color: #f9f9f9;
  border-radius: 5px;
  margin-bottom: 10px;
}

.task-list li button {
  background-color: #e53935;
  color: white;
  border: none;
  padding: 5px 10px;
  border-radius: 3px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.task-list li button:hover {
  background-color: #c62828;
}
</style>


<script lang="ts">
import { defineComponent } from 'vue';
import { Todo } from '~/types/todo';

export default defineComponent({
  name: 'TodoPage',
  components: {
    TodoItem: () => import('~/components/TodoItem.vue'),
  },
  data() {
    return {
      newTask: '',
      todos: [] as Todo[],
      nextId: 1,
    };
  },
  methods: {
    addTask(): void {
      if (this.newTask.trim() !== '') {
        this.todos.push({
          id: this.nextId++,
          text: this.newTask.trim(),
        });
        this.newTask = '';
      }
    },
    deleteTask(id: number): void {
      this.todos = this.todos.filter(todo => todo.id !== id);
    },
  },
});
</script>
