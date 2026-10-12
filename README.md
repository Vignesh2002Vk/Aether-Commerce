# AETHER: Next-Generation Multi-Category E-Commerce Platform

AETHER is a modern, enterprise-grade e-commerce application inspired by the functionality and catalog breadth of **Amazon** and **Flipkart**, styled with a distinctive, high-end minimalist design language inspired by **[NextSense](https://nextsense.io/)**.

Built with **Next.js (App Router)**, **TypeScript**, **PostgreSQL**, **Prisma ORM**, **Tailwind CSS**, and **Razorpay Sandbox Integration**.

---

## 1. Key Platform Features

- **Storefront & Design System (NextSense Inspired)**:
  - Deep dark canvas (`#07080B`), precision translucent micro-borders, glowing electric emerald/lime accents (`#00F59B`), subtle depth glassmorphism, and responsive typography.
  - Multi-tier navigation header with instant search autocomplete, Indian PIN code delivery location selector, live cart count, and user session menu.
  - Homepage with high-converting hero section, curated category cards across 9 retail departments, today's deals with live countdown timers, trending carousels, featured brands, and verified buyer reviews.
- **Indian Commerce Primitives**:
  - Currency formatting in Indian Rupees (₹) with decimal-safe calculations.
  - 6-digit postal PIN code delivery SLA estimator with Metro Same-Day Express (Bengaluru, Delhi NCR, Mumbai, Hyderabad), Next-Day Priority, and Standard Express.
  - Razorpay payment gateway integration in Sandbox/Test Mode with HMAC-SHA256 server-side signature verification.
  - Cash on Delivery (COD) support.
  - GST-compliant order summary and printable tax invoice generator.
- **Multi-Category Breadth (9 Core Departments)**:
  - Electronics & Computing, Mobiles & Flagships, Fashion & Luxury, Home & Living, Appliances, Beauty & Grooming, Books & Tech Culture, Sports & Neuro-Fitness, Premium Accessories.
- **Full Catalog & Precision Filtering**:
  - Indexed server-side search across titles, descriptions, and tags.
  - Multi-attribute filtering by category, brand, price slider, minimum rating, today's deals, and stock availability.
  - Shareable search URLs with dynamic sorting (Featured, Price Low-High, Price High-Low, Rating, Newest).
- **Product Details & Verification**:
  - Interactive multi-angle image gallery with thumbnail zoom.
  - Variant selection (colors, storage capacities, editions) with dynamic SKU and price adjustments.
  - Real-time stock status indicator.
  - Technical specifications table & engineering highlights.
  - Verified buyer review submission system.
- **Shopping Cart & Checkout**:
  - Persistent cart with guest cookie support, automatically synchronized upon login.
  - Concurrency-safe inventory validation before checkout.
  - Promotional coupon engine (`AETHER10`, `WELCOME500`, `FESTIVE20`).
  - Multi-step checkout wizard (Delivery Address -> Review -> Payment Channel).
- **Order Management & Tracking**:
  - Unique order tracking numbers (`AET-2026-XXXXX`).
  - Visual shipment progress timeline (Confirmed -> Processing -> In Transit -> Delivered).
  - Item snapshot preservation ensuring historical invoices remain accurate.
- **Admin Command Center**:
  - Real-time sales KPI overview, processed order counts, and low-stock alerts.
  - Order status management (Pending, Confirmed, Processing, Shipped, Delivered, Cancelled).
  - Catalog inventory manager with live stock unit updates.
  - Product creation and coupon generation tools.
  - Server-enforced Role-Based Access Control (RBAC).

---

## 2. Technology Stack

- **Framework**: Next.js 15 (App Router with React Server Components & Server Actions)
- **Language**: TypeScript 5
- **Styling**: Tailwind CSS
- **Icons**: Lucide React
- **Animations**: Framer Motion & CSS Keyframes
- **Database**: PostgreSQL 16 (Relational Engine)
- **ORM**: Prisma ORM 5
- **Authentication**: Cryptographically signed HTTP-only cookies with bcrypt password hashing
- **Payments**: Razorpay Node.js SDK (with HMAC-SHA256 test signature verification)
- **Testing**: Vitest unit & integration test runner

---

## 3. Prerequisites & Environment Setup

### Prerequisites
- **Node.js**: v20+ or v24+
- **npm**: v10+ or v11+
- **PostgreSQL 16**: (A portable native PostgreSQL instance is pre-configured in `.pgsql` on port `5433`).

### Environment Variables
Copy `.env.example` to `.env`:

```bash
cp .env.example .env
```

The default `.env` is configured as:

```env
# Database Connection (Native PostgreSQL 16 on port 5433)
DATABASE_URL="postgresql://postgres:postgres@127.0.0.1:5433/aether_db?schema=public"

# Auth Secret
AUTH_SECRET="aether_super_secret_session_encryption_key_2026_at_least_32_characters"
NEXT_PUBLIC_APP_URL="http://localhost:3000"

# Razorpay Test Mode Credentials
RAZORPAY_KEY_ID="rzp_test_AetherCommerce2026"
RAZORPAY_KEY_SECRET="sec_AetherCommerceSecretKey2026"
RAZORPAY_WEBHOOK_SECRET="whsec_AetherWebhookKey2026"
```

---

## 4. Database Setup & Seeding

To initialize the PostgreSQL database, push the Prisma schema, and seed realistic demo products:

```bash
# 1. Start the PostgreSQL daemon (if not already running)
npm run db:start

# 2. Push schema to PostgreSQL
npm run db:push

# 3. Seed realistic products, categories, admin & customer accounts
npm run db:seed
```

### Pre-Configured Demo Accounts:
- **Admin Account**:
  - Email: `admin@aether.io`
  - Password: `AdminPassword123!`
  - Role: `ADMIN`
- **Customer Account**:
  - Email: `alex@nexus.io`
  - Password: `CustomerPass123!`
  - Role: `CUSTOMER`
  *(Both accounts can be filled with 1-click in the Auth Modal)*

---

## 5. Development Server

Start the Next.js development server:

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

---

## 6. Running Tests

Execute the automated test suite with Vitest:

```bash
npm test
```

Tests cover:
- Decimal pricing arithmetic, percentage discount calculations, and GST rate formulas (`tests/pricing.test.ts`)
- Indian postal PIN code validator, metro express routing, and SLA estimation (`tests/pincode.test.ts`)
- Cryptographic session signing, tamper protection, and bcrypt password hashing (`tests/auth-crypto.test.ts`)

---

## 7. Production Build & Deployment

To verify and create a production build:

```bash
npm run build
npm start
```

---

## 8. Troubleshooting

1. **Port 5433 Already in Use**:
   If port 5433 is in use, modify the port in `scripts/start-db.ps1` and `.env` `DATABASE_URL`.
2. **Prisma Client Regeneration**:
   Run `npx prisma generate` after any modifications to `prisma/schema.prisma`.
3. **PowerShell Execution Policy**:
   If executing scripts manually on Windows, use `powershell -ExecutionPolicy Bypass -File scripts/...`.
