<template>
  <li class="todo-item" v-show="localTodo">
    <div class="flex-container">
      <input
        type="checkbox"
        v-model="localTodo.completed"
        class="completed-checkbox round"
        @change="toggleCompleted"
      />
      <span :class="{ 'line-through': localTodo.completed }" class="todo-text">
        {{ localTodo.text }}
      </span>
    </div>
    <div>
      <button @click="edit" class="edit-button">
        <font-awesome-icon
          :icon="['fas', 'pencil-alt']"
          flip
          size="xl"
          style="color: #c8beff"
        />
      </button>
      <button @click="deleteItem" class="delete-button">
        <font-awesome-icon icon="trash" flip size="xl" style="color: #c8beff" />
      </button>
    </div>
  </li>
</template>

<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";

export default {
  props: {
    todo: Object,
  },
  components: {
    FontAwesomeIcon,
  },
  data() {
    return {
      localTodo: { ...this.todo },
    };
  },
  watch: {
    todo(newTodo) {
      this.localTodo = { ...newTodo };
    },
  },
  methods: {
    edit() {
      this.$emit("edit", this.localTodo);
    },
    deleteItem() {
      this.$emit("delete", this.localTodo.id);
    },
    toggleCompleted() {
      this.$emit("toggleCompleted", this.localTodo);
    },
  },
};
</script>

<style scoped>
.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 10px;
  padding: 5px;
  border: 1px solid #c8b6ff;
  border-radius: 5px;
  white-space: normal;
  word-wrap: break-word;
  overflow: auto;
  box-shadow: 0px 1px 2px 0px rgba(189, 16, 224, 1),
    0px 2px 4px 0px rgba(0, 0, 0, 0.07), 0px 4px 8px 0px rgba(0, 0, 0, 0.07),
    0px 8px 16px 0px rgba(0, 0, 0, 0.07), 0px 16px 32px 0px rgba(0, 0, 0, 0.07),
    0px 32px 64px 0px rgba(0, 0, 0, 0.07);
  transition: all 0.3s ease;
  font-size: 14px;
}

@media screen and (max-width: 600px) {
  .todo-item {
    overflow: hidden; /* Hide overflow on smaller screens */
    white-space: pre-wrap; /* Enable word wrap on smaller screens */
  }
}

.flex-container {
  display: flex;
  align-items: center;
}

.completed-checkbox {
  margin-right: 10px;
  background-color: blueviolet;
}

.round {
  border-radius: 50%;
}

.line-through {
  text-decoration: line-through;
}

.todo-text {
  overflow: hidden;
}

.edit-button,
.delete-button {
  margin-left: 10px;
  cursor: pointer;
  background-color: #fff;
  border: 1px solid #c8b6ff;
}
</style>
