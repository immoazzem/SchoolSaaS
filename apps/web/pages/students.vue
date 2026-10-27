<script setup lang="ts">
import { ref } from 'vue'

const searchQuery = ref('')
const selectedClass = ref('All')

const students = ref([
  { id: 'STU-1001', name: 'Zayan Ahmed', class: 'Class 10', section: 'A', roll: '01', guardian: 'Kamal Ahmed', phone: '+880 1711-234567', status: 'Active' },
  { id: 'STU-1002', name: 'Nusrat Jahan', class: 'Class 10', section: 'A', roll: '02', guardian: 'Mizanur Rahman', phone: '+880 1712-345678', status: 'Active' },
  { id: 'STU-1003', name: 'Tanvir Hossain', class: 'Class 9', section: 'B', roll: '05', guardian: 'Shahidul Islam', phone: '+880 1813-456789', status: 'Active' },
  { id: 'STU-1004', name: 'Fatima Zohra', class: 'Class 8', section: 'A', roll: '03', guardian: 'Enamul Haque', phone: '+880 1914-567890', status: 'Active' },
  { id: 'STU-1005', name: 'Arif Mahmud', class: 'Class 10', section: 'B', roll: '12', guardian: 'Mahmudur Rahman', phone: '+880 1615-678901', status: 'Inactive' },
])
</script>

<template>
  <div class="space-y-6">
    <div class="flex flex-col sm:flex-row sm:items-center sm:justify-between gap-4">
      <div>
        <h2 class="text-2xl font-black text-slate-900 tracking-tight">Student Directory</h2>
        <p class="text-xs text-slate-500 mt-1">Manage active student admissions, enrollments, and profiles</p>
      </div>
      <div class="flex items-center space-x-3">
        <button class="px-4 py-2 bg-indigo-600 hover:bg-indigo-700 text-white font-semibold text-xs rounded-lg shadow-sm transition">
          + Admit New Student
        </button>
      </div>
    </div>

    <!-- Filters -->
    <div class="bg-white p-4 rounded-xl border border-slate-200 flex flex-wrap gap-4 items-center justify-between">
      <div class="flex items-center space-x-3 w-full sm:w-auto">
        <input 
          v-model="searchQuery"
          type="text" 
          placeholder="Search student name, roll or ID..." 
          class="px-3.5 py-2 border border-slate-300 rounded-lg text-xs w-64 focus:outline-none focus:ring-1 focus:ring-indigo-500"
        />
        <select v-model="selectedClass" class="px-3 py-2 border border-slate-300 rounded-lg text-xs focus:outline-none">
          <option value="All">All Classes</option>
          <option value="Class 10">Class 10</option>
          <option value="Class 9">Class 9</option>
          <option value="Class 8">Class 8</option>
        </select>
      </div>
      <span class="text-xs text-slate-400 font-medium">Showing 5 of 1,420 Enrolled</span>
    </div>

    <!-- Table -->
    <div class="bg-white rounded-xl border border-slate-200 shadow-sm overflow-hidden">
      <table class="w-full text-left text-xs text-slate-700">
        <thead class="bg-slate-50 text-slate-500 uppercase font-bold border-b border-slate-200">
          <tr>
            <th class="px-6 py-3.5">Student ID & Name</th>
            <th class="px-6 py-3.5">Class / Section</th>
            <th class="px-6 py-3.5">Roll No.</th>
            <th class="px-6 py-3.5">Guardian & Contact</th>
            <th class="px-6 py-3.5">Status</th>
            <th class="px-6 py-3.5 text-right">Actions</th>
          </tr>
        </thead>
        <tbody class="divide-y divide-slate-100 font-medium">
          <tr v-for="stu in students" :key="stu.id" class="hover:bg-slate-50/70 transition">
            <td class="px-6 py-4 flex items-center space-x-3">
              <div class="h-8 w-8 rounded-full bg-slate-100 text-indigo-600 font-bold flex items-center justify-center shrink-0">
                {{ stu.name.charAt(0) }}
              </div>
              <div>
                <p class="font-bold text-slate-900">{{ stu.name }}</p>
                <p class="text-[11px] text-slate-400 font-mono">{{ stu.id }}</p>
              </div>
            </td>
            <td class="px-6 py-4">
              <span class="inline-flex px-2 py-0.5 rounded-md bg-slate-100 font-semibold text-slate-800">
                {{ stu.class }} (Sec {{ stu.section }})
              </span>
            </td>
            <td class="px-6 py-4 font-mono font-bold">{{ stu.roll }}</td>
            <td class="px-6 py-4">
              <p class="text-slate-800">{{ stu.guardian }}</p>
              <p class="text-[11px] text-slate-400">{{ stu.phone }}</p>
            </td>
            <td class="px-6 py-4">
              <span 
                :class="stu.status === 'Active' ? 'bg-emerald-50 text-emerald-700 border-emerald-200' : 'bg-slate-100 text-slate-600 border-slate-200'"
                class="px-2 py-0.5 rounded-full border text-[11px] font-semibold"
              >
                {{ stu.status }}
              </span>
            </td>
            <td class="px-6 py-4 text-right space-x-2">
              <button class="text-indigo-600 hover:text-indigo-800 font-bold">Edit</button>
              <button class="text-slate-400 hover:text-slate-600">Profile</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>
