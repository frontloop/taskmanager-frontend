<script setup lang="ts">
import TaskList from './components/TaskList.vue'
import TaskEditor from './components/TaskEditor.vue'
import { onMounted } from 'vue'

import { useTaskStore } from '@/stores/task';

const taskStore = useTaskStore()

onMounted(() => {
  taskStore.getAll()
})

</script>

<template>
  <div>
    <TaskList />
    <div v-if="taskStore.taskEditorOpen" class="editor">
      <TaskEditor @ontasksaved="taskStore.taskEditorOpen = false" />
    </div>
  </div>
</template>

<style scoped>
.editor {
  position: fixed; 
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(156, 174, 194, 0.9);
}

</style>
