<script setup lang="ts">
import { ref } from "vue";

let toDoArray = ref<{ desc: string; done: boolean }[]>([]);

const showCreateBar = ref(false);
const showUpdateBar = ref(false);
const showDeleteBar = ref(false);

// sideNote: toDoArray.value[listIndex].desc um desc des objektes anzuzeigen.

const entry = ref("");
const listIndex = ref(0);

function create() {
  showCreateBar.value = true;
}

function update() {
  showUpdateBar.value = true;
}

function erase() {
  showDeleteBar.value = true;
}

function updateEntry() {}

function addNewEntry() {
  toDoArray.value.push({ desc: entry.value, done: false });
  entry.value = "";
  showCreateBar.value = false;
  console.log(toDoArray);
}

function entryDeletion() {
  toDoArray.value.splice(listIndex.value - 1, 1);
  showDeleteBar.value = false;
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
        placeholder="Enter your entry:"
      />
      <input
        type="text"
        v-model="listIndex"
        @keydown.enter="updateEntry()"
        v-if="showUpdateBar"
        placeholder="Enter number to update"
      />
      <input
        type="text"
        v-model="listIndex"
        @keydown.enter="entryDeletion()"
        v-if="showDeleteBar"
        placeholder="Enter number to delete"
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
</style>
