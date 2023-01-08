<template>
  <form @submit.prevent="handleSubmit">
    <input 
      type="text" 
      placeholder="Jag behöver göra..."
      v-model="newTask">
    <button>Lägg till</button>
  </form>
</template>

<script>
import { ref } from 'vue';
import { useTaskStore } from '../Stores/TaskStore'

  export default {
    setup() {
      const taskStore = useTaskStore(); 

      const newTask = ref('')

      const handleSubmit = () => {
        if(newTask.value.length > 0){
          taskStore.addTask({
            title: newTask.value, 
            isFave: false,
            id: Math.floor(Math.random() * 10000)
          })
          newTask.value = ''
        }
      }

      return {handleSubmit, newTask}
    }
  }
</script>

