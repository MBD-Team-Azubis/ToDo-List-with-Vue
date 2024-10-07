<script setup lang="ts">
import { ref } from "vue";

let toDoArray = ref<{ desc: string; done: boolean }[]>([]);

const showCreateBar = ref(false);
const showUpdateBar = ref(false);
const showEntryUpdateBar = ref(false);
const showDeleteBar = ref(false);

// sideNote: toDoArray.value[listIndex].desc um desc des objektes anzuzeigen.

const entry = ref("");
const listIndex = ref(0);

function create() {
  showCreateBar.value = true;
  showUpdateBar.value = false;
  showEntryUpdateBar.value = false;
  showDeleteBar.value = false;
}

function update() {
  showUpdateBar.value = true;
  showEntryUpdateBar.value = false;
  showCreateBar.value = false;
  showDeleteBar.value = false;
}

function erase() {
  showDeleteBar.value = true;
  showCreateBar.value = false;
  showUpdateBar.value = false;
  showEntryUpdateBar.value = false;
}

function whichEntryToUpdate() {
  showUpdateBar.value = false;
  let tempStorage = listIndex.value;
  entry.value = toDoArray.value[tempStorage - 1].desc;
  showEntryUpdateBar.value = true;
}

function addNewEntry() {
  toDoArray.value.push({ desc: entry.value, done: false });
  entry.value = "";
  showCreateBar.value = false;
  console.log(toDoArray);
  listIndex.value = 0;
}

function entryUpdate() {
  let tempStorage = listIndex.value;
  toDoArray.value[tempStorage - 1].desc = entry.value;
  entry.value = "";
  listIndex.value = 0;
  showEntryUpdateBar.value = false;
}

function entryDeletion() {
  toDoArray.value.splice(listIndex.value - 1, 1);
  showDeleteBar.value = false;
  listIndex.value = 0;
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
        @keydown.enter="whichEntryToUpdate()"
        v-if="showUpdateBar"
        placeholder="Enter number to update"
      />
      <input
        type="text"
        v-model="entry"
        @keydown.enter="entryUpdate()"
        v-if="showEntryUpdateBar"
        placeholder="entry"
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
