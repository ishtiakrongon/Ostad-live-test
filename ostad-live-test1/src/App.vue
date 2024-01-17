<template>
  <div>
    <div v-for="task in tasks" :key="task.name">
      {{ task.name }} - {{ task.time }} minutes
      <button @click="editTask(task)">Edit</button>
    </div>

    <div v-if="selectedTask">
      <h2>Edit Task</h2>
      <form @submit.prevent="updateTask">
        <label for="name">Name:</label>
        <input type="text" id="name" v-model="selectedTask.name" />
        <label for="time">Time:</label>
        <input type="number" id="time" v-model.number="selectedTask.time" />
        <button type="submit">Update</button>
      </form>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const tasks = ref([
      { name: 'Task 1', time: 30 },
      { name: 'Task 2', time: 40 },
      { name: 'Task 3', time: 60 },
      { name: 'Task 4', time: 45 },
      { name: 'Task 5', time: 50 },
    ]);

    const selectedTask = ref(null);

    const editTask = (task) => {
      selectedTask.value = task;
    };

    const updateTask = () => {
      const index = tasks.value.findIndex((t) => t.name === selectedTask.value.name);
      tasks.value[index] = selectedTask.value;
      selectedTask.value = null;
    };

    return {
      tasks,
      selectedTask,
      editTask,
      updateTask,
    };
  },
};
</script>

