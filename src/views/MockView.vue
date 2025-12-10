<script setup lang="ts">
import {
  Lock,
  Sparkles,
  Dumbbell,
  Brain,
  Coffee,
  Home,
  Trophy,
  Target,
  User,
} from 'lucide-vue-next' // ต้องเปลี่ยนมาใช้ lucide-vue-next แทน lucide-react
import { ref, computed } from 'vue' // ใช้ ref และ computed สำหรับ Vue

// Logic (State และ Functions) ยังคงคล้ายเดิม แต่ใช้ Vue Composition API
interface Quest {
  id: string
  icon: string
  title: string
  task: string
  reward: number
  category: 'knowledge' | 'health' | 'saving'
  isHighlight?: boolean
  completed?: boolean
}

const lockedFunds = ref(4200)
const dailyGoal = ref(200)
const quests = ref<Quest[]>([
  {
    id: '1',
    icon: '💰',
    title: 'Knowledge Quest',
    task: "Finish Chapter 5 of 'Atomic Habits'",
    reward: 150,
    category: 'knowledge',
    isHighlight: true,
  },
  {
    id: '2',
    icon: '🏋️',
    title: 'Health Quest',
    task: '30 Minute Yoga',
    reward: 50,
    category: 'health',
  },
  {
    id: '3',
    icon: '💡',
    title: 'Knowledge Quest',
    task: 'Solve 5 LeetCode Problems',
    reward: 100,
    category: 'knowledge',
  },
  {
    id: '4',
    icon: '☕',
    title: 'Saving Quest',
    task: 'Brew Coffee at Home',
    reward: 20,
    category: 'saving',
  },
])

const handleCompleteQuest = (questId: string) => {
  quests.value = quests.value.map((q) => (q.id === questId ? { ...q, completed: true } : q))
}

const getCategoryColor = (category: string) => {
  switch (category) {
    case 'knowledge':
      return 'quest-knowledge-gradient'
    case 'health':
      return 'quest-health-gradient'
    case 'saving':
      return 'quest-saving-gradient'
    default:
      return 'quest-default-gradient'
  }
}

const highlightedQuest = computed(() => quests.value.filter((q) => q.isHighlight))
const remainingQuests = computed(() => quests.value.filter((q) => !q.isHighlight))
</script>

