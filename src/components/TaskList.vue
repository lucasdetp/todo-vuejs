<template>
    <p>Il vous reste {{ remainingTasks }} tâches à faire.</p>
    
    <div>
      <ul>
        <li v-for="(task, index) in tasks" :key="index">
          <div v-if="!task.editing">
            <input type="checkbox" :checked="task.completed" @change="updateTaskStatus(task)">
            {{ task.name }}
            <button @click="editTask(index)">Modifier</button>
            <button @click="deleteTask(index)">Supprimer</button>
          </div>
          <div v-else>
            <input type="text" v-model="task.name" @keyup.enter="updateTask(task)">
            <button @click="updateTask(task)">Sauvegarder</button>
          </div>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    props: {
        tasks: {
            type: Array,
            default: () => []
        }
    },
    computed: {
        remainingTasks() {
            return this.tasks.filter(task => !task.completed).length;
        }
    },
    methods: {
        editTask(index) {
            this.tasks[index].editing = true;
        },
        updateTask(task) {
            task.editing = false;
        },
        deleteTask(index) {
            this.tasks.splice(index, 1);
        },
        updateTaskStatus(task) {
            task.completed = !task.completed;
        }
    }
};
  </script>
  
  <style>
  ul {
    list-style-type: none;
    padding: 0;
    margin: 0;
  }
  </style>
  