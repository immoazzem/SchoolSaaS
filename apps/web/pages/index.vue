<script lang="ts" setup>
definePageMeta({
  layout: 'blank',
  public: true,
})

const session = useSession()

const pricingTiers = [
  {
    name: 'Starter School',
    price: '$29',
    period: '/month',
    description: 'Perfect for single branch primary or secondary schools getting started.',
    features: [
      'Up to 500 Students',
      'Full Academic & Class Management',
      'Daily Student & Staff Attendance',
      'Basic Fee Collection & Receipts',
      'Parent & Student Mobile Portals',
      'Email Support',
    ],
    highlight: false,
    cta: 'Start Free Trial',
  },
  {
    name: 'School Pro',
    price: '$89',
    period: '/month',
    description: 'For growing institutions that need automated billing, exams, and payroll.',
    features: [
      'Up to 2,500 Students',
      'Automated Invoicing & SMS Alerts',
      'Exam Scheduling & GPA Engine',
      'Employee Payroll & Leave Approvals',
      'Digital Fee Gateways (bKash, Cards)',
      'Offline-First Progressive Web App',
      'Priority 24/7 Support',
    ],
    highlight: true,
    cta: 'Get Started with Pro',
  },
  {
    name: 'Multi-Campus Enterprise',
    price: '$249',
    period: '/month',
    description: 'Complete operational mastery for educational trusts and campus networks.',
    features: [
      'Unlimited Students & Staff',
      'Unlimited School Branches / Campuses',
      'Custom Role & Fine-Grained RBAC',
      'Full Audit Logging & Data Export',
      'Dedicated Database Instance Option',
      'Custom Domain & Subdomain Mapping',
      'Dedicated Account Manager',
    ],
    highlight: false,
    cta: 'Contact Sales',
  },
]

const features = [
  {
    icon: 'tabler-building',
    title: 'Multi-Campus Multi-Tenancy',
    desc: 'Run 1 or 100 schools under isolated databases with zero cross-tenant data leakage and custom school domains.',
  },
  {
    icon: 'tabler-user-check',
    title: 'Smart Attendance & Late Tracking',
    desc: 'Instant QR / roster attendance with late arrival tracking, half-day records, and instant SMS alerts to parents.',
  },
  {
    icon: 'tabler-receipt-2',
    title: 'Automated Billing & Gateways',
    desc: 'Generate monthly invoices in bulk, apply student discounts, and collect payments via bKash, Nagad, Stripe, or cash.',
  },
  {
    icon: 'tabler-award',
    title: 'Exams, GPA & Marks Management',
    desc: 'Customizable grade scales (Bangladesh 5.0 GPA & Letter Grades), exam schedules, teacher verification, and marksheet PDFs.',
  },
  {
    icon: 'tabler-device-mobile',
    title: 'Student & Parent Portals',
    desc: 'Transparent access for parents and students to view report cards, fee dues, attendance percentage, and notices on any device.',
  },
  {
    icon: 'tabler-wifi-off',
    title: 'Offline-First Resilience (PWA)',
    desc: 'Keep recording attendance and grades even during network drops. Queued mutations automatically sync upon reconnecting.',
  },
]
</script>

