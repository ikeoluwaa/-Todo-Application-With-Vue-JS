<template>
  <div class="completed-container">
    <h2>Completed</h2>
    <ul>
      <li v-for="todo in completedTodos" :key="todo.id" class="completed-todo">
        <div>
          <input
            type="checkbox"
            v-model="todo.completed"
            class="completed-checkbox round"
            @change="toggleCompleted(todo)"
          />
          <span :class="{ 'line-through': todo.completed }">{{
            todo.text
          }}</span>
        </div>
        <div>
          <button
            @click="showDeleteConfirmation(todo.id)"
            class="delete-button"
          >
            <font-awesome-icon
              icon="trash"
              flip
              size="xl"
              style="color: #c8beff"
            />
          </button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
import Swal from "sweetalert2";

export default {
  props: {
    completedTodos: Array,
  },
  methods: {
    async showDeleteConfirmation(todoId) {
      const result = await Swal.fire({
        title: "Delete Completed Todo",
        text: "Are you sure you want to delete this completed todo?",
        icon: "warning",
        showCancelButton: true,
        confirmButtonColor: "#d33",
        cancelButtonColor: "#C8B6FF",
        confirmButtonText: "Delete",
      });

      if (result.isConfirmed) {
        this.$emit("deleteCompletedTodo", todoId);
      }
    },
    toggleCompleted(todo) {
      this.$emit("toggleCompleted", todo);
    },
  },
};
</script>

<style scoped>
.completed-container {
  max-width: 100%;
  height: 30%;
  overflow-y: auto;
}
.completed-todo {
  margin-bottom: 10px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #c8b6ff;
  overflow-y: auto;
  box-shadow: 0px 1px 2px 0px rgba(189, 16, 224, 1),
    0px 2px 4px 0px rgba(0, 0, 0, 0.07), 0px 4px 8px 0px rgba(0, 0, 0, 0.07),
    0px 8px 16px 0px rgba(0, 0, 0, 0.07), 0px 16px 32px 0px rgba(0, 0, 0, 0.07),
    0px 32px 64px 0px rgba(0, 0, 0, 0.07);
}

.completed-checkbox {
  margin-right: 10px;
}

.line-through {
  text-decoration: line-through;
}

.delete-button {
  color: red;
  margin-left: 10px;
  cursor: pointer;
}
h2 {
  /* border-top: 1px solid #c8b6ff; */
  color: #5c677d;
  font-size: 16px;
  padding-top: 5px;
  text-transform: uppercase;
  font-style: normal;
}

@media screen and (max-width: 600px) {
  .completed-todo {
    flex-direction: column;
    gap: 1px;
  }

  .completed-checkbox {
    margin-right: 0; /* Remove margin for smaller screens */
    margin-bottom: 5px; /* Add some space between checkbox and text */
  }

  .delete-button {
    margin-top: 5px; /* Add some space above the delete button */
  }
}
</style>
