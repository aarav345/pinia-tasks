<template>
    <div>

        <form @submit.prevent="handleSubmit">
        <input 
        type="text"
        placeholder="I need to ..."
        v-model="newTask"
        >

        <button>add</button>
    </form>

    </div>
</template>

<script setup>
import { useTaskStore } from '@/stores/TaskStore';
import { ref } from 'vue';


const taskStore = useTaskStore()

const newTask = ref('')

const handleSubmit = () => {
    if (newTask.value.length  > 0) {
        taskStore.addTask({
            title : newTask.value,
            isFav : false,
            id: Math.ceil(Math.random() *  10000)

        })

        newTask.value = ''
    }
}
    
</script>