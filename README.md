# SchoolSaaS — Modern Multi-School Management SaaS Platform

[![PHP](https://img.shields.io/badge/PHP-8.5-777BB4?style=flat&logo=php&logoColor=white)](https://www.php.net)
[![Laravel](https://img.shields.io/badge/Laravel-13.38-FF2D20?style=flat&logo=laravel&logoColor=white)](https://laravel.com)
[![Nuxt](https://img.shields.io/badge/Nuxt-4.6-00DC82?style=flat&logo=nuxtdotjs&logoColor=white)](https://nuxt.com)
[![Vue](https://img.shields.io/badge/Vue-3.5-4FC08D?style=flat&logo=vuedotjs&logoColor=white)](https://vuejs.org)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-18.6-4169E1?style=flat&logo=postgresql&logoColor=white)](https://www.postgresql.org)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind-CSS-06B6D4?style=flat&logo=tailwindcss&logoColor=white)](https://tailwindcss.com)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.9-3178C6?style=flat&logo=typescript&logoColor=white)](https://www.typescriptlang.org)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

An enterprise-grade, multi-school management SaaS platform built with **Laravel 13**, **Nuxt 4**, **Vue 3**, **TypeScript**, and **PostgreSQL**. Designed with multi-tenancy, granular RBAC, offline resilience, and modern UX from day one.

---

## 🌟 Highlights & Features

- **Multi-Tenant Architecture**: Complete data isolation per school with subdomain and session context support.
- **Granular RBAC**: 7 seeded role definitions (Super Admin, School Owner, Principal, Teacher, Accountant, Auditor, Student/Parent) with fine-grained permission scopes.
- **Academic Suite**: Academic years, classes, sections, groups, shifts, class subjects, and curriculum management.
- **Student Information System (SIS)**: Enrollment tracking, guardian management, multi-year history, and student profiles.
- **Attendance Management**: Student and staff attendance with late arrival tracking, half-day support, and summary rollups.
- **Examination & Grading System**: Exam scheduling, weighted terms, grade scale configurations, marks entry verification, and automatic result computation.
- **Finance & Billing Engine**: Fee categories, custom fee structures, recurring student invoicing, multi-channel payment logging (bKash, Nagad, Cash, Card), and automated receipts.
- **Staff Operations & Payroll**: Designations, salary structures, allowance/deduction breakdowns, monthly payroll generation, and leave approvals.
- **Student & Parent Portals**: Role-filtered dashboards, fee payment overviews, attendance metrics, and published exam report cards.
- **Offline PWA Capability**: Service worker caching and offline mutation queue for recording attendance and marks in low-connectivity environments.
- **Security & Auditability**: Every sensitive mutation logged with IP, actor, payload snapshot, and tenant identifier.

---

## 🏗 System Architecture

```text
SchoolSaaS/
├── apps/
│   ├── api/          # Laravel 13 REST API (PHP 8.5, PostgreSQL, Sanctum)
│   └── web/          # Nuxt 4 SPA (Vue 3, TypeScript, Vuetify, Tailwind)
├── docs/             # Architecture, API specifications, and deployment guides
└── .github/          # CI/CD automated test & build workflows
```

---

## 🚀 Quick Start

### Prerequisites

- **PHP** >= 8.3 (PHP 8.5 tested) with `pdo_pgsql`, `mbstring`, `openssl`
- **PostgreSQL** >= 16 (18.6 tested)
- **Node.js** >= 20.x
- **Composer** >= 2.x

### 1. Backend Setup (Laravel 13 API)

```bash
cd apps/api

# Install PHP dependencies
composer install

# Configure environment
cp .env.example .env
php artisan key:generate

# Run migrations & seed demo dataset
php artisan migrate --seed
php artisan db:seed --class=DemoDataSeeder

# Start API server (port 8000)
php artisan serve --port=8000
```

### 2. Frontend Setup (Nuxt 4 SPA)

```bash
cd apps/web

# Install JavaScript dependencies
npm install

# Configure environment
cp .env.example .env

# Start development server (port 3000)
npm run dev
```

---

## 🧪 Testing & Verification

The suite includes 118 automated backend tests across all foundation, operational, and reporting modules:

```bash
cd apps/api
php artisan test
```

Frontend QA and visual layout validation:

```bash
cd apps/web
npm run qa:roles
npm run qa:visual-layout
```

---

## 📄 License

This software is released under the [MIT License](LICENSE).
