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
  <div id="input-container" class="flex justify-center h-100 pt-10">
    <input
      class="border-black border-2 outline-red-500 pr-2 rounded-full"
      v-model="newTask"
    />
    <button
      class="bg-green-600 hove r:bg-green-900 text-white font-bold py-2 px-4 rounded-full"
      @click="validateAddtask"
      :key="newTask.id"
    >
      Add task
    </button>
  </div>
  <div class="pt-20 w-screen h-10">
    <li
      class="mx-auto mb-5 block list-none bg-green-900 h-10 w-1/2"
      v-for="task in tasks"
      :key="task.id"
    >
      <input type="checkbox" v-model="task.done" />
      <span :class="{ done: task.done }">{{ task.text }}</span>
      <button class="border-2 border-black ml-7" @click="deleteTask(task)">
        X
      </button>
    </li>
  </div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
