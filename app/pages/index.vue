<template>
    <div class="flex flex-col items-center justify-center mt-8">
        <BaseCard variant="default" rounded="lg" class="flex justify-between gap-2 p-8">
            <BaseInput v-model="value" type="text" placeholder="Crie uma tarefa aqui..." rounded="full" class="">
            </BaseInput>
            <BaseButton @click="addTask" size="md" rounded="full" class="">
                Criar tarefa 
            </BaseButton>
        </BaseCard>
        <BaseCard variant="default" rounded="lg" class="p-40">
            <BaseList ordered class="ps-8">
                <li v-for="(task, index) in tasks" :key="index">
                    {{ index + 1 }}. {{ task }}
                </li>
            </BaseList>
        </BaseCard>
    </div>
</template>

<script setup lang="ts">
import { BaseInput } from '#components';
import { addTemplate } from 'nuxt/kit';
import { ref } from 'vue'
const value = ref('')
const tasks = ref<string[]>([])
function addTask() {
    if (value.value.trim() !== '') {
        tasks.value.push(value.value.trim())
        value.value = ''
    }
}

</script>
