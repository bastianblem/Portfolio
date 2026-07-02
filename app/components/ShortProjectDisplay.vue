<script setup lang="ts">
import projects from "~/data/projects.json";
import ShortProjectCard from "./cards/ShortProjectCard.vue";
import { Swiper, SwiperSlide } from "swiper/vue";
import { Pagination, Navigation } from "swiper/modules";
/*
 *   Swiper modules added to build an easy swiper for the projects
 */
import "swiper/css";
import "swiper/css/pagination";
import "swiper/css/navigation";
// Reduce displayed Projects
const featured = projects.slice(0, 4);
</script>

<template>
  <div class="relative px-10 md:px-16 max-w-7xl mx-auto">
    <!-- Swiper implementation -->
    <Swiper
      :modules="[Pagination, Navigation]"
      :slides-per-view="1"
      :space-between="24"
      :navigation="{ nextEl: '.next-btn', prevEl: '.prev-btn' }"
      :pagination="{ clickable: true, el: '.custom-pagination' }"
      :breakpoints="{ 768: { slidesPerView: 2 }, 1024: { slidesPerView: 3 } }"
      class="pb-12 h-full"
    >
      <SwiperSlide v-for="p in featured" :key="p.id" class="!h-auto">
        <ShortProjectCard :project="p" class="h-full" />
      </SwiperSlide>
    </Swiper>

    <!-- Arrow navigation through projects left/right(UX) -->
    <button
      class="prev-btn absolute left-0 top-1/2 -translate-y-1/2 z-10 flex items-center p-2 bg-surface-card border border-surface-hover rounded-full"
    >
      <Icon name="heroicons:arrow-left" class="h-6 text-text-heading" />
    </button>
    <button
      class="next-btn absolute right-0 top-1/2 -translate-y-1/2 z-10 flex items-center p-2 bg-surface-card border border-surface-hover rounded-full"
    >
      <Icon name="heroicons:arrow-right" class="h-6 text-text-heading" />
    </button>

    <!-- Progress bar: gives location within projects(UX) -->
    <div class="custom-pagination"></div>
  </div>
</template>
