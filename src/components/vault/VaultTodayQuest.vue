<script setup lang="ts">
import { CircleDollarSignIcon, Sparkles, TrophyIcon } from 'lucide-vue-next'
</script>

<template>
  <div class="today-quest-section">
    <div class="today-quest-card">
      <div class="card-glow-effect"></div>

      <div class="card-content">
        <!-- Quest Header -->
        <div class="quest-header">
          <div class="quest-header-trophy">
            <TrophyIcon class="icon-md trophy-icon" />
            <span class="quest-title">TODAY'S QUEST</span>
          </div>
          <div class="quest-high-reward">HIGH REWARD</div>
        </div>

        <!-- Quest Description -->
        <div class="quest-description">
          <div class="quest-icon-container">
            <CircleDollarSignIcon />
            <div class="quest-text-container">
              <div class="today-header">Knowledge Quest</div>
              <div class="today-detail">Task: Finish Chapter 5 of 'Atomic Habits'</div>
            </div>
          </div>
          <div class="quest-reward-section">
            <div class="quest-unlocked">
              <Sparkles class="icon-sm sparkles-icon" />
              <span class="unlock-text">Unlock $150</span>
            </div>
          </div>

          <button class="complete-button" true>✓ COMPLETED</button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.quest-header {
  margin: 0 0 1rem 0;
  display: flex;
  gap: 2rem;
  align-items: center;
  .trophy-icon {
    color: var(--color-amber-400);
  }
  .quest-header-trophy {
    font-weight: bold;
    display: flex;
    align-items: center;
    gap: 0.5rem;
  }
  .quest-high-reward {
    background-color: oklch(from var(--color-amber-400) l c h / 0.2); /* 20% opacity */
    color: var(--color-amber-400);
    padding: 0.25rem 0.5rem;
    border-radius: 0.5rem;
    font-size: 0.75rem;
    font-weight: 600;
  }
}
.quest-description {
  border: var(--color-amber-400) 3.5px solid;
  border-radius: 1rem;
  padding: 1.25rem;
  .quest-icon-container {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    margin-bottom: 1rem;
    justify-content: left;

    .today-header {
      font-size: 1.125rem; /* text-lg */
      font-weight: 500;
      margin-bottom: 0.25rem;
      color: var(--color-foreground);
    }

    .today-detail {
      font-size: 0.875rem;
      color: var(--text-color-gray-1);
    }
  }
  .quest-unlocked {
    color: var(--color-amber-400);
    gap: 0.5rem;
    display: flex;
    align-items: center;
  }

  .quest-reward-section {
    margin-bottom: 1rem;
  }
  .unlock-text {
    font-weight: 500;
  }

  .complete-button {
    width: 100%;
    padding: 1rem;
    border-radius: 0.75rem;
    font-weight: 600;
    background-color: var(--color-slate-700);
    color: var(--color-slate-400);
    cursor: not-allowed;
    border: none;
    transition: all 0.2s;
  }

  .complete-button:not(:disabled) {
    background: linear-gradient(to right, var(--color-amber-400), #eab308);
    color: var(--color-slate-900);
    cursor: pointer;
  }

  .complete-button:not(:disabled):active {
    transform: scale(0.95);
  }
}
</style>
