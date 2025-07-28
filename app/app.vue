<script setup lang="ts">
const nuxtApp = useNuxtApp()
</script>

<template>
  <BaseProviders> 
    <BaseHeading as="h1" size="4xl" weight="semibold" lead="normal" class="flex items-center justify-center gap-2">
      <Icon name="solar:bill-list-outline" />
      To-Do List
    </BaseHeading>
    <NuxtPage />
  </BaseProviders>
</template>




