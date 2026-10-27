<script setup lang="ts">
import { ref } from 'vue'

const attendanceDate = ref(new Date().toISOString().split('T')[0])
const selectedClass = ref('Class 10-A')

const records = ref([
  { roll: '01', name: 'Zayan Ahmed', status: 'Present', time: '07:54 AM' },
  { roll: '02', name: 'Nusrat Jahan', status: 'Present', time: '07:58 AM' },
  { roll: '03', name: 'Tanvir Hossain', status: 'Late', time: '08:16 AM' },
  { roll: '04', name: 'Fatima Zohra', status: 'Present', time: '07:49 AM' },
  { roll: '05', name: 'Arif Mahmud', status: 'Absent', time: '-' },
])

function setStatus(idx: number, status: string) {
  records.value[idx].status = status
}
</script>

<template>
  <div class="space-y-6">
    <div class="flex flex-col sm:flex-row sm:items-center sm:justify-between gap-4">
      <div>
        <h2 class="text-2xl font-black text-slate-900 tracking-tight">Daily Student Attendance</h2>
        <p class="text-xs text-slate-500 mt-1">Real-time attendance ledger with biometric & manual punch reconciliation</p>
      </div>
      <div class="flex items-center space-x-3">
        <button class="px-4 py-2 bg-emerald-600 hover:bg-emerald-700 text-white font-semibold text-xs rounded-lg shadow-sm">
          ✓ Save Attendance
        </button>
      </div>
    </div>

    <!-- Date & Class filter bar -->
    <div class="bg-white p-4 rounded-xl border border-slate-200 flex flex-wrap gap-4 items-center justify-between">
      <div class="flex items-center space-x-3">
        <div>
          <label class="block text-[10px] font-bold uppercase text-slate-400 mb-0.5">Date</label>
          <input v-model="attendanceDate" type="date" class="px-3 py-1.5 border border-slate-300 rounded-lg text-xs" />
        </div>
        <div>
          <label class="block text-[10px] font-bold uppercase text-slate-400 mb-0.5">Class / Section</label>
          <select v-model="selectedClass" class="px-3 py-1.5 border border-slate-300 rounded-lg text-xs">
            <option>Class 10-A</option>
            <option>Class 10-B</option>
            <option>Class 9-A</option>
          </select>
        </div>
      </div>

      <!-- Quick summary pills -->
      <div class="flex items-center space-x-2 text-xs">
        <span class="px-2.5 py-1 bg-emerald-100 text-emerald-800 rounded-md font-bold">3 Present</span>
        <span class="px-2.5 py-1 bg-amber-100 text-amber-800 rounded-md font-bold">1 Late</span>
        <span class="px-2.5 py-1 bg-rose-100 text-rose-800 rounded-md font-bold">1 Absent</span>
      </div>
    </div>

    <!-- Attendance Table -->
    <div class="bg-white rounded-xl border border-slate-200 shadow-sm overflow-hidden">
      <table class="w-full text-left text-xs text-slate-700">
        <thead class="bg-slate-50 text-slate-500 uppercase font-bold border-b border-slate-200">
          <tr>
            <th class="px-6 py-3.5">Roll</th>
            <th class="px-6 py-3.5">Student Name</th>
            <th class="px-6 py-3.5">Punch Timestamp</th>
            <th class="px-6 py-3.5">Attendance Status</th>
            <th class="px-6 py-3.5 text-right">Quick Mark</th>
          </tr>
        </thead>
        <tbody class="divide-y divide-slate-100 font-medium">
          <tr v-for="(rec, idx) in records" :key="rec.roll" class="hover:bg-slate-50 transition">
            <td class="px-6 py-4 font-mono font-bold">{{ rec.roll }}</td>
            <td class="px-6 py-4 font-bold text-slate-900">{{ rec.name }}</td>
            <td class="px-6 py-4 text-slate-500 font-mono">{{ rec.time }}</td>
            <td class="px-6 py-4">
              <span 
                :class="{
                  'bg-emerald-50 text-emerald-700 border-emerald-200': rec.status === 'Present',
                  'bg-amber-50 text-amber-700 border-amber-200': rec.status === 'Late',
                  'bg-rose-50 text-rose-700 border-rose-200': rec.status === 'Absent'
                }"
                class="px-2.5 py-1 rounded-full border text-[11px] font-bold"
              >
                {{ rec.status }}
              </span>
            </td>
            <td class="px-6 py-4 text-right space-x-1.5">
              <button @click="setStatus(idx, 'Present')" class="px-2.5 py-1 bg-emerald-50 text-emerald-700 hover:bg-emerald-600 hover:text-white rounded text-xs font-semibold transition">P</button>
              <button @click="setStatus(idx, 'Late')" class="px-2.5 py-1 bg-amber-50 text-amber-700 hover:bg-amber-600 hover:text-white rounded text-xs font-semibold transition">L</button>
              <button @click="setStatus(idx, 'Absent')" class="px-2.5 py-1 bg-rose-50 text-rose-700 hover:bg-rose-600 hover:text-white rounded text-xs font-semibold transition">A</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>
