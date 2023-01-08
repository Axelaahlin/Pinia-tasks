<template>
  <main>
    <header>
      <img src="./assets/pinia_logo.svg" alt="pinia logo">
      <h1>Pinia Tasks</h1>
    </header>

    <div class="new-task-form">
      <Taskform/>
    </div>

    <nav class="filter">
      <button @click="filter ='all'">Alla tasks</button>
      <button @click="filter = 'favs'">Favorit tasks</button>
    </nav>

    <div 
      class="loading"
      v-if="taskStore.isLoading"
    >
      laddar tasks...
    </div>

    <div class="task-list" v-if="filter === 'all'">
      <p>Du har {{ taskStore.totalCount }} saker att göra</p>
      <div v-for="task in taskStore.tasks" :key="task.id">
        <TaskDetails :task="task"/>
      </div>
    </div>

    <div class="task-list" v-if="filter === 'favs'">
      <p>Du har {{ taskStore.favCount }} favoritsaker att göra</p> 
      <div v-for="task in taskStore.favs" :key="task.id">
        <TaskDetails :task="task"/>
      </div>
    </div>

    <button @click="taskStore.$reset">Börja om</button>
  </main>
</template>

<script>
import { ref } from 'vue'
import TaskDetails from './components/TaskDetails.vue'
import Taskform from './components/Taskform.vue'
import {useTaskStore} from './Stores/TaskStore'

export default {
  components: { TaskDetails, Taskform },
  setup() {
    const taskStore = useTaskStore()

    taskStore.getTasks()

    const filter = ref('all')

    return { taskStore, filter }
  }
}
</script>

