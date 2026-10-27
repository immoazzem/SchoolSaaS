<script setup lang="ts">
import { ref } from 'vue'

const invoices = ref([
  { id: 'INV-2026-001', student: 'Zayan Ahmed', class: 'Class 10', amount: '$150.00', type: 'Tuition Fee (October)', status: 'Paid', method: 'bKash Online' },
  { id: 'INV-2026-002', student: 'Nusrat Jahan', class: 'Class 10', amount: '$150.00', type: 'Tuition Fee (October)', status: 'Paid', method: 'Credit Card' },
  { id: 'INV-2026-003', student: 'Tanvir Hossain', class: 'Class 9', amount: '$140.00', type: 'Tuition Fee (October)', status: 'Pending', method: '-' },
  { id: 'INV-2026-004', student: 'Fatima Zohra', class: 'Class 8', amount: '$130.00', type: 'Tuition Fee (October)', status: 'Paid', method: 'Nagad Gateway' },
  { id: 'INV-2026-005', student: 'Arif Mahmud', class: 'Class 10', amount: '$150.00', type: 'Tuition Fee (October)', status: 'Overdue', method: '-' },
])
</script>

<template>
  <div class="space-y-6">
    <div class="flex items-center justify-between">
      <div>
        <h2 class="text-2xl font-black text-slate-900 tracking-tight">Finance & Fee Invoicing</h2>
        <p class="text-xs text-slate-500 mt-1">Multi-tenant automated fee generation, payments, and gateway reconciliation</p>
      </div>
      <button class="px-4 py-2 bg-indigo-600 hover:bg-indigo-700 text-white font-semibold text-xs rounded-lg shadow-sm">
        + Dispatch Bulk Invoices
      </button>
    </div>

    <!-- Revenue overview cards -->
    <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
      <div class="bg-white p-6 rounded-xl border border-slate-200">
        <span class="text-xs font-bold uppercase text-slate-400">Total Billed This Month</span>
        <p class="text-2xl font-black text-slate-900 mt-2">$42,850.00</p>
      </div>
      <div class="bg-white p-6 rounded-xl border border-slate-200">
        <span class="text-xs font-bold uppercase text-emerald-600">Total Collected</span>
        <p class="text-2xl font-black text-emerald-700 mt-2">$38,200.00</p>
      </div>
      <div class="bg-white p-6 rounded-xl border border-slate-200">
        <span class="text-xs font-bold uppercase text-amber-600">Pending / Outstanding</span>
        <p class="text-2xl font-black text-amber-700 mt-2">$4,650.00</p>
      </div>
    </div>

    <!-- Invoices Table -->
    <div class="bg-white rounded-xl border border-slate-200 shadow-sm overflow-hidden">
      <table class="w-full text-left text-xs text-slate-700">
        <thead class="bg-slate-50 text-slate-500 uppercase font-bold border-b border-slate-200">
          <tr>
            <th class="px-6 py-3.5">Invoice #</th>
            <th class="px-6 py-3.5">Student / Class</th>
            <th class="px-6 py-3.5">Fee Category</th>
            <th class="px-6 py-3.5">Amount</th>
            <th class="px-6 py-3.5">Payment Method</th>
            <th class="px-6 py-3.5">Status</th>
            <th class="px-6 py-3.5 text-right">Receipt</th>
          </tr>
        </thead>
        <tbody class="divide-y divide-slate-100 font-medium">
          <tr v-for="inv in invoices" :key="inv.id" class="hover:bg-slate-50 transition">
            <td class="px-6 py-4 font-mono font-bold text-indigo-600">{{ inv.id }}</td>
            <td class="px-6 py-4">
              <p class="font-bold text-slate-900">{{ inv.student }}</p>
              <p class="text-[11px] text-slate-400">{{ inv.class }}</p>
            </td>
            <td class="px-6 py-4">{{ inv.type }}</td>
            <td class="px-6 py-4 font-mono font-extrabold text-slate-900">{{ inv.amount }}</td>
            <td class="px-6 py-4 text-slate-500">{{ inv.method }}</td>
            <td class="px-6 py-4">
              <span 
                :class="{
                  'bg-emerald-50 text-emerald-700 border-emerald-200': inv.status === 'Paid',
                  'bg-amber-50 text-amber-700 border-amber-200': inv.status === 'Pending',
                  'bg-rose-50 text-rose-700 border-rose-200': inv.status === 'Overdue'
                }"
                class="px-2.5 py-1 rounded-full border text-[11px] font-bold"
              >
                {{ inv.status }}
              </span>
            </td>
            <td class="px-6 py-4 text-right">
              <button class="text-indigo-600 font-bold hover:underline">Download PDF</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>
