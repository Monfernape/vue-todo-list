<template>
  <div>
    <TodoForm
      :editItem="editTodoItem"
      @add-todo="addTodo"
      @update-todo="updateTodoTitle"
    />
    <TodoList
      v-if="todos.length > 0"
      :todos="todos"
      @update-todo-status="updateTodoStatus"
      @delete-todo="deleteTodo"
      @edit-todo="editTodo"
    />
  </div>
</template>

<script>
import TodoForm from "./components/TodoForm";
import TodoList from "./components/TodoList";

export default {
  name: "App",
  data: function () {
    return {
      todos: localStorage.getItem("todos")
        ? JSON.parse(localStorage.getItem("todos"))
        : [],
      editTodoItem: null,
    };
  },
  components: {
    TodoForm,
    TodoList,
  },
  watch: {
    todos: function (a) {
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
  },
  methods: {
    addTodo(todo) {
      this.todos = [
        ...this.todos,
        { title: todo, completed: false, id: Date.now() },
      ];
    },
    updateTodoTitle(title) {
      this.todos = this.todos.map((x) =>
        x.id === this.editTodoItem.id ? { ...this.editTodoItem, title } : x
      );
    },
    updateTodoStatus({ id, status: completed }) {
      this.todos = this.todos.map((x) =>
        x.id === id ? { ...x, completed } : x
      );
    },
    deleteTodo(id) {
      this.todos = this.todos.filter((x) => x.id !== id);
    },
    editTodo(id) {
      this.editTodoItem = this.todos.find((x) => x.id === id);
    },
  },
};
</script>

<style>
</style>
