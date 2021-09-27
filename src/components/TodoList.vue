<template>
  <ul>
    <li v-for="todo in todos" :key="todo.id">
      <input
        type="checkbox"
        :checked="todo.completed"
        @change="updateTodoStatus($event, todo.id)"
      />
      {{ todo.title }}
      <button @click="deleteTodo(todo.id)">Delete</button>
      <button @click="editTodo(todo.id)">Edit</button>
    </li>
  </ul>
</template>

<script>
export default {
  name: "TodoList",
  props: {
    todos: Array,
  },
  methods: {
    updateTodoStatus(event, id) {
      this.$emit("update-todo-status", { id, status: event.target.checked });
    },
    deleteTodo(id) {
      this.$emit("delete-todo", id);
    },
    editTodo(id) {
      this.$emit("edit-todo", id);
    },
  },
};
</script>