<template>
  <div class="vault-home-layout">
    <header class="app-header">
      <div class="flex items-center gap-3">
        <div class="header-icon-bg">
          <Lock class="icon-lg" />
        </div>
        <h1 class="text-xl">The Earned Spend Vault</h1>
      </div>
    </header>

    <div class="px-6 mb-6">
      <div class="vault-status-card">
        <div class="card-glow-effect"></div>

        <div class="relative">
          <div class="flex items-center gap-2 mb-4">
            <Sparkles class="icon-sm text-purple-400" />
            <span class="text-purple-300 text-sm">Vault Status</span>
          </div>

          <div class="mb-4">
            <div class="text-slate-400 text-sm mb-1">Locked Funds</div>
            <div class="locked-funds-amount">${{ lockedFunds.toLocaleString() }}</div>
          </div>

          <div class="goal-indicator">
            <Target class="icon-sm text-emerald-400" />
            <span class="text-slate-300"> Goal: Unlock ${{ dailyGoal }}/Day </span>
          </div>
        </div>
      </div>
    </div>

    <div class="px-6 mb-4">
      <div class="flex items-center gap-2 mb-3">
        <Trophy class="icon-sm text-amber-400" />
        <h2 class="text-lg text-slate-200">TODAY&apos;S QUESTS</h2>
        <span class="high-reward-badge"> HIGH REWARD </span>
      </div>

      <div
        v-for="quest in highlightedQuest"
        :key="quest.id"
        :class="[
          'highlight-quest-wrapper',
          getCategoryColor(quest.category),
          { 'animate-pulse-slow': !quest.completed },
        ]"
      >
        <div class="highlight-quest-inner">
          <div class="flex items-start gap-3 mb-4">
            <span class="text-3xl">{{ quest.icon }}</span>
            <div class="flex-1">
              <h3 class="text-lg mb-1">{{ quest.title }}</h3>
              <p class="text-slate-300 text-sm">Task: {{ quest.task }}</p>
            </div>
          </div>

          <div class="flex items-center justify-between mb-4">
            <div class="flex items-center gap-2">
              <Sparkles class="icon-xs text-amber-400" />
              <span class="text-amber-400"> Unlock ${{ quest.reward }} </span>
            </div>
          </div>

          <button
            @click="handleCompleteQuest(quest.id)"
            :disabled="quest.completed"
            :class="[
              'highlight-quest-button',
              { 'completed-button': quest.completed, 'pending-button': !quest.completed },
            ]"
          >
            {{ quest.completed ? '✓ COMPLETED' : 'COMPLETE & EARN' }}
          </button>
        </div>
      </div>
    </div>

    <div class="px-6 mb-6">
      <h3 class="text-slate-400 text-sm mb-3">QUEST LIST</h3>
      <div class="quest-list-container">
        <div v-for="quest in remainingQuests" :key="quest.id" class="normal-quest-card">
          <div class="flex items-start gap-3 mb-3">
            <span class="text-2xl">{{ quest.icon }}</span>
            <div class="flex-1">
              <h4 class="text-slate-200 mb-1">{{ quest.title }}</h4>
              <p class="text-slate-400 text-sm">{{ quest.task }}</p>
            </div>
          </div>

          <div class="flex items-center justify-between">
            <div class="flex items-center gap-2">
              <Sparkles class="icon-xs text-emerald-400" />
              <span class="text-emerald-400 text-sm"> Unlock ${{ quest.reward }} </span>
            </div>
            <button
              @click="handleCompleteQuest(quest.id)"
              :disabled="quest.completed"
              :class="[
                'normal-quest-button',
                { 'completed-button-sm': quest.completed, 'pending-button-sm': !quest.completed },
              ]"
            >
              {{ quest.completed ? 'Done' : 'Complete' }}
            </button>
          </div>
        </div>
      </div>
    </div>

    <nav class="bottom-nav">
      <div class="max-w-md mx-auto px-6 py-4">
        <div class="flex items-center justify-around">
          <button class="nav-button active">
            <div class="nav-icon-bg">
              <Home class="icon-lg" />
            </div>
            <span class="text-xs">Vault</span>
          </button>
          <button class="nav-button inactive">
            <Trophy class="icon-lg" />
            <span class="text-xs">Quests</span>
          </button>
          <button class="nav-button inactive">
            <Target class="icon-lg" />
            <span class="text-xs">Goals</span>
          </button>
          <button class="nav-button inactive">
            <User class="icon-lg" />
            <span class="text-xs">Profile</span>
          </button>
        </div>
      </div>
    </nav>
  </div>
</template>

<style scoped>
/* =======================================
   1. GLOBAL LAYOUT & COLORS
   ======================================= */
/* ค่าสีเหล่านี้มาจากตัวแปร CSS ใน example/src/index.css และถูกใช้ใน Tailwind */
/* ใน Vue/CSS ธรรมดา เราต้องกำหนดค่าสีเอง หรือใช้ตัวแปรที่มีอยู่จาก base.css/globals.css */

.vault-home-layout {
  width: 100%;
  max-width: 28rem; /* max-w-md */
  margin: 0 auto; /* mx-auto */
  min-height: 100vh;
  background-color: var(--color-slate-950); /* bg-slate-950 */
  color: var(--color-white); /* text-white */
  padding-bottom: 5rem; /* pb-20 (5rem = 80px) */
  position: relative;
}

.app-header {
  padding: 2rem 1.5rem 1.5rem 1.5rem; /* pt-8 pb-6 px-6 (8*4=32px, 6*4=24px) */
}

/* Icon Sizing (W-6 H-6) */
.icon-lg {
  width: 1.5rem;
  height: 1.5rem;
}
.icon-sm {
  width: 1.25rem;
  height: 1.25rem;
}
.icon-xs {
  width: 1rem;
  height: 1rem;
}

