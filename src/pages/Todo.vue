<template>
  <q-page class="bg-grey-3 column">
    <div class="row q-pa-sm bg-primary">
      <q-input
        v-model="newTask"
        class="col"
        bg-color="white"
        filled
        placeholder="Add task"
        dense
      >
        <template v-slot:append>
          <q-btn @click="addTask()" round dense flat icon="add" />
        </template>
      </q-input>
    </div>
    <q-list separator bordered class="bg-white">
      <q-item
        v-for="(task, index) in tasks"
        @click="task.done = !task.done"
        v-ripple
        :key="task.title"
        clickable
        :class="{ 'done bg-blue-1': task.done }"
      >
        <q-item-section avatar>
          <q-checkbox v-model="task.done" color="primary" />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{ task.title }}</q-item-label>
        </q-item-section>
        <q-item-section v-if="task.done" side>
          <q-btn
            flat
            round
            color="primary"
            @click.stop="deleteTask(index)"
            icon="delete"
          />
        </q-item-section>
      </q-item>
    </q-list>
    <div v-if="!tasks.length" class="no-tasks absolute-center">
      <q-icon name="check" size="100px" color="primary"></q-icon>
      <div class="text-h5 text-primary text-center">No Tasks</div>
    </div>
  </q-page>
</template>

<script setup lang="ts">
import { ref } from "vue";
import { useQuasar } from "quasar";
const $q = useQuasar();
interface Task {
  title: string;
  done: boolean;
}

const newTask = ref<string>("");

const tasks = ref<Task[]>([]);
function addTask() {
  tasks.value.push({ title: newTask.value, done: false });
  newTask.value = "";
}
function deleteTask(index: number) {
  $q.dialog({
    title: "Confirm",
    message: "Really delete?",
    cancel: true,
    persistent: true,
  }).onOk(() => {
    tasks.value.splice(index, 1);
    $q.notify("Task deleted");
  });
}
</script>

<style class="scss">
.done {
  .q-item__label {
    text-decoration: line-through;
    color: #bbb;
  }
}
.no-tasks {
  opacity: 0.5;
}
</style>
