<script setup lang="ts">
import { RouterLink, RouterView, useRoute } from 'vue-router'
import { computed } from 'vue'
const route = useRoute()
const isDatingApp = computed(() => route.path.includes('/dating'))
</script>

<template>
  <header>
    <div class="max-w-4xl mx-auto">
      <nav class="p-4 bg-gray-100 rounded-b-lg shadow-md flex gap-4">
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
        <RouterLink to="/contact">Contact</RouterLink>
        <RouterLink to="/dating" class="text-[#ff6f61] font-bold">Dating App</RouterLink>
      </nav>
    </div>
  </header>

  <main :class="isDatingApp ? 'w-full min-h-screen' : 'max-w-4xl mx-auto mt-5'">
    <RouterView />
  </main>
</template>