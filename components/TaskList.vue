<template>
  <ul>
    <li
      v-for="(task, index) in tasks"
      :key="index"
      class="flex items-center justify-between p-4 border-b hover:bg-gray-50 transition-colors"
    >
      <div class="flex items-center">
        <input
          type="checkbox"
          v-model="task.completed"
          class="mr-2 h-5 w-5 text-blue-600 focus:ring-blue-500"
        />
        <span
          :class="{
            'line-through text-gray-500': task.completed,
            'text-gray-800': !task.completed,
          }"
          >{{ task.title }}</span
        >
      </div>
      <div>
        <button
          @click="editTask(index)"
          class="text-blue-500 mr-2 hover:text-blue-600 transition-colors"
        >
          Edit
        </button>
        <button
          @click="removeTask(index)"
          class="text-red-500 hover:text-red-600 transition-colors"
        >
          Delete
        </button>
      </div>
    </li>
  </ul>
</template>

<script>
export default {
  props: {
    tasks: {
      type: Array,
      required: true,
    },
  },
  emits: ["remove-task", "update-task"],
  methods: {
    removeTask(index) {
      this.$emit("remove-task", index);
    },
    editTask(index) {
      const newTitle = prompt("Edit task title:", this.tasks[index].title);
      if (newTitle !== null) {
        this.$emit("update-task", {
          index,
          task: { ...this.tasks[index], title: newTitle },
        });
      }
    },
  },
};
</script>

<style>
.line-through {
  text-decoration: line-through;
}
</style>
