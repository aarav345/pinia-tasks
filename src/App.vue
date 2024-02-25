<template>
  <div>

    <header>
      <img src="./assets/pinia-logo.svg" alt="Pinia logo">
      <h1>Pinia tasks</h1>
      
    </header>

    <div class="new-task-form">
      <TaskForm />
    </div>

    <nav class="filter">
      <button @click="filter = 'all'">All tasks</button>
      <button @click="filter = 'favs'">Fav tasks</button>

    </nav>

    <div class="loading" v-if="loading">
      Loading tasks...
    </div>

    <div class="task-list" v-if="filter === 'all'">
      <p>You have {{ totalCount }} task left to do</p>
      <div v-for="task in tasks">
        <TaskDetails :task = "task" />
      </div>
    </div>

    <div class="task-list" v-if="filter === 'favs'">
      <p>You have {{ favCount }} task left to do</p>
      <div v-for="task in favs">
        <TaskDetails :task = "task" />
      </div>
    </div>

    <button @click="taskstore.$reset">reset state</button>

  </div>
</template>

<script setup>

import {useTaskStore} from './stores/TaskStore'
import TaskDetails from  './components/TaskDetails.vue'
import { ref } from 'vue';
import TaskForm from './components/TaskForm.vue';
import { storeToRefs } from 'pinia';



const taskstore = useTaskStore()

const { tasks, loading, favs, totalCount, favCount} = storeToRefs(taskstore)

taskstore.getTasks()

const filter = ref('all')
  
</script>