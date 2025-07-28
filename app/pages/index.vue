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

function removeTask(index: number){
    tasks.value.splice(index, 1)
}

</script>

<template>
    <div class="flex flex-col items-center mt-8">
        <BaseCard rounded="lg" class="flex justify-between gap-2 p-2">
            <BaseInput v-model="input" type="text" placeholder="Crie uma tarefa aqui..." rounded="full" class="">
            </BaseInput>
            <BaseButton @click="addTask" rounded="full" class="">
                <Icon name="solar:add-circle-line-duotone" width="24" height="24" /> 
            </BaseButton>
        </BaseCard>
        <BaseCard rounded="lg" class="w-full max-w-xl h-64 mt-2">
            <BaseList class="">
                <li v-for="(task, index) in tasks">
                    {{ index + 1 }}. {{ task }}
                    <BaseButton @click="removeTask" rounded="full">
                        <Icon name="solar:close-square-bold" width="24" height="24" />
                    </BaseButton>
                </li>
            </BaseList>
        </BaseCard>
    </div>
</template>

