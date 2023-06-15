<script setup>
import { ref, watch } from "vue";
const id = ref(0);
const newTask = ref("");
const tasks = ref([]);

const hasError = ref(false);

function addTask() {
  tasks.value.push({ id: id.value++, text: newTask.value });
  newTask.value = "";
}
function deleteTask(taskId) {
  // tasks.value = tasks.value.filter((t) => t.id != taskId); //creates a second array, using more memory
  tasks.value.splice(
    tasks.value.findIndex((insideTask) => insideTask.id === taskId),
    1
  ); //searches the array until it finds an id equal to task.id
}

function validateAddtask() {
  if (newTask.value == "") {
    hasError.value = true;
  } else {
    addTask();
    hasError.value = false;
  }
}
watch(newTask, (value) => {
  //value = newTask
  if (value != "") {
    hasError.value = false;
  }
});
function editTask(task) {
  console.log(task);
}
</script>

<template>
  <div class="flex flex-col justify-center items-center">
    <div id="input-container" class="flex justify-center pt-10">
      <input
        class="border-black border-2 pr-2 rounded-full"
        :class="{ 'border-red-500': hasError }"
        v-model="newTask"
      />
      <button
        class="bg-green-600 hover:bg-green-900 text-white font-bold py-2 px-4 rounded-full"
        @click="validateAddtask"
        :key="newTask.id"
      >
        Add task
      </button>
    </div>

    <div
      id="main"
      class="flex flex-col justify-center items-center pt-20 w-screen h-full"
    >
      <div id="list-container" class="mx-auto space-y-5 list-none w-1/2">
        <li
          class="bg-green-900 flex justify-center items-center"
          v-for="task in tasks"
          :key="task.id"
        >
          <input type="checkbox" v-model="task.done" />
          <span
            class="flex-grow text-center text-white"
            contenteditable="false"
            :class="{ done: task.done }"
          >
            {{ task.text }}
          </span>
          <button
            class="border-2 border-white ml-7 mr-2 text-white"
            @click="deleteTask(task.id)"
          >
            X
          </button>
          <button
            class="text-white border-2 border-white"
            @click="editTask(task.text)"
          >
            EDIT
          </button>
        </li>
      </div>
    </div>
  </div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
