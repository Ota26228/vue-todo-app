<template>
  <li style="margin-bottom: 8px;">
    <label style="display: flex; align-items: center; gap: 8px;">
      <input type="checkbox" v-model="props.todo.done" />
      <span :class="props.todo.done ? 'line-through text-gray-400':'text-gray-800'">
        {{ props.todo.text }}
      </span>
    </label>
  </li>
</template>

<script setup lang="ts">
const props = defineProps<{
  todo: { text: string; done: boolean }
  index: number
}>()
</script>