/* =======================================
   2. VAULT STATUS CARD (StatCard)
   ======================================= */

.header-icon-bg {
  padding: 0.5rem;
  border-radius: 0.75rem; /* rounded-xl */
  background-image: linear-gradient(
    to bottom right,
    var(--color-purple-600),
    var(--color-pink-600)
  ); /* bg-gradient-to-br from-purple-600 to-pink-600 */
}

.vault-status-card {
  background-image: linear-gradient(
    to bottom right,
    var(--color-slate-900),
    var(--color-slate-800)
  ); /* bg-gradient-to-br from-slate-900 to-slate-800 */
  border-radius: 1rem; /* rounded-2xl (16px) */
  padding: 1.5rem; /* p-6 */
  border: 1px solid var(--color-slate-700); /* border border-slate-700 */
  box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.4); /* shadow-2xl */
  position: relative;
  overflow: hidden;
}

.card-glow-effect {
  position: absolute;
  top: 0;
  right: 0;
  width: 8rem; /* w-32 */
  height: 8rem; /* h-32 */
  background-color: color-mix(
    in srgb,
    var(--color-purple-600) 20%,
    transparent
  ); /* bg-purple-600/20 */
  border-radius: 9999px; /* rounded-full */
  filter: blur(64px); /* blur-3xl */
}

.locked-funds-amount {
  font-size: 2.25rem; /* text-4xl */
  background-image: linear-gradient(
    to right,
    var(--color-purple-400),
    var(--color-pink-400)
  ); /* bg-gradient-to-r from-purple-400 to-pink-400 */
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
}

.goal-indicator {
  display: flex;
  align-items: center;
  gap: 0.5rem; /* gap-2 */
  background-color: color-mix(
    in srgb,
    var(--color-slate-800) 50%,
    transparent
  ); /* bg-slate-800/50 */
  border-radius: 0.5rem; /* rounded-lg */
  padding: 0.75rem; /* p-3 */
  border: 1px solid var(--color-slate-700);
}

/* =======================================
   3. QUESTS SECTION
   ======================================= */

.high-reward-badge {
  font-size: 0.75rem; /* text-xs */
  color: var(--color-amber-400); /* text-amber-400 */
  background-color: color-mix(
    in srgb,
    var(--color-amber-400) 10%,
    transparent
  ); /* bg-amber-400/10 */
  padding: 0.25rem 0.5rem; /* px-2 py-1 */
  border-radius: 9999px; /* rounded-full */
}

/* Highlight Quest Card (Outer Gradient Border) */
.highlight-quest-wrapper {
  border-radius: 1rem; /* rounded-2xl */
  padding: 0.25rem; /* p-1 (Creates the border effect) */
  margin-bottom: 1rem; /* mb-4 */
  box-shadow:
    0 10px 15px -3px rgba(255, 193, 7, 0.2),
    0 4px 6px -4px rgba(255, 193, 7, 0.2); /* shadow-lg shadow-amber-500/20 (Approximation) */
}

.highlight-quest-inner {
  background-color: var(--color-slate-900); /* bg-slate-900 */
  border-radius: 0.75rem; /* rounded-xl */
  padding: 1.25rem; /* p-5 */
}

/* Quest Category Gradients */
.quest-knowledge-gradient {
  background-image: linear-gradient(
    to bottom right,
    var(--color-amber-500),
    var(--color-yellow-500)
  ); /* from-amber-500 to-yellow-500 */
}
.quest-health-gradient {
  background-image: linear-gradient(
    to bottom right,
    var(--color-emerald-500),
    var(--color-green-500)
  ); /* from-emerald-500 to-green-500 */
}
.quest-saving-gradient {
  background-image: linear-gradient(
    to bottom right,
    var(--color-blue-500),
    var(--color-cyan-500)
  ); /* from-blue-500 to-cyan-500 */
}

