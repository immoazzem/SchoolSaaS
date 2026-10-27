<script setup lang="ts">
import { ref } from 'vue'

const classes = ref([
  { id: 1, name: 'Class 10', code: 'CLS-10', sections: ['A', 'B', 'Science', 'Commerce'], students: 160, status: 'Active' },
  { id: 2, name: 'Class 9', code: 'CLS-09', sections: ['A', 'B'], students: 155, status: 'Active' },
  { id: 3, name: 'Class 8', code: 'CLS-08', sections: ['A', 'B', 'C'], students: 180, status: 'Active' },
  { id: 4, name: 'Class 7', code: 'CLS-07', sections: ['A', 'B'], students: 140, status: 'Active' },
  { id: 5, name: 'Class 6', code: 'CLS-06', sections: ['A', 'B'], students: 135, status: 'Active' },
])
</script>

<template>
  <div class="space-y-6">
    <div class="flex items-center justify-between">
      <div>
        <h2 class="text-2xl font-black text-slate-900 tracking-tight">Academic Classes & Sections</h2>
        <p class="text-xs text-slate-500 mt-1">Configure academic hierarchy, class subjects, and sections</p>
      </div>
      <button class="px-4 py-2 bg-indigo-600 hover:bg-indigo-700 text-white font-semibold text-xs rounded-lg shadow-sm">
        + Create Class
      </button>
    </div>

    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
      <div 
        v-for="c in classes" 
        :key="c.id" 
        class="bg-white rounded-xl p-6 border border-slate-200/90 shadow-sm hover:shadow-md transition space-y-4"
      >
        <div class="flex items-center justify-between">
          <div>
            <h3 class="text-lg font-extrabold text-slate-900">{{ c.name }}</h3>
            <span class="text-xs font-mono text-slate-400 font-medium">{{ c.code }}</span>
          </div>
          <span class="px-2.5 py-0.5 rounded-full text-[11px] font-bold bg-emerald-50 text-emerald-700 border border-emerald-200">
            {{ c.status }}
          </span>
        </div>

        <div>
          <p class="text-xs font-semibold text-slate-500 uppercase tracking-wider mb-2">Sections</p>
          <div class="flex flex-wrap gap-1.5">
            <span 
              v-for="sec in c.sections" 
              :key="sec"
              class="px-2 py-1 bg-slate-100 hover:bg-indigo-50 hover:text-indigo-600 text-slate-700 rounded text-xs font-semibold cursor-pointer transition"
            >
              Section {{ sec }}
            </span>
          </div>
        </div>

        <div class="pt-3 border-t border-slate-100 flex items-center justify-between text-xs text-slate-500">
          <span>👥 <strong class="text-slate-800">{{ c.students }}</strong> Total Students</span>
          <button class="text-indigo-600 font-bold hover:underline">Manage Subjects →</button>
        </div>
      </div>
    </div>
  </div>
</template>