<template>
  <div class="landing-page min-h-screen bg-slate-950 text-slate-100 selection:bg-blue-600 selection:text-white">
    <!-- Navigation Bar -->
    <header class="sticky top-0 z-50 border-b border-slate-800/80 bg-slate-950/80 backdrop-blur-md">
      <div class="mx-auto flex max-w-7xl items-center justify-between px-6 py-4">
        <div class="flex items-center gap-3">
          <div class="flex h-10 w-10 items-center justify-center rounded-xl bg-gradient-to-tr from-blue-600 to-indigo-500 font-bold text-white shadow-lg shadow-blue-500/25">
            SS
          </div>
          <div>
            <span class="text-xl font-bold tracking-tight text-white">School<span class="text-blue-500">SaaS</span></span>
            <span class="ml-2 rounded-full border border-blue-500/30 bg-blue-500/10 px-2 py-0.5 text-[10px] font-semibold text-blue-400">v2.0 Enterprise</span>
          </div>
        </div>

        <nav class="hidden md:flex items-center gap-8 text-sm font-medium text-slate-300">
          <a href="#features" class="transition hover:text-white">Features</a>
          <a href="#solutions" class="transition hover:text-white">Academic Suite</a>
          <a href="#pricing" class="transition hover:text-white">Pricing</a>
          <a href="#security" class="transition hover:text-white">Security & RBAC</a>
        </nav>

        <div class="flex items-center gap-4">
          <template v-if="session.token.value">
            <NuxtLink to="/dashboard" class="rounded-lg bg-blue-600 px-4 py-2 text-sm font-semibold text-white transition hover:bg-blue-500 shadow-sm shadow-blue-600/30">
              Go to Workspace →
            </NuxtLink>
          </template>
          <template v-else>
            <NuxtLink to="/login" class="text-sm font-medium text-slate-300 transition hover:text-white">
              Sign In
            </NuxtLink>
            <NuxtLink to="/login" class="rounded-lg bg-blue-600 px-4 py-2 text-sm font-semibold text-white transition hover:bg-blue-500 shadow-sm shadow-blue-600/30">
              Live Demo
            </NuxtLink>
          </template>
        </div>
      </div>
    </header>

    <!-- Hero Section -->
    <section class="relative overflow-hidden px-6 pt-20 pb-28 text-center lg:pt-32">
      <!-- Background Ambient Glow -->
      <div class="pointer-events-none absolute inset-0 flex items-center justify-center">
        <div class="h-[450px] w-[650px] rounded-full bg-blue-600/20 blur-[130px]" />
      </div>

      <div class="relative mx-auto max-w-4xl">
        <div class="inline-flex items-center gap-2 rounded-full border border-blue-500/30 bg-blue-500/10 px-4 py-1.5 text-xs font-medium text-blue-400 mb-8">
          <span class="flex h-2 w-2 rounded-full bg-emerald-400 animate-pulse" />
          The Unified Operating System for Modern Education
        </div>

        <h1 class="text-4xl font-extrabold tracking-tight sm:text-6xl lg:text-7xl">
          Everything your school needs, <br>
          <span class="bg-gradient-to-r from-blue-400 via-indigo-300 to-teal-300 bg-clip-text text-transparent">
            in one intelligent platform.
          </span>
        </h1>

        <p class="mx-auto mt-6 max-w-2xl text-lg text-slate-400 sm:text-xl">
          From student admissions and real-time attendance to complex term exams, multi-channel fee billing, and teacher payroll — engineered for modern schools of all sizes.
        </p>

        <div class="mt-10 flex flex-wrap items-center justify-center gap-4">
          <NuxtLink to="/login" class="inline-flex items-center gap-2 rounded-xl bg-gradient-to-r from-blue-600 to-indigo-600 px-7 py-3.5 text-base font-semibold text-white shadow-xl shadow-blue-600/25 transition hover:from-blue-500 hover:to-indigo-500">
            <span>Explore Demo Campus</span>
            <span class="text-xl">→</span>
          </NuxtLink>
          <a href="#features" class="inline-flex items-center gap-2 rounded-xl border border-slate-700 bg-slate-900/60 px-6 py-3.5 text-base font-semibold text-slate-300 transition hover:border-slate-600 hover:bg-slate-800 hover:text-white">
            View All Features
          </a>
        </div>

        <!-- Metric Badges -->
        <div class="mt-16 grid grid-cols-2 gap-4 border-t border-slate-800/80 pt-10 sm:grid-cols-4">
          <div>
            <div class="text-3xl font-extrabold text-white">250+</div>
            <div class="text-xs font-medium text-slate-400 mt-1">Versioned API Endpoints</div>
          </div>
          <div>
            <div class="text-3xl font-extrabold text-blue-400">7 Roles</div>
            <div class="text-xs font-medium text-slate-400 mt-1">Granular RBAC Security</div>
          </div>
          <div>
            <div class="text-3xl font-extrabold text-emerald-400">100%</div>
            <div class="text-xs font-medium text-slate-400 mt-1">Tenant Data Isolation</div>
          </div>
          <div>
            <div class="text-3xl font-extrabold text-amber-400">PWA Ready</div>
            <div class="text-xs font-medium text-slate-400 mt-1">Offline-First Sync</div>
          </div>
        </div>
      </div>
    </section>

    <!-- Features Grid -->
    <section id="features" class="border-t border-slate-800/80 bg-slate-900/40 px-6 py-24">
      <div class="mx-auto max-w-7xl">
        <div class="text-center">
          <h2 class="text-xs font-bold uppercase tracking-wider text-blue-400">Enterprise Capabilities</h2>
          <p class="mt-2 text-3xl font-bold tracking-tight text-white sm:text-4xl">
            Built for everyday teachers, accountants, and principals
          </p>
          <p class="mx-auto mt-4 max-w-2xl text-sm text-slate-400">
            Every module is crafted to eliminate repetitive manual work, prevent revenue leakage, and keep guardians informed.
          </p>
        </div>

        <div class="mt-16 grid grid-cols-1 gap-8 md:grid-cols-2 lg:grid-cols-3">
          <div v-for="feat in features" :key="feat.title" class="group relative rounded-2xl border border-slate-800 bg-slate-900/50 p-8 transition hover:border-blue-500/50 hover:bg-slate-800/50">
            <div class="flex h-12 w-12 items-center justify-center rounded-xl bg-blue-500/10 text-blue-400 group-hover:bg-blue-600 group-hover:text-white transition">
              <VIcon :icon="feat.icon" size="24" />
            </div>
            <h3 class="mt-5 text-xl font-semibold text-white">{{ feat.title }}</h3>
            <p class="mt-2 text-sm leading-relaxed text-slate-400">{{ feat.desc }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Pricing Section -->
    <section id="pricing" class="px-6 py-24">
      <div class="mx-auto max-w-7xl">
        <div class="text-center">
          <h2 class="text-xs font-bold uppercase tracking-wider text-blue-400">Transparent Pricing</h2>
          <p class="mt-2 text-3xl font-bold tracking-tight text-white sm:text-4xl">
            Simple, predictable pricing for schools
          </p>
          <p class="mx-auto mt-4 max-w-2xl text-sm text-slate-400">
            No hidden setup fees. Upgrade or adjust plans as your student body expands.
          </p>
        </div>

        <div class="mt-16 grid grid-cols-1 gap-8 lg:grid-cols-3">
          <div
            v-for="tier in pricingTiers"
            :key="tier.name"
            class="relative flex flex-col rounded-2xl border p-8 transition"
            :class="tier.highlight ? 'border-blue-500 bg-blue-950/20 shadow-2xl shadow-blue-500/10' : 'border-slate-800 bg-slate-900/40'"
          >
            <div v-if="tier.highlight" class="absolute -top-3.5 left-1/2 -translate-x-1/2 rounded-full bg-blue-600 px-3 py-1 text-[11px] font-bold text-white uppercase tracking-wider">
              Most Popular
            </div>

            <div>
              <h3 class="text-xl font-bold text-white">{{ tier.name }}</h3>
              <p class="mt-2 text-xs text-slate-400">{{ tier.description }}</p>
              <div class="mt-6 flex items-baseline gap-1">
                <span class="text-4xl font-extrabold text-white">{{ tier.price }}</span>
                <span class="text-sm font-medium text-slate-400">{{ tier.period }}</span>
              </div>
            </div>

            <ul class="mt-8 flex-1 space-y-3 border-t border-slate-800/80 pt-6 text-sm text-slate-300">
              <li v-for="item in tier.features" :key="item" class="flex items-center gap-3">
                <VIcon icon="tabler-check" size="18" class="text-emerald-400 shrink-0" />
                <span>{{ item }}</span>
              </li>
            </ul>

            <NuxtLink
              to="/login"
              class="mt-8 block rounded-xl py-3 text-center text-sm font-semibold transition"
              :class="tier.highlight ? 'bg-blue-600 text-white hover:bg-blue-500 shadow-lg shadow-blue-600/30' : 'border border-slate-700 bg-slate-800 text-slate-200 hover:bg-slate-700 hover:text-white'"
            >
              {{ tier.cta }}
            </NuxtLink>
          </div>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="border-t border-slate-800/80 bg-slate-950 px-6 py-12 text-sm text-slate-500">
      <div class="mx-auto flex max-w-7xl flex-col items-center justify-between gap-6 sm:flex-row">
        <div class="flex items-center gap-3">
          <div class="flex h-8 w-8 items-center justify-center rounded-lg bg-blue-600 font-bold text-white text-xs">
            SS
          </div>
          <span class="font-bold text-slate-300">SchoolSaaS Platform</span>
        </div>

        <div class="flex gap-6 text-xs text-slate-400">
          <NuxtLink to="/login" class="hover:text-white">Admin Login</NuxtLink>
          <NuxtLink to="/login" class="hover:text-white">Teacher Portal</NuxtLink>
          <NuxtLink to="/login" class="hover:text-white">Guardian Portal</NuxtLink>
          <a href="https://github.com/immoazzem/SchoolSaaS" target="_blank" class="hover:text-white">GitHub Repository</a>
        </div>

        <div class="text-xs">
          © {{ new Date().getFullYear() }} SchoolSaaS. Built with Laravel 13, Nuxt 4 & PostgreSQL.
        </div>
      </div>
    </footer>
  </div>
</template>

<style scoped>
.landing-page {
  font-family: 'Inter', system-ui, -apple-system, sans-serif;
}
</style>
