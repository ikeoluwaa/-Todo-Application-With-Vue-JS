<template>
  <div>
    <h2>Add Todo</h2>
    <form @submit.prevent="addNewTodo" class="add-form">
      <div class="input-container">
        <input
          v-model="newTodo"
          type="text"
          placeholder="Add Task"
          required
          class="add-item-input"
        />
        <button type="submit" class="add-button">
          <font-awesome-icon
            :icon="['fas', 'circle-plus']"
            size="2xl"
            style="color: #5c677d"
          />
        </button>
      </div>
    </form>
    <p class="current-date">{{ getCurrentDate() }}</p>
  </div>
</template>

<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";

export default {
  components: {
    FontAwesomeIcon,
  },
  data() {
    return {
      newTodo: "",
    };
  },
  methods: {
    addNewTodo() {
      if (this.newTodo.trim() !== "") {
        this.$emit("addTodo", {
          id: Date.now(),
          text: this.newTodo.trim(),
          completed: false,
        });

        this.newTodo = "";
      }
    },
    getCurrentDate() {
      const options = {
        weekday: "long",
        year: "numeric",
        month: "long",
        day: "numeric",
      };
      const currentDate = new Date().toLocaleDateString("en-US", options);
      return currentDate;
    },
  },
};
</script>

<style>
.add-form {
  text-align: center;
}

.input-container {
  display: flex;
}

.add-item-input {
  width: 80%;
  height: 2rem;
  border-radius: 10px;
  border: none;
  padding: 5px;
  background-color: #c8b6ff;
  color: #fff;
  transition: border-color 0.3s ease;
}
.add-item-input:focus {
  outline: none;
  border-color: transparent;
}

.add-item-input::placeholder {
  font-size: 16px;
  color: #5c677d;
  padding: 4px;
}

.add-button {
  border: none;
  color: #fff;
  cursor: pointer;
  background: none;
}

.current-date {
  text-align: center;
  margin-top: 10px;
  color: #7d8597;
}

h2 {
  color: #5c677d;
  font-size: 18px;
  font-style: italic;
}

@media screen and (max-width: 600px) {
  .add-item-input {
    width: 100%;
  }

  .add-button {
    top: 0;
    right: 0;
    transform: translate(0, 0);
  }
}
</style>
