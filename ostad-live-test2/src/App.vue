<template>
  <div>
    <TaskList :tasks="tasks" @edit-task="handleEditTask" />
    <EditTaskPopup v-if="selectedTask" :task="selectedTask" :show-popup="showPopup" @update-task="handleUpdateTask" />
  </div>
</template>

<script>
import TaskList from 'src/components/TaskList.vue';
import EditTaskPopup from 'src/components/EditTaskPopup.vue';
import { ref } from 'vue';

export default {
  components: {
    TaskList,
    EditTaskPopup,
  },
  setup() {
    const tasks = ref([
      { name: 'task 1', time: 30 },
      { name: 'task 2', time: 40 },
      { name: 'task 3', time: 60 },
      { name: 'task 4', time: 45 },
      { name: 'task 5', time: 50 },
    ]);

    const selectedTask = ref(null);
    const showPopup = ref(false);

    const handleEditTask = (task) => {
      selectedTask.value = task;
      showPopup.value = true;
    };

    const handleUpdateTask = (updatedTask) => {
      // Update the original task in the list
      const index = tasks.value.findIndex((t) => t.name === updatedTask.name);
      tasks.value[index] = updatedTask;
      showPopup.value = false;
      selectedTask.value = null;
    };

  }, 
};
</script>
