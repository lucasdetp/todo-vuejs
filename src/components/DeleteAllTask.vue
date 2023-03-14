<template>
    <button v-if="tasks.length > 0" @click="deleteAllTasks">Supprimer toutes les tâches</button>
  </template>
  
  <script>
  export default {
    props: {
      tasks: {
        type: Array,
        required: true
      }
    },
    methods: {
      deleteAllTasks() {
        this.$emit('delete-all');
      },
    }
  }
  </script>
  