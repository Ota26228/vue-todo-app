<template>
  <ul style="list-style: none; padding: 0;">
    <TodoItem
      v-for="(todo, index) in todos"
      :key="index"
      :todo="todo"
      :index="index"
    />
  </ul>
</template>

<script setup lang="ts">
import TodoItem from './TodoItem.vue'

defineProps<{
  todos: { text: string; done: boolean }[]
}>()
</script>
