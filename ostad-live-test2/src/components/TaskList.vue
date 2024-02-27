<template>
    <div>
      <ul>
        <li v-for="task in tasks" :key="task.name">
          {{ task.name }} - {{ task.time }} minutes
          <button @click="$emit('edit-task', task)">Edit</button>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  import { ref } from 'vue';
  import EditTaskPopup from './EditTaskPopup.vue';
  
  export default {
    props: ['tasks'],
    components: {
      EditTaskPopup,
    },
    setup(props) {
      const emitEditTask = (task) => {
        props.emit('edit-task', task);
      };
  
      return {
        emitEditTask,
      };
    },
  };
  </script>
  