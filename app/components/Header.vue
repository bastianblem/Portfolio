<script setup lang="ts">
import { ref, onMounted, onUnmounted } from "vue";

const isMenuOpen = ref(false);
const isScrolled = ref(false);
const handleScroll = () => {
  isScrolled.value = window.scrollY > 10;
};
onMounted(() => {
  window.addEventListener("scroll", handleScroll);
  handleScroll();
});
onUnmounted(() => {
  window.removeEventListener("scroll", handleScroll);
});
const navLinks = [
  { label: "Projects", to: "/projects" },
  { label: "About Me", to: "/about" },
  { label: "My CV", to: "/cv" },
];
</script>

<template>
  <header
    :class="[
      'fixed top-4 left-1/2 -translate-x-1/2 z-50 w-[95%] max-w-6xl px-6 py-3 rounded-full border transition-all duration-300 flex items-center justify-between',
      isScrolled
        ? 'backdrop-blur-xl bg-surface-card/80 border-surface-hover shadow-lg shadow-black/40'
        : 'backdrop-blur-md bg-surface-card/30 border-transparent',
    ]"
  >
    <!-- Left: Brand -->
    <NuxtLink
      to="/"
      class="flex items-center gap-2 hover:opacity-80 transition-opacity z-50"
      ><span class="text-text-heading font-bold font-display text-lg"
        >Bastian Büttner</span
      >
      <span class="text-text-body/50 font-light hidden sm:block">|</span>
      <span
        class="text-accent-teal font-medium text-sm tracking-wide hidden sm:block"
        >blubdev</span
      ></NuxtLink
    >
    <!-- Center: Navigation -->
    <nav class="hidden md:flex gap-8 text-text-body">
      <NuxtLink
        v-for="navLink in navLinks"
        :key="navLink.to"
        :to="navLink.to"
        class="hover:text-text-heading hover:text-shadow-sm transition-all font-medium"
        >{{ navLink.label }}</NuxtLink
      >
    </nav>
    <!-- Right: Desktop CTA & Mobile Toggle -->
    <div class="flex items-center gap-4 z-50">
      <button
        class="hidden md:block px-5 py-2 rounded-full bg-accent-teal/10 text-accent-teal font-medium hover:bg-accent-teal/20 border border-accent-teal/20 transition-colors"
      >
        Contact me
      </button>

      <!-- Mobile Burger Button -->
      <button
        @click="isMenuOpen = !isMenuOpen"
        class="md:hidden text-text-heading hover:text-accent-teal transition-colors p-1"
        aria-label="Toggle Menu"
      >
        <!-- Tauscht das Icon dynamisch aus, wenn das Menü offen ist -->
        <Icon
          :name="isMenuOpen ? 'heroicons:x-mark' : 'heroicons:bars-3'"
          class="w-7 h-7"
        />
      </button>
    </div>
    <!-- Mobile Menu Dropdown -->
    <div
      v-if="isMenuOpen"
      class="absolute top-full left-0 mt-4 w-full bg-surface-card border border-surface-hover rounded-2xl p-4 flex flex-col gap-4 shadow-xl shadow-black/50 md:hidden"
    >
      <NuxtLink
        v-for="navLink in navLinks"
        :key="navLink.to"
        :to="navLink.to"
        @click="isMenuOpen = false"
        class="text-text-heading hover:text-accent-teal transition-colors font-medium text-lg text-center py-3 border-b border-surface-hover/50 last:border-none"
      >
        {{ navLink.label }}
      </NuxtLink>
      <button
        class="w-full mt-2 px-5 py-3 rounded-xl bg-accent-teal/10 text-accent-teal font-medium hover:bg-accent-teal/20 border border-accent-teal/20 transition-colors"
      >
        Contact me
      </button>
    </div>
  </header>
</template>
