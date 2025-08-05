<script setup lang="ts">
import { ref } from 'vue'

const input = ref('')
const tasks = ref<string[]>([])
const completed = ref<number[]>([])

function addTask() {
    if (input.value.trim() !== '') {
        tasks.value.push(input.value.trim())
        input.value = ''
    }
}
function removeTask(index: number){
    tasks.value.splice(index, 1)
    completed.value.splice(index, 1)
}
function completedTask(index: number){
    const a = completed.value.indexOf(index)
    if (a === -1) {
        completed.value.push(index)
    }
    else {
        completed.value.splice(index, 1)
    }
}

</script>

<template>
    <div class="flex flex-col items-center mt-8">
        <BaseCard rounded="lg" class="flex justify-between items-center gap-2 p-2 w-full max-w-xl">
            <BaseInput v-model="input" type="text" placeholder="Crie uma tarefa aqui..." rounded="full" class=""/>
            <Icon name="solar:add-circle-line-duotone" class="size-10 cursor-pointer" @click="addTask"/>
        </BaseCard>
        <BaseCard rounded="lg" class="nui-slimscroll w-full max-w-xl overflow-y-auto h-96 mt-2">
            <div class="flex justify-between p-2">
                <p class="flex items-center gap-2"> Tarefas Criadas <span class="flex items-center justify-center bg-zinc-500 rounded-full text-sm px-2 py-0.5">{{ tasks.length }}</span> </p>
            </div>
            <BaseList class="p-2">
                <li v-for="(task, index) in tasks" class="flex items-center justify-between text-wrap">
                    <div class="flex items-center gap-2">
                    <Icon name="solar:check-circle-bold" class="size-6 cursor-pointer" @click="completedTask(index)"> </Icon>
                    <p :class="{'line-through': completed.includes(index)}">{{ index + 1 }}. {{ task }}</p>
                    </div>
                    <Icon name="solar:close-square-bold" class="size-6 cursor-pointer" @click="removeTask(index)"/>
                </li>
            </BaseList>
        </BaseCard>
    </div>
</template>

