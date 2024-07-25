<template>
  <div class="min-h-screen bg-gray-100 py-10">
    <div class="container mx-auto p-4 bg-white shadow-lg rounded-lg">
      <h1 class="text-center text-4xl font-extrabold text-blue-600 mb-6">
        To-Do List
      </h1>
      <TaskForm @add-task="addTask" />
      <TaskList
        :tasks="tasks"
        @remove-task="removeTask"
        @update-task="updateTask"
      />
    </div>
  </div>
</template>

<script>
import TaskForm from "@/components/TaskForm.vue";
import TaskList from "@/components/TaskList.vue";

export default {
  components: {
    TaskForm,
    TaskList,
  },
  data() {
    return {
      tasks: [],
    };
  },
  mounted() {
    if (process.client) {
      this.tasks = JSON.parse(localStorage.getItem("tasks")) || [];
    }
  },
  watch: {
    tasks: {
      handler(tasks) {
        if (process.client) {
          localStorage.setItem("tasks", JSON.stringify(tasks));
        }
      },
      deep: true,
    },
  },
  methods: {
    addTask(task) {
      this.tasks.push(task);
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
    },
    updateTask({ index, task }) {
      this.$set(this.tasks, index, task);
    },
  },
};
</script>
