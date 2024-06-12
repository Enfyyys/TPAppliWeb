<template>
  <v-app>
    <Navbar />
    <v-main>
      <NuxtPage />
    </v-main>
  </v-app>
</template>

<script setup>
import Navbar from '@/components/navBar.vue'
</script>

<style>
.page-enter-active,
.page-leave-active {
  transition: all 0.4s;
}
.page-enter-from,
.page-leave-to {
  opacity: 0;
  filter: blur(1rem);
}
</style>
