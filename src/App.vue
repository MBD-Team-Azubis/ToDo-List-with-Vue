<script setup lang="ts">
import { ref } from "vue";

let toDoArray = ref<{ desc: string; done: boolean }[]>([]);

let showBar = ref<"create" | "entryUpdate" | "update" | "delete" | "">(
  "create"
);

// sideNote: toDoArray.value[listIndex].desc um desc des objektes anzuzeigen.

const entry = ref("");
const listIndex = ref(0);

function addNewEntry() {
  toDoArray.value.push({ desc: entry.value, done: false });
  entry.value = "";
  showBar.value = "";
  console.log(toDoArray);
  listIndex.value = 0;
}

function whichEntryToUpdate() {
  showBar.value = "update";
  let tempStorage = listIndex.value;
  entry.value = toDoArray.value[tempStorage - 1].desc;
  showBar.value = "entryUpdate";
}

function entryUpdate() {
  let tempStorage = listIndex.value;
  toDoArray.value[tempStorage - 1].desc = entry.value;
  entry.value = "";
  listIndex.value = 0;
  showBar.value = "";
}

function entryDeletion() {
  toDoArray.value.splice(listIndex.value - 1, 1);
  showBar.value = "";
  listIndex.value = 0;
}
</script>

<template>
  <div class="screen">
    <div class="container">
      <div class="headline">
        <h1>To-Do-List</h1>
      </div>
      <div class="buttons">
        <button @click="showBar = 'create'">Create</button>
        <button @click="showBar = 'update'">Update</button>
        <button @click="showBar = 'delete'">Delete</button>
      </div>
      <input
        type="text"
        v-model="entry"
        @keydown.enter="addNewEntry()"
        v-if="showBar === 'create'"
        placeholder="Enter your entry:"
      />
      <input
        type="text"
        v-model="listIndex"
        @keydown.enter="whichEntryToUpdate()"
        v-if="showBar === 'update'"
        placeholder="Enter number to update"
      />
      <input
        type="text"
        v-model="entry"
        @keydown.enter="entryUpdate()"
        v-if="showBar === 'entryUpdate'"
        placeholder="entry"
      />
      <input
        type="text"
        v-model="listIndex"
        @keydown.enter="entryDeletion()"
        v-if="showBar === 'delete'"
        placeholder="Enter number to delete"
      />
      <div v-for="(item, index) in toDoArray" :key="item.desc">
        <p :class="{ open: !item.done, done: item.done }">
          {{ index + 1 }} : {{ item.desc }}
        </p>
      </div>
    </div>
  </div>
</template>

<style scoped>
div .screen {
  height: 100vh;
  background-color: #e9edc9;
}

.container {
  background-color: #fefae0;
  margin: 0 auto;
  height: auto;
  width: calc(100% / 3);
  border: 2px solid black;
  text-align: center;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  font-weight: 600;
  font-size: medium;
}

.headline {
  border-bottom: solid black 2px;
}

.buttons {
  border-bottom: solid black 2px;
}

.buttons button {
  margin: 15px;
  background-color: #fefae0;
  width: 5em;
  height: 2em;
  font-size: small;
  font-weight: 600;
}
</style>
