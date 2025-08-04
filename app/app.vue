<script setup lang="ts">
const nuxtApp = useNuxtApp()
</script>

<template>
  <div class="min-h-screen bg-black bg-gradient-to-b from-sky-600 to-sky-800">
    <BaseProviders> 
    <BaseHeading as="h1" size="4xl" weight="semibold" lead="normal" class="flex items-center justify-center gap-2 font-mono">
      <Icon name="solar:bill-list-outline" />
      todo
    </BaseHeading>
    <NuxtPage />
  </BaseProviders>
  </div>
</template>




