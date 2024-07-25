<template>
  <form @submit.prevent="handleSubmit" class="mb-4 flex">
    <input
      v-model="taskTitle"
      type="text"
      placeholder="Add a new task"
      class="flex-1 border rounded-l px-4 py-2 focus:outline-none focus:ring-2 focus:ring-blue-400"
      required
    />
    <button
      type="submit"
      class="bg-blue-500 text-white px-6 py-2 rounded-r hover:bg-blue-600 transition-colors"
    >
      Add Task
    </button>
  </form>
</template>

<script>
import { ref } from "vue";

export default {
  emits: ["add-task"],
  setup(_, { emit }) {
    const taskTitle = ref("");

    const handleSubmit = () => {
      if (taskTitle.value.trim() !== "") {
        emit("add-task", { title: taskTitle.value, completed: false });
        taskTitle.value = "";
      }
    };

    return {
      taskTitle,
      handleSubmit,
    };
  },
};
</script>
