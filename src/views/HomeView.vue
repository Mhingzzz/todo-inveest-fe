<script setup lang="ts">
import VaultHeader from '@/components/vault/VaultHeader.vue'
import VaultStatusCard from '@/components/vault/VaultStatusCard.vue'
</script>

<template>
  <div class="vault-home-layout">
    <VaultHeader />
    <VaultStatusCard :locked-amount="1250.0" :goal-amount="100" currency="THB" />
  </div>
</template>

<style scoped>
.vault-home-layout {
  width: 100%;
  max-width: 28rem;
  margin: 0 auto;
  min-height: 100vh;
  color: var(--color-white);
  padding-bottom: 5rem;
  position: relative;
  background-color: var(--color-background);
}
</style>
