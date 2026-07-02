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
  { label: "My CV", to: "/cv" },
  {
    label: "About Me",
    to: "/about",
    dropdown: [
      {
        label: "GitHub",
        href: "https://github.com/bastianblem",
        icon: "mdi:github",
      },
      {
        label: "LinkedIn",
        href: "https:// linkedin.com/in/bastian-buettner/",
        icon: "mdi:linkedin",
      },
    ],
  },
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
      ><span class="text-text-heading font-display text-lg"
        >Bastian Büttner</span
      >
      <span class="text-text-body/50 font-light hidden sm:block">|</span>
      <span
        class="text-accent-teal font-medium text-sm tracking-wide hidden sm:block"
        >blubdev</span
      ></NuxtLink
    >
    <!-- Center: Desktop Navigation -->
    <nav class="hidden md:flex items-center gap-8 text-text-body">
      <div
        v-for="navLink in navLinks"
        :key="navLink.label"
        class="relative group"
      >
        <!-- Links without dropdown option -->
        <NuxtLink
          v-if="!navLink.dropdown"
          :to="navLink.to"
          class="flex items-center hover:text-text-heading hover:text-shadow-sm transition-all font-medium py-2"
        >
          {{ navLink.label }}
        </NuxtLink>

        <!-- Link with dropdown option -->
        <div v-else class="flex items-center gap-1 cursor-pointer py-2">
          <NuxtLink
            :to="navLink.to"
            class="hover:text-text-heading hover:text-shadow-sm transition-all font-medium"
          >
            {{ navLink.label }}
          </NuxtLink>
          <!-- Arrow: up/down -->
          <Icon
            name="heroicons:chevron-down"
            class="w-4 h-4 opacity-70 group-hover:rotate-180 transition-transform duration-300"
          />

          <!-- Dropdown menu -->
          <div
            class="absolute top-full left-1/2 -translate-x-1/2 mt-2 w-48 opacity-0 invisible group-hover:opacity-100 group-hover:visible transition-all duration-200 bg-surface-card/95 backdrop-blur-xl border border-surface-hover rounded-xl shadow-xl shadow-black/50 p-2 flex flex-col gap-1"
          >
            <a
              v-for="subLink in navLink.dropdown"
              :key="subLink.label"
              :href="subLink.href"
              target="_blank"
              rel="noopener noreferrer"
              class="flex items-center gap-3 px-3 py-2 rounded-lg hover:bg-surface-hover text-text-body hover:text-accent-teal transition-colors"
            >
              <Icon :name="subLink.icon" class="w-5 h-5" />
              <span class="font-medium">{{ subLink.label }}</span>
            </a>
          </div>
        </div>
      </div>
    </nav>
    <!-- Right: Desktop CTA & Mobile Toggle -->
    <div class="flex items-center gap-4 z-50">
      <button
        class="hidden md:block px-5 py-2 rounded-full bg-accent-teal/10 text-accent-teal font-medium hover:bg-accent-teal/20 border border-accent-teal/20 transition-colors"
      >
        Contact me
      </button>

      <!-- Mobile burger button -->
      <button
        @click="isMenuOpen = !isMenuOpen"
        class="md:hidden text-text-heading hover:text-accent-teal transition-colors p-1"
        aria-label="Toggle Menu"
      >
        <Icon
          :name="isMenuOpen ? 'heroicons:x-mark' : 'heroicons:bars-3'"
          class="w-7 h-7"
        />
      </button>
    </div>

    <!-- Mobile menu dropdown -->
    <div
      v-if="isMenuOpen"
      class="absolute top-full left-0 mt-4 w-full bg-surface-card/95 backdrop-blur-xl border border-surface-hover rounded-2xl p-4 flex flex-col gap-2 shadow-xl shadow-black/50 md:hidden"
    >
      <template v-for="navLink in navLinks" :key="navLink.label">
        <!-- links within mobile menu-->
        <NuxtLink
          :to="navLink.to"
          @click="isMenuOpen = false"
          class="text-text-heading hover:text-accent-teal transition-colors font-medium text-lg text-center py-3 border-b border-surface-hover/50 last:border-none"
        >
          {{ navLink.label }}
        </NuxtLink>

        <!-- sublinks within mobile menu-->
        <div
          v-if="navLink.dropdown"
          class="flex flex-col gap-2 bg-surface-base/50 rounded-xl p-3 mb-2"
        >
          <a
            v-for="subLink in navLink.dropdown"
            :key="subLink.label"
            :href="subLink.href"
            target="_blank"
            rel="noopener noreferrer"
            class="flex items-center justify-center gap-2 text-text-body hover:text-accent-teal transition-colors py-2"
          >
            <Icon :name="subLink.icon" class="w-5 h-5" />
            <span>{{ subLink.label }}</span>
          </a>
        </div>
      </template>
      <!-- CTA button -->
      <button
        class="w-full mt-2 px-5 py-3 rounded-full bg-accent-teal/10 text-accent-teal font-medium hover:bg-accent-teal/20 border border-accent-teal/20 transition-colors"
      >
        Contact me
      </button>
    </div>
  </header>
</template>
