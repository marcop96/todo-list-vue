<script setup>
import { ref } from "vue";

const props = defineProps(["task"]);
const emit = defineEmits(["delete", "edit"]);
const isCompleted = ref(false);
</script>

<template>
  <li class="bg-green-900 flex justify-center items-center" :key="task.id">
    <input type="checkbox" v-model="isCompleted" />

    <span
      class="flex-grow text-center text-white"
      contenteditable="false"
      :class="{ done: isCompleted }"
    >
      {{ task.text }}
    </span>
    <button
      class="border-2 border-white ml-7 mr-2 text-white"
      @click="$emit('delete', task.id)"
    >
      X
    </button>
    <button
      class="text-white border-2 border-white"
      @click="$emit('edit', task.text)"
    >
      EDIT
    </button>
  </li>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
