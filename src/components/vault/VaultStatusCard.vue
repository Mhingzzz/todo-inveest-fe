<script setup lang="ts">
import { DollarSign, Goal, Sparkles } from 'lucide-vue-next'

defineProps<{
  lockedAmount: number
  goalAmount: number
  currency?: string
}>()
</script>

<template>
  <div class="vault-status-section">
    <div class="vault-status-card">
      <div class="card-glow-effect"></div>

      <div class="card-content">
        <!-- Status Header -->
        <div class="status-header">
          <Sparkles class="icon-sm sparkles-icon" />
          <span class="status-title">Vault Status</span>
        </div>

        <!-- Locked Funds Label -->
        <div class="locked-funds-section">
          <div class="locked-funds-label">Locked Funds</div>
        </div>

        <!-- Amount Display -->
        <h1 class="locked-funds-amount">
          <DollarSign class="icon-lg dollar" />
          <span
            >{{
              lockedAmount.toLocaleString('en-US', {
                minimumFractionDigits: 2,
                maximumFractionDigits: 2,
              })
            }}
            {{ currency || 'THB' }}</span
          >
        </h1>

        <!-- Goal Indicator -->
        <div class="goal-indicator">
          <Goal class="icon-sm emerald-icon" />
          <span class="goal-text">Goal: Unlock ${{ goalAmount }}/Day</span>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.vault-status-section {
  padding: 1rem;
  margin-bottom: 1rem;
  align-items: center;
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

.card-glow-effect {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: radial-gradient(circle at top left, rgba(192, 132, 252, 0.1), transparent);
  pointer-events: none;
}

.card-content {
  position: relative;
}

.status-header {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  margin-bottom: 1rem;
}

.sparkles-icon {
  color: #c084fc;
}

.status-title {
  color: #d8b4fe;
  font-size: 0.875rem;
}

.locked-funds-section {
  margin-bottom: 1rem;
}

.locked-funds-label {
  color: #94a3b8;
  font-size: 0.875rem;
  margin-bottom: 0.25rem;
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

.emerald-icon {
  color: #34d399;
}

.goal-indicator {
  margin: 1rem 0 0 0;
  padding: 0.75rem;
  border-radius: 0.75rem;
  border: var(--color-slate-700) 2px solid;
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.goal-text {
  color: var(--text-color-gray-1);
}
</style>
