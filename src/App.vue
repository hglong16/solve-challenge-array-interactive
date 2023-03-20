<template>
  <div class="app">
    <div class="title">
      <h3>Change cell directly, click right side to add an item</h3>
    </div>
    <div class="container">
      <div class="cell" v-for="(cell, index) in cells" :key="index">
        <input
          class="input__cell"
          type="text"
          :value="cell"
          :style="{ width: cell.length + 'ch' }"
          @input="(event) => handleInputOnChange(event, index)"
        />

        <span class="add__to-right" @click="addToRight(index)"></span>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { createSlots, ref, computed } from "vue";

const cells = ref(["a", "b", "c"]);

const handleInputOnChange = (event: Event, index: number) => {
  for (let [i, v] of cells.value.entries()) {
    cells.value[i] =
      i === index ? (event.target as HTMLTextAreaElement).value : v;
  }
};

const addToRight = (index: number) => {
  console.log("hello");
  cells.value = [
    ...cells.value.slice(0, index + 1),
    "_",
    ...cells.value.slice(index + 1),
  ];
};

(window as any).testArray = computed(() => cells.value);
</script>

<style scoped>
.app {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  align-items: center;
  height: 100vh;
}

.container {
  display: flex;
  flex-direction: row;
  flex-wrap: auto;
  max-width: 920px;
  margin: auto auto;
  gap: 5px;
}

.title {
  color: white;
  width: 100%;
  text-align: center;
  margin: 50px auto;
}
.cell {
  display: flex;
  position: relative;
  padding: 5px;
  height: 50px;
  width: fit-content;
  min-width: 50px;
  border: 1px solid #dedede;
  color: white;
  border-radius: 10px;
  align-items: center;
  justify-content: center;
}

.input__cell {
  background-color: none;
  border: none;
  cursor: pointer;
  color: #fff;
  outline: none;
}

.input_cell:focus {
  outline: none;
  border: none;
}

.add__to-right {
  position: absolute;
  border-radius: 2px;
  right: -7px;
  top: 0;
  background-color: transparent;
  width: 10px;
  cursor: pointer;
  z-index: 1;
  height: 100%;
}

.add__to-right:hover {
  background-color: #73f58025;
}
</style>
