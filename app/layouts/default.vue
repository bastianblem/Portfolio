<!-- Future default layout for chosen pages -->
<template>
  <Header />
  <main>
    <slot />
  </main>
  <Footer />
</template>
<script setup lang="ts">
import Footer from "~/components/Footer.vue";
import Header from "~/components/Header.vue";
</script>
