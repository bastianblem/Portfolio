<template>
  <AppContainer class="py-20">
    <h1 class="text-4xl font-display text-text-heading mb-12">Alle Projekte</h1>
    <FullProjectDisplay />
  </AppContainer>
</template>
<script setup lang="ts">
import FullProjectDisplay from "~/components/FullProjectDisplay.vue";
import AppContainer from "~/components/container/AppContainer.vue";
</script>
