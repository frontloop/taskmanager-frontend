<template>
    <NewTaskButton class="newtaskbutton" @click="taskStore.taskEditorOpen = true" />
    <div>
        <TaskRow v-for="task in taskStore.taskList" :task="task" />
    </div>
  </template>

<script setup lang="ts">
import TaskRow from '@/components/TaskRow.vue'
import NewTaskButton from '@/components/NewTaskButton.vue'
import { useTaskStore } from '@/stores/task';

const taskStore = useTaskStore()

</script>