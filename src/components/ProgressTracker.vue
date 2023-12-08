<template>
  <div class="progress-tracker">
    <p>You Have Completed : {{ progressPercentage }}% of Your Task</p>
    <div class="progress-bar">
      <div :style="{ width: progressPercentage + '%' }"></div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    completedTodos: {
      type: Number,
      required: true,
    },
    totalTodos: {
      type: Number,
      required: true,
    },
  },
  computed: {
    progressPercentage() {
      let total = this.totalTodos + this.completedTodos;
      return total > 0 ? ((this.completedTodos / total) * 100).toFixed(0) : 0;
    },
  },
};
</script>

<style scoped>
.progress-tracker {
  text-align: center;
  margin-bottom: 0.2rem;
}

.progress-bar {
  background-color: #eee;
  height: 1.2rem;
  border-radius: 1rem;
  overflow: hidden;
  margin-bottom: 0;
}

.progress-bar div {
  height: 100%;
  background-color: #5c677d;
  border-radius: 10px;
  transition: width 0.3s ease-in-out;
}

@media screen and (max-width: 600px) {
  .progress-bar {
    height: 0.8rem;

    .progress-bar div {
      border-radius: 8px;
    }
  }
}
</style>
