<script setup lang="ts">
import { ref } from "vue";

const toDoArray = [{ desc: "Test", done: false }];

const showCreateBar = ref(false);

// const savedText = ref("");

function create() {
  showCreateBar.value = true;
  // if(){}
}

function update() {}

function erase() {}
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
      <input type="text" v-if="showCreateBar" />
      <button>Submit</button>
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
