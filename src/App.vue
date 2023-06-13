<script setup>
import { ref } from "vue";
const id = ref(0);
const newTask = ref("");
const tasks = ref([]);
function addTask() {
  tasks.value.push({ id: id.value++, text: newTask.value });
  newTask.value = "";
}
</script>

<template>
  <input v-model="newTask" />

  <button @click="addTask" :key="newTask.id">Add task</button>

  <li v-for="task in tasks">
    {{ task.text }}
  </li>
</template>

<style scoped></style>
