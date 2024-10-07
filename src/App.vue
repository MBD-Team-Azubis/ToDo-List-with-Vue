<script setup lang="ts">
import { ref } from "vue";

let toDoArray = ref<{ desc: string; done: boolean }[]>([]);

let showBar = ref<"create" | "entryUpdate" | "update" | "delete" | "">("");

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
  <body>
    <div class="container">
      <h1>To-Do-List</h1>
      <hr />
      <button @click="showBar = 'create'">Create</button>
      <button @click="showBar = 'update'">Update</button>
      <button @click="showBar = 'delete'">Delete</button>
      <hr />
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
  </body>
</template>

<style scoped>
.container {
  margin: 0 auto;
  height: 600px;
  width: 500px;
  border: 2px solid black;
  text-align: center;
}
</style>
