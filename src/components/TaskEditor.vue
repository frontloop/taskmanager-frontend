<template>
    <div class="surface">
        <p class="fieldLabel">Name</p>
        <input v-model="taskStore.editedDask.name" placeholder="edit me" class="name-input" />
        <p>
            <label class="fieldLabel">Done:</label>
            <input type="checkbox" v-model="taskStore.editedDask.done">
        </p>
        <div>
            <label class="fieldLabel">Priority: </label>
            <input type="radio" name="priority" id="priority_low" value="LOW" style="accent-color: green;" v-model="taskStore.editedDask.priority">
            <label for="one">Low</label>
            <input type="radio" name="priority" id="priority_normal" value="NORMAL" style="accent-color: blue;" v-model="taskStore.editedDask.priority">
            <label for="one">Normal</label>
            <input type="radio" name="priority" id="priority_urgent" value="URGENT" style="accent-color: red;" v-model="taskStore.editedDask.priority">
            <label for="one">Urgent</label>
        </div>
        <p class="buttons">
            <button @click="save">save</button>
            <button @click="cancel">cancel</button>
        </p>
    </div>
</template>

<script setup lang="ts">
import { useTaskStore } from '@/stores/task';

const taskStore = useTaskStore()

const emit = defineEmits(['ontasksaved'])

const save = async () => {
    if (taskStore.editedDask.id > -1) {
        await taskStore.save();
    } else {
        await taskStore.create()
    }
    emit('ontasksaved')
}

const cancel = () => {
    taskStore.resetEditedTask()
    taskStore.taskEditorOpen = false
}
</script>

<style scoped>
.surface {
    position: absolute;
    background-color: #bdd8df;
    border-radius: 15px;
    border: 3px solid #7b8b96;
    padding: 20px;
    top: 300px;
    left: 33%;
}

.surface div {
    color: rgb(51, 53, 55);
}

.fieldLabel {
    font-family: Arial, Helvetica, sans-serif;
    font-weight: bold;
    color: #595a5c;
    margin-bottom: 2px;
}

label {
    font-family: Arial, Helvetica, sans-serif;
    color: #595a5c;
}

.buttons {
  display: flex;
  padding-left: 30%;
  gap: 40px;
  width: 100%;
}

.name-input {
    width: 400px;
}
</style>