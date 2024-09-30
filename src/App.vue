<script setup lang="ts">
import { ref } from "vue";

let toDoArray = ref<{ desc: string; done: boolean }[]>([]);

const showCreateBar = ref(false);

let countOfEntrys = 0;

const entry = ref("");

function create() {
  showCreateBar.value = true;
}

function update() {}

function erase() {}

function addNewEntry() {
  countOfEntrys++;

  toDoArray.value.push({ desc: entry.value, done: false });
  entry.value = "";
}
</script>

<template>
  <body>
    <div>
      <h1>To-Do-List</h1>
      <hr />
      <button @click="create()">Create</button>
      <button @click="update()">Update</button>
      <button @click="erase()">Delete</button>
      <hr />
      <input
        type="text"
        v-model="entry"
        @keydown.enter="addNewEntry()"
        v-if="showCreateBar"
      />
      <div v-for="(item, index) in toDoArray" :key="item.desc">
        <p :class="{ open: !item.done, done: item.done }">
          {{ index + 1 }} : {{ item.desc }}
        </p>
      </div>
    </div>
  </body>
</template>

<style scoped>
body {
  margin: 0 auto;
  height: 600px;
  width: 500px;
  border: 2px solid black;
  text-align: center;
}

button {
  margin: 10px;
}
</style>
