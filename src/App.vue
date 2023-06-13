<script setup>
import { ref } from "vue";
const id = ref(0);
const newTask = ref("");
const tasks = ref([]);
function addTask() {
  tasks.value.push({ id: id.value++, text: newTask.value });
  newTask.value = "";
}
function deleteTask(task) {
  tasks.value = tasks.value.filter((t) => t != task);
  console.log("delete task");
}
</script>

<template>
  <input v-model="newTask" />

  <button @click="addTask" :key="newTask.id">Add task</button>

  <li v-for="task in tasks">
    {{ task.text }} <button @click="deleteTask(task)">X</button>
  </li>
</template>

<style scoped></style>
