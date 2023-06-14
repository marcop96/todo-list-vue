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
}
function validateAddtask() {
  if (newTask.value == "") {
    console.log("input vacio");
  } else {
    addTask();
  }
}
</script>

<template>
  <input v-model="newTask" :class="error" />
  <button @click="validateAddtask" :key="newTask.id">Add task</button>
  <li v-for="task in tasks" :key="task.id">
    <input type="checkbox" v-model="task.done" />
    <span :class="{ done: task.done }">{{ task.text }}</span>
    <button @click="deleteTask(task)">X</button>
  </li>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
