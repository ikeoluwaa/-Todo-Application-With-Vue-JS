<template>
  <div class="todo-container">
    <h2>To do</h2>
    <div v-if="todos.length === 0" class="no-todos-message">
      No todos available. Add some tasks!
    </div>
    <ul v-else>
      <TodoItem
        v-for="todo in todos"
        :key="todo.id"
        :todo="todo"
        @edit="editTodoItem"
        @delete="deleteTodoItem"
        @toggleCompleted="toggleCompleted"
        class="todo-list"
      />
    </ul>
  </div>
</template>

<script>
import TodoItem from "./TodoItem.vue";
import Swal from "sweetalert2";

export default {
  props: {
    todos: Array,
  },
  components: {
    TodoItem,
  },
  methods: {
    async editTodoItem(todo) {
      const { value: updatedText } = await Swal.fire({
        title: "Edit Todo",
        input: "text",
        inputValue: todo.text,
        showCancelButton: true,
        confirmButtonText: "Save",
      });

      if (updatedText && updatedText.trim() !== todo.text) {
        // Update the todo directly for reactivity in Vue 3
        todo.text = updatedText.trim();
      }
    },
    async deleteTodoItem(todoId) {
      const result = await Swal.fire({
        title: "Delete Todo",
        text: "Are you sure you want to delete this todo?",
        icon: "warning",
        showCancelButton: true,
        confirmButtonColor: "#d33",
        cancelButtonColor: "#C8B6FF",
        confirmButtonText: "Delete",
      });

      if (result.isConfirmed) {
        const filteredTodos = this.todos.filter((todo) => todo.id !== todoId);
        this.$emit("updateTodos", filteredTodos);
      }
    },
    toggleCompleted(todo) {
      this.$emit("toggleCompleted", todo);
    },
  },
};
</script>
<style scoped>
.todo-container {
  max-width: 100%;
  height: 35%;
  overflow-y: auto;
}
.todo-list {
  margin-bottom: 0.8rem;
  padding: 0.6rem;
  border: 0.1px solid #ccc;
  border-radius: 0.45rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  overflow-y: auto;
}
</style>
<style scoped>
h2 {
  color: #333;
  margin-bottom: 0.6rem;
}

ul {
  list-style-type: none;
  padding: 0;
}

/* Style for each todo item */
.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border: 1px solid #ccc;
  border-radius: 5px;
  padding: 10px;
  margin-bottom: 10px;
  background-color: #fff;
}

.completed-checkbox {
  margin-right: 10px;
}

.no-todos-message {
  color: #888;
  font-style: italic;
  margin-top: 10px;
}
.line-through {
  text-decoration: line-through;
}

.edit-button,
.delete-button {
  padding: 5px 10px;
  cursor: pointer;
  border: none;
  border-radius: 3px;
  background-color: #4caf50; /* Green */
  color: white;
  margin-right: 5px;
}

.edit-button:hover,
.delete-button:hover {
  background-color: #45a049;
}

.delete-button {
  background-color: #f44336; /* Red */
}

.delete-button:hover {
  background-color: #d32f2f;
}
h2 {
  border-top: 1px solid #c8b6ff;
  color: #5c677d;
  font-size: 16px;
  padding-top: 5px;
  margin-top: 0;
  text-transform: uppercase;
  font-style: normal;
}
</style>
