<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/WelcomeMessage.vue'
</script>

<template>
  <header class="lg:flex lg:items-start lg:justify-start lg:pr-[var(--section-gap)/2] max-h-screen leading-[1.5]">
    <div class="lg:flex lg:items-start lg:flex-wrap">
      <HelloWorld msg="Arsip Surat Teknik Elektro" />

      <nav class="w-full text-center lg:text-left mt-8 lg:mt-4 lg:ml-[-1rem] text-sm lg:text-base">
        <RouterLink to="/"
          class="inline-block px-4 py-2 lg:border-l border-gray-300 first:lg:border-0 hover:bg-gray-100">
          Beranda
        </RouterLink>
        <RouterLink to="/about" class="inline-block px-4 py-2 lg:border-l border-gray-300 hover:bg-gray-100">
          Tentang
        </RouterLink>
      </nav>
    </div>
  </header>

  <RouterView />
</template>

<style scoped>
:root {
  --color-text: #333;
  --color-border: #ddd;
  --section-gap: 2rem;
}
</style>
