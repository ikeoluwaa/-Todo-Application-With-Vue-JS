<template>
  <div class="app-container">
    <h1>Todo List</h1>

    <AddTodo @addTodo="addTodo" />

    <TodoList
      :todos="todos"
      @updateTodos="updateTodos"
      @editTodo="editTodo"
      @toggleCompleted="toggleCompleted"
    />

    <CompletedTodos
      :completedTodos="completedTodos"
      @deleteCompletedTodo="deleteCompletedTodo"
      @toggleCompleted="toggleCompleted"
    />

    <ProgressTracker
      :completedTodos="completedTodos.length"
      :totalTodos="todos.length"
    />
  </div>
</template>

<script>
import AddTodo from "./components/AddTodo.vue";
import TodoList from "./components/TodoList.vue";
import CompletedTodos from "./components/CompletedTodos.vue";
import ProgressTracker from "./components/ProgressTracker.vue";

export default {
  data() {
    return {
      todos: [],
      completedTodos: [],
    };
  },
  methods: {
    addTodo(todo) {
      this.todos.push(todo);
    },
    updateTodos(filteredTodos) {
      this.todos = filteredTodos;
    },
    editTodo(editedTodo) {
      this.todos = this.todos.map((todo) =>
        todo.id === editedTodo.id ? editedTodo : todo
      );
    },
    toggleCompleted(todo) {
      if (todo.completed) {
        this.completedTodos.push(todo);
        this.todos = this.todos.filter((t) => t.id !== todo.id);
      } else {
        this.completedTodos = this.completedTodos.filter(
          (completedTodo) => completedTodo.id !== todo.id
        );
        this.todos.push(todo);
      }
    },
    deleteCompletedTodo(todoId) {
      this.completedTodos = this.completedTodos.filter(
        (completedTodo) => completedTodo.id !== todoId
      );
    },
  },
  components: {
    AddTodo,
    TodoList,
    CompletedTodos,
    ProgressTracker,
  },
};
</script>

<style>
body {
  background: linear-gradient(
    315deg,
    hsla(255, 100%, 86%, 1) 0%,
    hsla(255, 100%, 94%, 1) 42%,
    hsla(0, 0%, 100%, 1) 90%,
    hsla(0, 0%, 100%, 1) 98%,
    hsla(0, 0%, 99%, 1) 100%
  );

  background: -moz-linear-gradient(
    315deg,
    hsla(255, 100%, 86%, 1) 0%,
    hsla(255, 100%, 94%, 1) 42%,
    hsla(0, 0%, 100%, 1) 90%,
    hsla(0, 0%, 100%, 1) 98%,
    hsla(0, 0%, 99%, 1) 100%
  );

  background: -webkit-linear-gradient(
    315deg,
    hsla(255, 100%, 86%, 1) 0%,
    hsla(255, 100%, 94%, 1) 42%,
    hsla(0, 0%, 100%, 1) 90%,
    hsla(0, 0%, 100%, 1) 98%,
    hsla(0, 0%, 99%, 1) 100%
  );

  filter: progid: DXImageTransform.Microsoft.gradient( startColorstr="#c8b6ff", endColorstr="#E7DFFF", GradientType=1 );
}
.app-container {
  margin: 0 auto;
  max-width: 22rem;
  height: 90vh;
  overflow-y: auto;
  padding: 20px;
  font-family: "Arial", sans-serif;
  background-color: #fff;
  box-shadow: rgba(0, 0, 0, 0.4) 0px 30px 90px;
  border-radius: 1.8rem;
  margin-top: 0.5rem;
}

h1 {
  margin-top: 0;
  text-align: right;
  color: #5c677d;
  font-size: 1.3rem;
}
@media screen and (max-width: 600px) {
  .app-container {
    max-width: 100%;
  }

  h1 {
    text-align: center;
  }
}
</style>
