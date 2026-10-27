<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { useAuth } from '~/composables/useAuth'

const { user, selectedSchool } = useAuth()

const stats = ref([
  { name: 'Active Students', value: '1,420', change: '+12%', icon: '👥', color: 'from-blue-500 to-indigo-600' },
  { name: 'Teachers & Staff', value: '78', change: 'Stable', icon: '👩‍🏫', color: 'from-emerald-500 to-teal-600' },
  { name: 'Attendance Rate', value: '96.4%', change: '+1.8%', icon: '📅', color: 'from-amber-500 to-orange-600' },
  { name: 'Monthly Fee Collected', value: '$42,850', change: '+8.2%', icon: '💳', color: 'from-purple-500 to-pink-600' },
])

const recentActivities = [
  { title: 'Class 10-A Final Exam Results Published', time: '10 mins ago', type: 'Exams' },
  { title: 'Monthly Tuition Invoices Dispatched (450 Students)', time: '1 hour ago', type: 'Finance' },
  { title: 'Teacher Attendance Auto-Reconciled', time: '3 hours ago', type: 'Attendance' },
  { title: 'New Student Admission: Tanvir Hasan (ID #2026-089)', time: 'Yesterday', type: 'Admission' },
]
</script>

<template>
  <div class="space-y-8">
    <!-- Header banner -->
    <div class="bg-gradient-to-r from-indigo-900 via-indigo-800 to-slate-900 rounded-2xl p-8 text-white shadow-xl relative overflow-hidden">
      <div class="relative z-10 max-w-2xl">
        <span class="inline-flex items-center px-3 py-1 rounded-full text-xs font-semibold bg-indigo-500/30 text-indigo-200 border border-indigo-400/30 mb-3">
          Academic Year 2026 – Term 2
        </span>
        <h2 class="text-3xl font-extrabold tracking-tight">
          Welcome back, {{ user?.name || 'Administrator' }}!
        </h2>
        <p class="text-slate-300 mt-2 text-sm leading-relaxed">
          Manage institution operations, view real-time student demographics, issue fees, and publish report cards seamlessly.
        </p>
      </div>
      <div class="absolute -right-10 -bottom-10 w-64 h-64 bg-indigo-500/10 rounded-full blur-3xl pointer-events-none"></div>
    </div>

    <!-- Stat cards -->
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
      <div 
        v-for="stat in stats" 
        :key="stat.name"
        class="bg-white rounded-xl p-6 border border-slate-200/80 shadow-sm hover:shadow-md transition-shadow"
      >
        <div class="flex items-center justify-between">
          <span class="text-xs font-bold uppercase tracking-wider text-slate-500">{{ stat.name }}</span>
          <div class="h-10 w-10 rounded-lg flex items-center justify-center text-lg bg-slate-100">
            {{ stat.icon }}
          </div>
        </div>
        <div class="mt-4 flex items-baseline justify-between">
          <span class="text-2xl font-extrabold text-slate-900">{{ stat.value }}</span>
          <span class="text-xs font-semibold text-emerald-600 bg-emerald-50 px-2 py-0.5 rounded-full border border-emerald-200">
            {{ stat.change }}
          </span>
        </div>
      </div>
    </div>

    <!-- Operational Split -->
    <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
      <!-- Quick Action Shortcuts -->
      <div class="lg:col-span-2 bg-white rounded-xl p-6 border border-slate-200 shadow-sm space-y-4">
        <h3 class="text-base font-bold text-slate-900">Institutional Operations</h3>
        <div class="grid grid-cols-2 sm:grid-cols-3 gap-4">
          <NuxtLink 
            to="/classes" 
            class="p-4 rounded-xl border border-slate-200 hover:border-indigo-500 hover:bg-indigo-50/50 transition group flex flex-col items-center text-center space-y-2"
          >
            <span class="text-2xl">🏫</span>
            <span class="text-sm font-semibold text-slate-800 group-hover:text-indigo-600">Classes & Sections</span>
            <span class="text-xs text-slate-400">View hierarchy</span>
          </NuxtLink>

          <NuxtLink 
            to="/students" 
            class="p-4 rounded-xl border border-slate-200 hover:border-indigo-500 hover:bg-indigo-50/50 transition group flex flex-col items-center text-center space-y-2"
          >
            <span class="text-2xl">🎓</span>
            <span class="text-sm font-semibold text-slate-800 group-hover:text-indigo-600">Student Directory</span>
            <span class="text-xs text-slate-400">Manage enrollment</span>
          </NuxtLink>

          <NuxtLink 
            to="/attendance" 
            class="p-4 rounded-xl border border-slate-200 hover:border-indigo-500 hover:bg-indigo-50/50 transition group flex flex-col items-center text-center space-y-2"
          >
            <span class="text-2xl">📋</span>
            <span class="text-sm font-semibold text-slate-800 group-hover:text-indigo-600">Daily Attendance</span>
            <span class="text-xs text-slate-400">Mark & reconcile</span>
          </NuxtLink>

          <NuxtLink 
            to="/finance" 
            class="p-4 rounded-xl border border-slate-200 hover:border-indigo-500 hover:bg-indigo-50/50 transition group flex flex-col items-center text-center space-y-2"
          >
            <span class="text-2xl">💰</span>
            <span class="text-sm font-semibold text-slate-800 group-hover:text-indigo-600">Finance & Fees</span>
            <span class="text-xs text-slate-400">Invoices & gateways</span>
          </NuxtLink>

          <div class="p-4 rounded-xl border border-slate-200 bg-slate-50 flex flex-col items-center text-center space-y-2">
            <span class="text-2xl">📊</span>
            <span class="text-sm font-semibold text-slate-800">Exam Grading</span>
            <span class="text-xs text-slate-400">GPA calculator</span>
          </div>

          <div class="p-4 rounded-xl border border-slate-200 bg-slate-50 flex flex-col items-center text-center space-y-2">
            <span class="text-2xl">⚙️</span>
            <span class="text-sm font-semibold text-slate-800">System Settings</span>
            <span class="text-xs text-slate-400">Multi-tenant config</span>
          </div>
        </div>
      </div>

      <!-- Feed / Audit log -->
      <div class="bg-white rounded-xl p-6 border border-slate-200 shadow-sm">
        <h3 class="text-base font-bold text-slate-900 mb-4">Recent Institutional Logs</h3>
        <ul class="space-y-4">
          <li v-for="(act, idx) in recentActivities" :key="idx" class="flex items-start space-x-3 text-xs">
            <div class="h-2 w-2 rounded-full bg-indigo-600 mt-1.5 shrink-0"></div>
            <div>
              <p class="font-medium text-slate-800">{{ act.title }}</p>
              <div class="flex items-center space-x-2 mt-0.5 text-slate-400">
                <span>{{ act.type }}</span>
                <span>•</span>
                <span>{{ act.time }}</span>
              </div>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>
