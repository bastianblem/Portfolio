<template>
  <!-- detailed project card to give out every relevant information about the projects -->
  <div
    class="group flex flex-col bg-surface-card border border-surface-hover rounded-2xl overflow-hidden hover:border-accent-teal/50 transition-all duration-300"
  >
    <div
      class="h-48 bg-surface-hover flex items-center justify-center overflow-hidden"
    >
      <Icon name="heroicons:photo" class="w-12 h-12 text-surface-base/50" />
    </div>

    <div class="p-6 flex flex-col grow">
      <div class="mb-4">
        <h3 class="text-text-heading font-display text-xl font-bold">
          {{ project.title }}
        </h3>
        <p class="text-accent-blue text-sm font-medium">
          {{ project.subtitle }}
        </p>
      </div>

      <p class="text-text-body text-sm mb-6 grow">
        {{ project.description }}
      </p>

      <div class="flex flex-wrap gap-2 mb-6">
        <span
          v-for="tag in project.tags"
          :key="tag"
          class="text-[10px] uppercase tracking-wider bg-surface-base text-text-body px-2 py-1 rounded-md border border-surface-hover"
        >
          {{ tag }}
        </span>
      </div>

      <!-- links to view repository/live-preview(vercel/figma) -->
      <div class="p-6 flex flex-col grow">
        <div
          v-if="project.links?.live || project.links?.repo"
          class="flex items-center gap-3 mt-auto pt-4 border-t border-surface-hover"
        >
          <a
            v-if="project.links?.live && project.links.live !== '#'"
            :href="project.links.live"
            target="_blank"
            class="text-sm font-medium text-text-heading hover:text-accent-teal transition-colors"
          >
            → Live Demo
          </a>
          <a
            v-if="project.links?.repo && project.links.repo !== '#'"
            :href="project.links.repo"
            target="_blank"
            class="text-sm font-medium text-text-body hover:text-accent-teal transition-colors"
          >
            → Source Code
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
defineProps<{
  project: {
    title: string;
    subtitle: string;
    description: string;
    tags: string[];
    /*
     *  optional links since not every project
     *  has a live preview no accessible github repository
     */
    links?: {
      live?: string;
      repo?: string;
    };
    image: string;
  };
}>();
</script>
