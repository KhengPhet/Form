<script setup>
import AppHeader from '@/components/layout/AppHeader.vue'
import AppFooter from '@/components/layout/AppFooter.vue'
</script>
<template>
  <div>
    <AppHeader />
    <main class="min-h-screen bg-background-light dark:bg-background-dark transition-colors">
      <slot />
    </main>
    <AppFooter />
  </div>
</template>

