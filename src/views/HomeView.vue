<script setup lang="ts">
import { CurrencyIcon, DollarSign, Goal, Lock, Sparkles } from 'lucide-vue-next' // ต้องเปลี่ยนมาใช้ lucide-vue-next แทน lucide-react
</script>

<template>
  <div class="vault-home-layout">
    <header class="app-header">
      <div class="header-icon-bg">
        <Lock class="icon-md" />
      </div>
      <h1 class="text-xl">The Earned Spend Vault</h1>
    </header>

    <!--Vault Status -->
    <div class="vault-status-section">
      <div class="vault-status-card">
        <div class="card-glow-effect"></div>

        <div class="card-content">
          <div class="status-header">
            <Sparkles class="icon-sm sparkles-icon" />
            <span class="status-title">Vault Status</span>
          </div>

          <div class="locked-funds-section">
            <div class="locked-funds-label">Locked Funds</div>
          </div>

          <h1 class="locked-funds-amount">
            <DollarSign class="icon-lg dollar" />
            <span>1,250.00 THB</span>
          </h1>

          <div class="goal-indicator">
            <Goal class="icon-sm emerald-icon" />
            <span class="text-slate-300"> Goal: Unlock ${{ 100 }}/Day </span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.vault-home-layout {
  width: 100%;
  max-width: 28rem; /* max-w-md */
  margin: 0 auto; /* mx-auto */
  min-height: 100vh;
  color: var(--color-white); /* text-white */
  padding-bottom: 5rem; /* pb-20 (5rem = 80px) */
  position: relative;
  background-color: var(--color-background);
}
.vault-status-card {
  background: linear-gradient(
    to bottom right,
    oklch(0.208 0.042 265.755),
    oklch(0.279 0.041 260.031)
  );
  border-radius: 1rem;
  padding: 1.5rem;
  border: 1px solid oklch(0.372 0.044 257.287);
  box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
  position: relative;
  overflow: hidden;
}
.app-header {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0.4rem 0.4rem; /* py-8 (2rem = 32px), px-4 (1rem = 16px) */
  gap: 1rem; /* gap-4 (1rem = 16px) */
}

.icon-md {
  width: 1.5rem;
  height: 1.5rem;
}
.icon-lg {
  width: 2rem;
  height: 2rem;
}

.vault-status-section {
  padding: 1rem 1rem;
  margin-bottom: 1rem;
  align-items: center;
}
.locked-funds-amount {
  display: flex;
  align-items: center;
  background: linear-gradient(to right, #c084fc, #d8b4fe);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.locked-funds-amount .icon-lg {
  color: #c084fc;
}
.card-content {
  position: relative; /* relative */
}

.status-header {
  display: flex; /* flex */
  align-items: center; /* items-center */
  gap: 0.5rem; /* gap-2 */
  margin-bottom: 1rem; /* mb-4 */
}

.icon-sm {
  width: 1rem;
  height: 1rem;
}

.sparkles-icon {
  color: #c084fc; /* text-purple-400 */
}

.status-title {
  color: #d8b4fe; /* text-purple-300 */
  font-size: 0.875rem; /* text-sm */
}

.locked-funds-section {
  margin-bottom: 1rem; /* mb-4 */
}

.locked-funds-label {
  color: #94a3b8; /* text-slate-400 */
  font-size: 0.875rem; /* text-sm */
  margin-bottom: 0.25rem; /* mb-1 */
}

.emerald-icon {
  color: #34d399; /* text-emerald-400 */
}
.header-icon-bg {
  padding: 0.5rem;
  border-radius: 0.75rem; /* rounded-xl */
  background-image: linear-gradient(
    to bottom right,
    var(--color-purple-600),
    var(--color-pink-500)
  ); /* bg-gradient-to-br from-purple-600 to-pink-600 */
}
.goal-indicator {
  margin: 1rem 0 0 0;
  padding: 0.75rem 0.75rem;
  border-radius: 0.75rem;
  border: var(--color-slate-700) 2px solid;
}
</style>
