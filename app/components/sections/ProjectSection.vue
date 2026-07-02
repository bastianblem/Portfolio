<template>
  <section class="py-16 w-full">
    <AppContainer>
      <h2 class="text-3xl font-display text-text-heading mb-8">
        Ausgewählte Projekte
      </h2>
      <ShortProjectDisplay />
      <div class="mt-10 text-center">
        <NuxtLink
          to="/projects"
          class="w-full mt-2 px-5 py-3 rounded-full bg-accent-teal/10 text-accent-teal font-medium hover:bg-accent-teal/20 border border-accent-teal/20 transition-colors"
        >
          Alle Projekte ansehen
        </NuxtLink>
      </div>
    </AppContainer>
  </section>
</template>
<script setup lang="ts">
import ShortProjectDisplay from "../ShortProjectDisplay.vue";
import AppContainer from "../container/AppContainer.vue";
</script>
