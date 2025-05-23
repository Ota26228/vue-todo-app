<!-- src/DeleteComplitedButton.vue-->
 <template>
    <button @click="$emit('click')" class="w-full bg-red-500 text-white py-2 rounded hover:bg-red-600 transition">
    完了済みタスクを削除
    </button>
 </template>

 <script setup lang="ts">
    defineEmits<{
        (e: 'click'): void
    }>()
 </script>