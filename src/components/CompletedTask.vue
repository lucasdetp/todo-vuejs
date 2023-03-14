<template>
    <div>
      <button v-if="completedTasks.length > 0" @click="deleteCompletedTasks">Supprimer les tâches complétées</button>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      tasks: {
        type: Array,
        required: true,
      },
    },
    computed: {
      completedTasks() {
        return this.tasks.filter(task => task.completed);
      },
    },
    methods: {
      deleteCompletedTasks() {
        this.$emit('delete-completed-tasks'); 
      },
    },
  };
  </script>
  