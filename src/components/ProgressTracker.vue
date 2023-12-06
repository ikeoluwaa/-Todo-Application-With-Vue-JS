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
  margin-bottom: 20px;
}

.progress-bar {
  background-color: #eee;
  height: 20px;
  border-radius: 10px;
  overflow: hidden;
}

.progress-bar div {
  height: 100%;
  background-color: #5c677d;
  border-radius: 10px;
  transition: width 0.3s ease-in-out;
}
</style>
