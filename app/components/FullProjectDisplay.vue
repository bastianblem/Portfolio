<script setup lang="ts">
import projects from "~/data/projects.json";
import ProjectCard from "./cards/ProjectCard.vue";
</script>

<template>
  <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
    <ProjectCard v-for="p in projects" :key="p.id" :project="p" />
  </div>
</template>
