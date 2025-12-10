<script setup lang="ts">
import { Lock } from 'lucide-vue-next'
</script>

<template>
  <header class="app-header">
    <div class="header-icon-bg">
      <Lock class="icon-md" />
    </div>
    <h1 class="header-title">The Earned Spend Vault</h1>
  </header>
</template>

<style scoped>
.app-header {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0.4rem;
  gap: 1rem;
}

.header-icon-bg {
  padding: 0.5rem;
  border-radius: 0.75rem;
  background-image: linear-gradient(
    to bottom right,
    var(--color-purple-600),
    var(--color-pink-500)
  );
}

.icon-md {
  width: 1.5rem;
  height: 1.5rem;
}

.header-title {
  font-size: 1.25rem;
}
</style>
