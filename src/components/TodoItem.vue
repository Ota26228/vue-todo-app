<template>
  <li style="margin-bottom: 8px;">
    <label style="display: flex; align-items: center; gap: 8px;">
      <input type="checkbox" v-model="todo.done" />
      <span :style="{ textDecoration: todo.done ? 'line-through' : 'none' }">
        {{ todo.text }}
      </span>
      <button @click="handleDelete" style="margin-left: auto;">削除</button>
    </label>
  </li>
</template>

<script setup lang="ts">
const props = defineProps<{
  todo: { text: string; done: boolean }
  index: number
}>()

const emit = defineEmits<{
  (e: 'delete', index: number): void
}>()

function handleDelete() {
  emit('delete', props.index)
}
</script>
