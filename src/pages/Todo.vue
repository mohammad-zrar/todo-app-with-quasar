<template>
  <q-page class="q-pa-md">
    <q-list separator bordered class="bg-white">
      <q-item
        v-for="task in tasks"
        @click="task.done = !task.done"
        v-ripple
        :key="task.title"
        clickable
      >
        <q-item-section avatar>
          <q-checkbox v-model="task.done" color="primary" />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{ task.title }}</q-item-label>
        </q-item-section>
      </q-item>
    </q-list></q-page
  >
</template>

<script setup lang="ts">
import { ref } from "vue";

interface Task {
  title: string;
  done: boolean;
}

const tasks = ref<Task[]>([
  { title: "First of all just do it", done: false },
  { title: "Second of all do it again", done: false },
]);
</script>
