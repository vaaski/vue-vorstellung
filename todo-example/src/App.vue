<script setup lang="ts">
import { ref, watch } from "vue"

const items = ref([
  { text: "Todo 1", done: false },
  { text: "Todo 2", done: false },
  { text: "Todo 3", done: false },
])

watch(
  items,
  () => {
    localStorage.setItem("todo", JSON.stringify(items.value))
  },
  { deep: true },
)

const existing = localStorage.getItem("todo")
if (existing) {
  items.value = JSON.parse(existing)
}

// --------------------------------------------------------------------------------------

const newTodo = ref("")
const addTodo = (text: string) => {
  items.value.push({ text, done: false })
}

const removeTodo = (index: number) => {
  items.value.splice(index, 1)
}
</script>

<template>
  <div>
    <h1>Todo Example</h1>

    <form @submit.prevent="addTodo(newTodo)">
      <input v-model="newTodo" placeholder="Add todo" />
      <button>Add</button>
    </form>

    <ul>
      <li v-for="(item, index) in items" :key="item.text">
        <label>
          <input type="checkbox" v-model="item.done" />
          {{ item.text }}
        </label>
        <button @click="removeTodo(index)">Remove</button>
      </li>
    </ul>
  </div>
</template>
