<template>
  <!-- Shortened project card for the index page to reduce information overload -->
  <div
    class="bg-surface-card border border-surface-hover p-5 rounded-xl hover:border-accent-teal/50 transition-all h-full flex flex-col"
  >
    <h3 class="text-text-heading font-display font-bold">
      {{ project.title }}
    </h3>
    <p class="text-accent-blue text-xs mb-3">{{ project.subtitle }}</p>

    <p class="text-text-body text-sm line-clamp-3 mb-6 grow">
      {{ project.description }}
    </p>

    <NuxtLink
      to="/projects"
      class="text-accent-teal text-sm font-medium hover:underline mt-auto"
    >
      Mehr erfahren →
    </NuxtLink>
  </div>
</template>

<script setup lang="ts">
defineProps<{ project: any }>();
</script>
