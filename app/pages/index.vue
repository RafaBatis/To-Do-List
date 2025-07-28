<script setup lang="ts">
import { ref } from 'vue'
const input = ref('')
const tasks = ref<string[]>([])
function addTask() {
    if (input.value.trim() !== '') {
        tasks.value.push(input.value.trim())
        input.value = ''
    }
}
</script>

<template>
    <div class="flex flex-col items-center mt-8">
        <BaseCard rounded="lg" class="flex justify-between gap-2 p-8">
            <BaseInput v-model="input" type="text" placeholder="Crie uma tarefa aqui..." rounded="full" class="">
            </BaseInput>
            <BaseButton @click="addTask" size="md" rounded="full" class="">
                Criar tarefa 
            </BaseButton>
        </BaseCard>
        <BaseCard rounded="lg" class="w-full max-w-xl h-64 mt-2">
            <BaseList class="">
                <li v-for="(task, index) in tasks">
                    {{ index + 1 }}. {{ task }}
                </li>
            </BaseList>
        </BaseCard>
    </div>
</template>

