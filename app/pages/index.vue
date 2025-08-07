<script setup lang="ts">
import { ref, defineExpose } from 'vue'

const input = ref('')
const inputRef = ref<HTMLInputElement | null>(null)
const tasks = ref<string[]>([])
const completed = ref<string[]>([])

defineExpose({
  focus: () => inputRef.value?.focus()
})

function addTask() {
    if (input.value.trim() !== '') {
        tasks.value.push(input.value.trim())
        input.value = ''
        inputRef.value?.focus()
    }
}
function removeTask(index: number){
    tasks.value.splice(index, 1)
    completed.value.splice(index, 1)
}
function completedTask(index: number){
    const task = tasks.value[index]
    if (task === undefined) return
    
    const a = completed.value.indexOf(task)
    if (a === -1) {
        completed.value.push(task)
    }
    else {
        completed.value.splice(a, 1)
    }
}
function enterTask(e: KeyboardEvent){
    if (e.key === 'Enter') {
        addTask()
    }
    
}

</script>

<template>
    <div class="flex flex-col items-center mt-8">
        <BaseCard rounded="lg" class="flex justify-between items-center gap-2 p-2 w-full max-w-xl">
            <BaseInput v-model="input" type="text" placeholder="Crie uma tarefa aqui..." rounded="full" class="" ref="inputRef" @keydown="enterTask"/>
            <Icon name="solar:add-circle-line-duotone" class="size-10 cursor-pointer" @click="addTask"/>
        </BaseCard>
        <BaseCard rounded="lg" class="nui-slimscroll w-full max-w-xl overflow-y-auto h-96 mt-2">
            <div class="flex justify-between p-2">
                <p class="flex items-center gap-2"> Tarefas Criadas <span class="flex items-center justify-center bg-zinc-500 rounded-full text-sm px-2 py-0.5">{{ tasks.length }}</span> </p>
                <p class="flex items-center gap-2">Tarefas concluídas <span class="flex items-center justify-center bg-zinc-500 rounded-full text-sm px-2 py-0.5">{{ completed.length }}</span> de <span class="flex items-center justify-center bg-zinc-500 rounded-full text-sm px-2 py-0.5">{{ tasks.length }}</span> </p>
            </div>
            <BaseList class="p-2">
                <li v-for="(task, index) in tasks" class="flex items-start justify-between text-wrap">
                    <div class="flex items-center gap-2">
                    <Icon :name="completed.includes(task) ? 'solar:check-circle-bold' : 'solar:check-circle-line-duotone'" class="size-6 cursor-pointer" @click="completedTask(index)"> </Icon>
                    <p :class="{'line-through': completed.includes(task)}" class="break-words max-w-[80%]">{{ index + 1 }}. {{ task }}</p>
                    </div>
                    <Icon name="solar:close-square-bold" class="size-6 cursor-pointer flex-shrink-0" @click="removeTask(index)"/>
                </li>
            </BaseList>
        </BaseCard>
    </div>
</template>

