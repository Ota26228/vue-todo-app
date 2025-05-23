<!-- src/components/TodoInput.vue -->
 <template>
    <input
     v-model="inputText"
     @keyup.enter="handleSubmit"
     placeholder="新しいTodoを追加"
     class="w-full px-4 py-2 border border-gray-300 rounded focus:outline-none focus:ring-2 focus:ring-blue-400"
    />
 </template>

 <script lang="ts" setup>
    import { ref, watch } from 'vue'

    const props = defineProps<{ modelValue: string }>()

    const emit = defineEmits<{
        (e: 'update:modelValue', value: string): void
        (e: 'submit'): void
    }>()

    const inputText = ref(props.modelValue)

        //親からの更新を反映する
        watch(
            () => props.modelValue,
            (newVal) => {
                inputText.value = newVal
            }
        )

        //入力値の変更を親に伝える
        watch(inputText, (val) => {
            emit('update:modelValue', val)
        })

        function handleSubmit() {
            emit('submit')
        }

</script>