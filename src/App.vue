<template>
  <div
    style="min-height: 100vh;"
  >
    <div
      style="width: 100%; max-width: 600px; padding: 24px; border-radius: 16px; backdrop-filter: blur(10px); border: 1px solid rgba(255, 255, 255, 0.2); box-shadow: 0 4px 16px rgba(0, 0, 0, 0.4);"
    >
      <h1
        style="font-size: 28px; font-weight: bold; text-align: center; margin-bottom: 24px;"
      >
        Todo
      </h1>

      <!-- タスク入力欄 -->
      <TodoInput v-model="newTodo" @submit="addTodo" />

      <!-- タスク一覧表示 -->
      <TodoList :todos="todos" />

      <!-- 完了済み一括削除ボタン -->
      <CompletedTaskButton @click="CompletedTask" />
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, watchEffect } from 'vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import CompletedTaskButton from './components/CompletedTaskButton.vue'

const newTodo = ref('')
const todos = ref<{ text: string; done: boolean }[]>([])

// 起動時にローカルストレージから読み込む
onMounted(() => {
  const saved = localStorage.getItem('todos')
  if (saved) {
    todos.value = JSON.parse(saved)
  }
})

// todosが変わるたびに保存
watchEffect(() => {
  localStorage.setItem('todos', JSON.stringify(todos.value))
})

// タスク追加処理
function addTodo() {
  if (newTodo.value.trim()) {
    todos.value.push({ text: newTodo.value, done: false })
    newTodo.value = ''
  }
}

// 完了済みタスクの一括削除
function CompletedTask() {
  todos.value = todos.value.filter(todo => !todo.done)
}
</script>
