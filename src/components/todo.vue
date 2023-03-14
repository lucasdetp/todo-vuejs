<template>
    <div>
      <h2>To Do List ({{ tasks.length }})</h2>
      <p>Il vous reste {{ remainingTasks }} tâches à faire.</p>
      <form @submit.prevent="addTask">
        <input type="text" v-model="newTask" placeholder="Ajouter une tâche...">
        <button>+</button>
      </form>
      <TaskList :tasks="tasks" @delete-task="deleteTask" @update-task="updateTask" />
      <DeleteAllTask :tasks="tasks" :completed-tasks="completedTasks" @delete-all="deleteAllTasks" @delete-completed="deleteCompletedTasks" />
      <CompletedTask :tasks="tasks" @delete-completed-tasks="deleteCompletedTasks" />
    </div>
  </template>
  
  <script>
  import TaskList from './TaskList.vue';
  import DeleteAllTask from './DeleteAllTask.vue';
  import CompletedTask from './CompletedTask.vue';
  
  export default {
    components: {
      TaskList,
      DeleteAllTask,
      CompletedTask,
    },
    data() {
      return {
        tasks: [
          { name: 'Aller chez le coiffeur', completed: true, editing: false },
          { name: 'Déposer le projet sur github', completed: false, editing: false },
        ],
        newTask: '',
      };
    },
    computed: {
      completedTasks() {
        return this.tasks.filter(task => task.completed);
      },
      remainingTasks() {
        return this.tasks.filter(task => !task.completed).length;
      },
    },
    methods: {
      addTask() {
        if (this.newTask) {
          this.tasks.push({ name: this.newTask, completed: false, editing: false });
          this.newTask = '';
        }
      },
      deleteTask(index) {
        this.tasks.splice(index, 1);
      },
      deleteAllTasks() {
        this.tasks = [];
      },
      deleteCompletedTasks() {
        this.tasks = this.tasks.filter(task => !task.completed);
      },
      updateTask(task) {
        task.editing = false;
      },
    },
  };
  </script>
  
  <style>
  input{
    padding: 10px;
  }
  h2{
    background-color: #68C3A3;
  }
  ul {
    list-style-type: none;
    padding: 0;
    margin: 0;
  }
  button{
    margin: 10px;
  }
  li{
    text-align: left;
  }
  </style>
  