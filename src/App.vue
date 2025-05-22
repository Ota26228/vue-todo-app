<template>
  <div style="padding: 20px">
    <h1 style="font-size: 32px;">Todo</h1>
    <input
      v-model="newTodo"
      @keyup.enter="addTodo"
      placeholder="新しいタスクを入力"
      style="margin-bottom: 10px; padding: 6px; width: 250px;"
    />
    <ul style="list-style-type: none; padding: 0; margin: 0;">
      <TodoItem
        v-for="(todo, index) in todos"
        :key="index"
        :todo="todo"
        :index="index"
        @delete="deleteTodo"
      />
        </ul>
    <button @click="deleteTodo">完了済みを一括削除</button>
  </div>
</template>

<script lang="ts" setup>
import { ref, watchEffect,onMounted } from 'vue'
import TodoItem from './components/TodoItem.vue'

const newTodo = ref('')
const todos = ref<{ text: string; done: boolean }[]>([])

//読み込み時にローカルストレージからデータを取得
onMounted(() => {
  const saved = localStorage.getItem('todos')
  if(saved) {
    todos.value=JSON.parse(saved)
  }
})

//自動でローカルストレージに保存
watchEffect(() => {
  localStorage.setItem('todos',JSON.stringify(todos.value))
})

function addTodo() {
  if (newTodo.value.trim()) {
    todos.value.push({ text: newTodo.value, done: false })
    newTodo.value = ''
  }
}

function deleteTodo() {
  todos.value=todos.value.filter(todo => !todo.done)
}
</script>


