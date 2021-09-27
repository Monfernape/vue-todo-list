<template>
  <form @submit.prevent="handleSubmitTodo">
    <label for="input">Title</label>
    <input v-model="todo" id="input" />
    <button :type="'submit'">{{ editItem ? "Update" : "Add" }}</button>
  </form>
</template>

<script>
export default {
  name: "TodoForm",
  props: {
    editItem: Object,
  },
  data: function () {
    return {
      todo: "",
    };
  },
  watch: {
    editItem: function () {
      this.todo = this.editItem.title;
    },
  },
  methods: {
    handleSubmitTodo() {
      if (this.editItem) this.$emit("update-todo", this.todo);
      else this.$emit("add-todo", this.todo);
      this.todo = "";
    },
  },
};
</script>