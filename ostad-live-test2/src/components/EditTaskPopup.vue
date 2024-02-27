<template>
    <div v-if="showPopup">
      <h2>Edit Task</h2>
      <form @submit.prevent="handleSubmit">
        <label for="name">Name:</label>
        <input type="text" id="name" v-model="task.name" />
        <label for="time">Time:</label>
        <input type="number" id="time" v-model.number="task.time" />
        <button type="submit">Update</button>
      </form>
    </div>
  </template>
  
  <script>
  import { ref } from 'vue';
  
  export default {
    props: ['task', 'showPopup'],
    data() {
      return {
        taskCopy: {},
      };
    },
    methods: {
      handleSubmit() { 
        this.$emit('update-task', this.taskCopy);
      },
    },
    watch: {
      task(newTask) {
        Object.assign(this.taskCopy, newTask);
      },
    },
  };
  </script>
  