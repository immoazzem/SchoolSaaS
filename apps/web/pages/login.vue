<script setup lang="ts">
import { ref } from 'vue'
import { useAuth } from '~/composables/useAuth'

definePageMeta({
  layout: false
})

const { login } = useAuth()
const router = useRouter()

const email = ref('admin@schoolsaas.io')
const password = ref('password')
const loading = ref(false)
const errorMessage = ref('')

async function handleSubmit() {
  loading.value = true
  errorMessage.value = ''
  try {
    await login(email.value, password.value)
    router.push('/dashboard')
  } catch (err: any) {
    errorMessage.value = err?.data?.message || err?.message || 'Authentication failed. Please verify credentials.'
  } finally {
    loading.value = false
  }
}

function quickFill(userEmail: string) {
  email.value = userEmail
  password.value = 'password'
}
</script>

<template>
  <div class="min-h-screen bg-gradient-to-br from-slate-900 via-indigo-950 to-slate-900 flex items-center justify-center p-6">
    <div class="w-full max-w-md bg-white rounded-2xl shadow-2xl overflow-hidden border border-slate-100">
      <div class="p-8 text-center bg-slate-900 text-white">
        <div class="inline-flex h-12 w-12 rounded-xl bg-gradient-to-tr from-indigo-500 to-violet-500 items-center justify-center font-black text-2xl text-white mb-3 shadow-lg shadow-indigo-500/30">
          S
        </div>
        <h2 class="text-2xl font-extrabold tracking-tight">SchoolSaaS Portal</h2>
        <p class="text-sm text-slate-300 mt-1">Multi-Tenant Institutional Management</p>
      </div>

      <div class="p-8 space-y-6">
        <div v-if="errorMessage" class="p-3 rounded-lg bg-rose-50 border border-rose-200 text-rose-700 text-xs">
          {{ errorMessage }}
        </div>

        <form @submit.prevent="handleSubmit" class="space-y-4">
          <div>
            <label class="block text-xs font-bold uppercase tracking-wider text-slate-600 mb-1">Email Address</label>
            <input 
              v-model="email" 
              type="email" 
              required
              class="w-full px-4 py-2.5 rounded-lg border border-slate-300 text-slate-900 text-sm focus:outline-none focus:ring-2 focus:ring-indigo-600 focus:border-indigo-600"
              placeholder="user@schoolsaas.io"
            />
          </div>

          <div>
            <label class="block text-xs font-bold uppercase tracking-wider text-slate-600 mb-1">Password</label>
            <input 
              v-model="password" 
              type="password" 
              required
              class="w-full px-4 py-2.5 rounded-lg border border-slate-300 text-slate-900 text-sm focus:outline-none focus:ring-2 focus:ring-indigo-600 focus:border-indigo-600"
              placeholder="••••••••"
            />
          </div>

          <button 
            type="submit" 
            :disabled="loading"
            class="w-full py-3 px-4 bg-indigo-600 hover:bg-indigo-700 text-white font-semibold rounded-lg shadow-md shadow-indigo-600/30 transition-all text-sm flex items-center justify-center space-x-2 disabled:opacity-50"
          >
            <span v-if="loading">Authenticating...</span>
            <span v-else>Sign In to Workspace</span>
          </button>
        </form>

        <!-- Quick Demo Switcher -->
        <div class="pt-4 border-t border-slate-100">
          <p class="text-xs font-semibold text-slate-400 uppercase tracking-wider mb-2 text-center">Demo Role Quick-Fill</p>
          <div class="grid grid-cols-2 gap-2 text-xs">
            <button 
              type="button" 
              @click="quickFill('admin@schoolsaas.io')"
              class="p-2 border border-slate-200 rounded-lg hover:border-indigo-500 hover:bg-indigo-50 text-slate-700 font-medium transition text-left"
            >
              👑 <span class="font-bold">Super Admin</span>
            </button>
            <button 
              type="button" 
              @click="quickFill('principal@dhaka-ideal.edu.bd')"
              class="p-2 border border-slate-200 rounded-lg hover:border-indigo-500 hover:bg-indigo-50 text-slate-700 font-medium transition text-left"
            >
              🎓 <span class="font-bold">Principal</span>
            </button>
            <button 
              type="button" 
              @click="quickFill('teacher@dhaka-ideal.edu.bd')"
              class="p-2 border border-slate-200 rounded-lg hover:border-indigo-500 hover:bg-indigo-50 text-slate-700 font-medium transition text-left"
            >
              📝 <span class="font-bold">Teacher</span>
            </button>
            <button 
              type="button" 
              @click="quickFill('student@dhaka-ideal.edu.bd')"
              class="p-2 border border-slate-200 rounded-lg hover:border-indigo-500 hover:bg-indigo-50 text-slate-700 font-medium transition text-left"
            >
              🎒 <span class="font-bold">Student</span>
            </button>
          </div>
        </div>

        <div class="text-center">
          <NuxtLink to="/" class="text-xs text-indigo-600 hover:text-indigo-800 font-medium">
            ← Back to SaaS Public Page
          </NuxtLink>
        </div>
      </div>
    </div>
  </div>
</template>
