<script setup lang="ts">
import { ref } from 'vue'
import { useAuth } from '~/composables/useAuth'

const { user, selectedSchool, schools, selectSchool, logout } = useAuth()
const router = useRouter()

const navLinks = [
  { label: 'Dashboard', path: '/dashboard', icon: 'M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6' },
  { label: 'Classes & Sections', path: '/classes', icon: 'M19 11H5m14 0a2 2 0 012 2v6a2 2 0 01-2 2H5a2 2 0 01-2-2v-6a2 2 0 012-2m14 0V9a2 2 0 00-2-2M5 11V9a2 2 0 012-2m0 0V5a2 2 0 012-2h6a2 2 0 012 2v2M7 7h10' },
  { label: 'Students', path: '/students', icon: 'M12 4.354a4 4 0 110 5.292M15 21H3v-1a6 6 0 0112 0v1zm0 0h6v-1a6 6 0 00-9-5.197M13 7a4 4 0 11-8 0 4 4 0 018 0z' },
  { label: 'Attendance', path: '/attendance', icon: 'M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2m-6 9l2 2 4-4' },
  { label: 'Finance & Fees', path: '/finance', icon: 'M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.599-1M21 12a9 9 0 11-18 0 9 9 0 0118 0z' },
]

async function handleLogout() {
  await logout()
  router.push('/login')
}
</script>

<template>
  <div class="min-h-screen bg-slate-50 flex">
    <!-- Sidebar -->
    <aside class="w-64 bg-slate-900 text-slate-100 flex flex-col justify-between shrink-0 shadow-xl border-r border-slate-800">
      <div>
        <div class="p-6 border-b border-slate-800 flex items-center space-x-3">
          <div class="h-10 w-10 rounded-xl bg-gradient-to-tr from-indigo-600 to-violet-500 flex items-center justify-center font-black text-white text-xl shadow-lg shadow-indigo-500/20">
            S
          </div>
          <div>
            <h1 class="font-extrabold text-white text-base tracking-tight">SchoolSaaS</h1>
            <p class="text-xs text-indigo-400 font-medium">Enterprise Cloud</p>
          </div>
        </div>

        <!-- Tenant Selector -->
        <div class="p-4 border-b border-slate-800/80 bg-slate-950/40">
          <label class="block text-xs font-semibold uppercase tracking-wider text-slate-400 mb-1.5">Active Institution</label>
          <select 
            :value="selectedSchool?.id"
            @change="selectSchool(Number(($event.target as HTMLSelectElement).value))"
            class="w-full bg-slate-800 text-slate-100 text-sm font-medium rounded-lg px-3 py-2 border border-slate-700 focus:outline-none focus:border-indigo-500 focus:ring-1 focus:ring-indigo-500"
          >
            <option v-for="school in schools" :key="school.id" :value="school.id">
              {{ school.name }}
            </option>
            <option v-if="!schools.length" :value="null">Demo Academy</option>
          </select>
        </div>

        <!-- Navigation Links -->
        <nav class="p-4 space-y-1">
          <NuxtLink
            v-for="link in navLinks"
            :key="link.path"
            :to="link.path"
            active-class="bg-indigo-600 text-white font-semibold shadow-md shadow-indigo-600/30"
            class="flex items-center space-x-3 px-3.5 py-2.5 rounded-lg text-sm text-slate-300 hover:bg-slate-800 hover:text-white transition-colors"
          >
            <svg class="h-5 w-5 shrink-0 opacity-80" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" :d="link.icon" />
            </svg>
            <span>{{ link.label }}</span>
          </NuxtLink>
        </nav>
      </div>

      <!-- User footer -->
      <div class="p-4 border-t border-slate-800 bg-slate-950/30 flex items-center justify-between">
        <div class="flex items-center space-x-3 truncate">
          <div class="h-9 w-9 rounded-full bg-indigo-700 flex items-center justify-center text-white font-bold text-sm shrink-0">
            {{ user?.name ? user.name.charAt(0) : 'A' }}
          </div>
          <div class="truncate">
            <p class="text-sm font-medium text-white truncate">{{ user?.name || 'Administrator' }}</p>
            <p class="text-xs text-slate-400 truncate">{{ user?.email || 'admin@schoolsaas.io' }}</p>
          </div>
        </div>
        <button
          @click="handleLogout"
          title="Sign out"
          class="p-2 text-slate-400 hover:text-rose-400 hover:bg-slate-800 rounded-lg transition-colors"
        >
          <svg class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 16l4-4m0 0l-4-4m4 4H7m6 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h4a3 3 0 013 3v1" />
          </svg>
        </button>
      </div>
    </aside>

    <!-- Main Content Area -->
    <main class="flex-1 flex flex-col min-w-0 overflow-y-auto">
      <header class="h-16 bg-white border-b border-slate-200 px-8 flex items-center justify-between shadow-sm sticky top-0 z-10">
        <div class="flex items-center space-x-3">
          <span class="inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-semibold bg-emerald-100 text-emerald-800 border border-emerald-200">
            Live Tenant: {{ selectedSchool?.name || 'Dhaka Ideal Academy' }}
          </span>
          <span class="text-xs text-slate-400">|</span>
          <span class="text-xs text-slate-500 font-mono">Laravel 13 API Connected</span>
        </div>

        <div class="flex items-center space-x-4">
          <NuxtLink to="/" class="text-xs font-medium text-slate-500 hover:text-indigo-600 transition-colors">
            Public Website
          </NuxtLink>
        </div>
      </header>

      <div class="p-8">
        <slot />
      </div>
    </main>
  </div>
</template>