/* Quest Button - Highlight */
.highlight-quest-button {
  width: 100%;
  padding: 1rem 0; /* py-4 */
  border-radius: 0.75rem; /* rounded-xl */
  transition: all 0.2s; /* transition-all */
  transform: scale(1); /* transform */
}

.highlight-quest-button:active {
  transform: scale(0.95); /* active:scale-95 */
}

.pending-button {
  background-image: linear-gradient(
    to right,
    var(--color-amber-500),
    var(--color-yellow-500)
  ); /* bg-gradient-to-r from-amber-500 to-yellow-500 */
  color: var(--color-slate-900); /* text-slate-900 */
  box-shadow: 0 10px 15px -3px rgba(255, 193, 7, 0.3); /* shadow-lg shadow-amber-500/30 */
}

.completed-button {
  background-color: var(--color-slate-700); /* bg-slate-700 */
  color: var(--color-slate-400); /* text-slate-400 */
  cursor: not-allowed;
}

/* =======================================
   4. QUEST LIST
   ======================================= */

.quest-list-container {
  display: flex;
  flex-direction: column;
  gap: 0.75rem; /* space-y-3 */
}

.normal-quest-card {
  background-color: var(--color-slate-900); /* bg-slate-900 */
  border: 1px solid var(--color-slate-800); /* border border-slate-800 */
  border-radius: 0.75rem; /* rounded-xl */
  padding: 1rem; /* p-4 */
  transition: border-color 0.2s; /* transition-colors */
}
.normal-quest-card:hover {
  border-color: var(--color-slate-700); /* hover:border-slate-700 */
}

/* Quest Button - Normal */
.normal-quest-button {
  padding: 0.5rem 1rem; /* px-4 py-2 */
  border-radius: 0.5rem; /* rounded-lg */
  font-size: 0.875rem; /* text-sm */
  transition: all 0.2s; /* transition-all */
}

.pending-button-sm {
  background-image: linear-gradient(
    to right,
    var(--color-emerald-600),
    var(--color-green-600)
  ); /* bg-gradient-to-r from-emerald-600 to-green-600 */
  color: var(--color-white); /* text-white */
}
.pending-button-sm:hover {
  background-image: linear-gradient(
    to right,
    var(--color-emerald-500),
    var(--color-green-500)
  ); /* hover:from-emerald-500 hover:to-green-500 */
}

.completed-button-sm {
  background-color: var(--color-slate-800); /* bg-slate-800 */
  color: var(--color-slate-500); /* text-slate-500 */
  cursor: not-allowed;
}

/* =======================================
   5. BOTTOM NAVIGATION
   ======================================= */

.bottom-nav {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: color-mix(
    in srgb,
    var(--color-slate-900) 95%,
    transparent
  ); /* bg-slate-900/95 */
  backdrop-filter: blur(16px); /* backdrop-blur-lg */
  border-top: 1px solid var(--color-slate-800); /* border-t border-slate-800 */
  z-index: 10;
}

.bottom-nav .max-w-md {
  max-width: 28rem;
  margin: 0 auto;
  padding: 1rem 1.5rem; /* py-4 px-6 */
}

.nav-button {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.25rem; /* gap-1 */
  transition: color 0.2s;
  background: none;
  border: none;
  cursor: pointer;
}

.nav-button.active {
  color: var(--color-purple-400); /* text-purple-400 */
}

.nav-button.inactive {
  color: var(--color-slate-500); /* text-slate-500 */
}
.nav-button.inactive:hover {
  color: var(--color-slate-300); /* hover:text-slate-300 */
}

.nav-icon-bg {
  padding: 0.5rem; /* p-2 */
  border-radius: 0.75rem; /* rounded-xl */
  background-color: color-mix(
    in srgb,
    var(--color-purple-600) 20%,
    transparent
  ); /* bg-purple-600/20 */
}

/* Animation from globals.css */
@keyframes pulse-slow {
  0%,
  100% {
    opacity: 1;
  }
  50% {
    opacity: 0.95;
  }
}
.animate-pulse-slow {
  animation: pulse-slow 2s cubic-bezier(0.4, 0, 0.6, 1) infinite;
}
</style>
