# Bazaria-store-showcase
A modern, scalable e-commerce platform for the UAE market.
# Bazaria.store

**A modern, scalable e-commerce platform for the UAE market.**

Bazaria.store is a full-stack e-commerce platform designed to support online retail, product discovery, shopping carts, checkout, order management, inventory control and customer engagement.

The platform is built with a modular architecture to support future business expansion, additional product categories, payment providers and customer-facing services.

**Repository:** https://github.com/Misbah-code/bazaria-store  
**Primary market:** United Arab Emirates (UAE)  
**Repository visibility:** Private  
**Current development status:** MVP – Active Development

---

## 1. Project Overview

Bazaria.store aims to provide a flexible online shopping experience with a centralized administration platform.

The current business direction focuses on residential water-filtration products, including:

- Kitchen and drinking water filtration systems
- Whole-house water filtration
- Shower filters
- Water softeners
- Replacement cartridges and accessories

The platform architecture is intended to support expansion into additional product categories.

### Business Objectives

- Provide a convenient online shopping experience.
- Support product discovery and catalogue management.
- Enable secure order processing and inventory management.
- Provide administrative control over products and orders.
- Improve customer engagement through product reviews.
- Establish a scalable foundation for future e-commerce services.

---

## 2. Technology Stack

| Layer | Technology |
|---|---|
| Frontend | Next.js 15 |
| UI Framework | React 19 |
| Programming Language | TypeScript |
| Backend | NestJS |
| Database | PostgreSQL 17 |
| ORM | Prisma 6.19.3 |
| Runtime | Node.js |
| Package Manager | npm |
| Containerization | Docker / Docker Compose |
| Version Control | Git / GitHub |

### Architecture

The solution uses a monorepo structure containing the frontend, backend API and shared database package.

```text
bazaria-store/
│
├── apps/
│   ├── web/                 # Next.js storefront
│   │   └── src/app/
│   │       ├── admin/
│   │       ├── cart/
│   │       ├── categories/
│   │       ├── checkout/
│   │       ├── order/
│   │       ├── products/
│   │       ├── search/
│   │       ├── track-order/
│   │       └── write-review/
│   │
│   └── api/                 # NestJS backend
│       └── src/
│           ├── admin-auth/
│           ├── admin-orders/
│           ├── admin-products/
│           ├── admin-reviews/
│           ├── admin-shipments/
│           ├── checkout/
│           ├── payments/
│           ├── products/
│           ├── reviews/
│           └── email.service.ts
│
├── packages/
│   └── database/
│       └── prisma/
│           ├── migrations/
│           ├── schema.prisma
│           ├── seed.ts
│           └── create-admin.ts
│
├── docker-compose.yml
├── package.json
├── package-lock.json
├── .env.example
├── .gitignore
├── README.md
└── IMPLEMENTATION_STATUS.md
```

---

## 3. Implemented Features

The following features have corresponding implementation files in the current codebase.

### 3.1 Customer Storefront

- Homepage and featured product presentation.
- Product catalogue.
- Category navigation.
- Product detail pages.
- Product search.
- Catalogue filtering.
- Shopping cart.
- Checkout interface.
- Order confirmation.
- Order tracking interface.

### 3.2 Product Management

- Administrative product management interface.
- Product catalogue administration.
- Product badges.
- Sale pricing support.
- Category-based product organization.

### 3.3 Checkout and Orders

- Guest checkout.
- Customer record creation or reuse through normalized email addresses.
- Order creation.
- Order item management.
- Inventory validation and transactional stock updates.
- Customer order information.
- Order management interface.

### 3.4 Payments

The current implementation includes:

- Cash on Delivery (COD) support.
- Development mock payment provider.
- Payment transaction infrastructure.
- Tabby-related payment reference fields in the database schema.

**Important:** Tabby production integration and live payment-provider processing must not be considered operational until their integrations and payment flows are completed and tested.

### 3.5 Administration

Administrative functionality includes:

- Admin authentication.
- Admin authorization guards.
- Order management.
- Product management.
- Review moderation.
- Shipment management.

### 3.6 Shipment Management

- Shipment management API.
- Shipment status tracking.
- Administrative shipment interface.
- Delivery status integration with review invitations.

### 3.7 Customer Reviews

- Product review submission.
- Email OTP verification.
- Review proof-token validation.
- Review moderation.
- Approved review display on product pages.
- Automated review invitation infrastructure for delivered orders.

Review invitations are designed to be triggered after delivery confirmation.

---

## 4. Database Architecture

The application uses PostgreSQL with Prisma ORM.

**Database configuration:**

- Database engine: PostgreSQL
- Database name in the current local configuration: `bazaria`
- Schema: `public`
- ORM: Prisma 6.19.3

### Database Management

Database schema:

`packages/database/prisma/schema.prisma`

Migration directory:

`packages/database/prisma/migrations/`

The current project contains 11 Prisma migration folders.

The local database migration status was verified successfully:

```text
11 migrations found in prisma/migrations

Database schema is up to date!
```

### Database Operations

Generate Prisma Client:

```powershell
npm.cmd run db:generate
```

Run migrations:

```powershell
npm.cmd run db:migrate
```

Check migration status:

```powershell
npm.cmd exec --workspace @bazaria/database -- prisma migrate status --schema prisma/schema.prisma
```

Always review the database environment and take a backup before executing database-changing operations.

---

## 5. Prerequisites

Before running the application, install:

- Node.js (compatible with the project dependencies)
- npm
- Docker Desktop
- Git
- PostgreSQL 17, or the supplied Docker PostgreSQL service

The project has been checked locally with:

- Node.js 24.22.1
- npm 11.19.1
- PostgreSQL 17
- Prisma 6.19.3

---

## 6. Local Development Setup

### Step 1: Clone the repository

```powershell
git clone https://github.com/Misbah-code/bazaria-store.git
```

Enter the project directory:

```powershell
cd bazaria-store
```

### Step 2: Install dependencies

```powershell
npm.cmd install
```

### Step 3: Configure environment variables

Review the example environment files:

```text
.env.example
apps/web/.env.example
```

Create the required local environment files based on the examples and the actual application configuration.

Do not commit real credentials, database passwords, SMTP passwords, API keys or security secrets.

### Step 4: Start PostgreSQL

Use the supplied Docker Compose configuration:

```powershell
docker compose up -d
```

Verify containers:

```powershell
docker ps
```

### Step 5: Generate Prisma Client

```powershell
npm.cmd run db:generate
```

### Step 6: Apply database migrations

```powershell
npm.cmd run db:migrate
```

Only apply migrations against the intended database after reviewing its configuration and backup status.

### Step 7: Start the backend API

Open a terminal:

```powershell
npm.cmd run dev:api
```

The local API base URL is:

```text
http://localhost:4000/api/v1
```

### Step 8: Start the frontend

Open another terminal:

```powershell
npm.cmd run dev:web
```

Open the storefront:

```text
http://localhost:3000
```

---

## 7. Available Project Commands

Run these commands from the project root.

| Command | Purpose |
|---|---|
| `npm.cmd run dev:web` | Start Next.js frontend |
| `npm.cmd run dev:api` | Start NestJS API |
| `npm.cmd run typecheck` | TypeScript checks across workspaces |
| `npm.cmd run build:web` | Build frontend |
| `npm.cmd run build:api` | Build backend |
| `npm.cmd run db:generate` | Generate Prisma Client |
| `npm.cmd run db:migrate` | Run database migrations |

On Windows PowerShell, `npm.cmd` is used to avoid PowerShell execution-policy restrictions affecting `npm.ps1`.

---

## 8. Security Considerations

The project includes foundational security measures such as:

- Backend request validation.
- Helmet security middleware.
- CORS allow-list configuration.
- API rate limiting.
- Security response headers.
- Administrative authentication and authorization.
- Transactional inventory updates.
- Email OTP verification for product reviews.
- Environment-based configuration.

### Environment File Protection

The following files must remain local and must never be committed:

```text
.env
.env.local
apps/web/.env.local
packages/database/.env
```

The repository `.gitignore` excludes environment files, generated dependencies and application upload files.

Production deployment still requires additional security work, including:

- Production secrets management.
- TLS configuration.
- Payment webhook verification and idempotency.
- Security testing.
- Database backup and recovery procedures.
- Monitoring and logging.
- Production deployment validation.

---

## 9. Development Roadmap

The following items are planned or require further implementation and verification.

| Feature | Status |
|---|---|
| Storefront and product catalogue | Implemented |
| Product details and search | Implemented |
| Shopping cart | Implemented |
| Guest checkout | Implemented |
| Order management | Implemented |
| Admin authentication | Implemented |
| Admin product management | Implemented |
| Shipment management | Implemented |
| Customer reviews and moderation | Implemented |
| Review email verification | Implemented |
| Review invitation infrastructure | Implemented; end-to-end verification pending |
| Customer registration and login | Planned |
| Customer account dashboard | Planned |
| Saved customer addresses | Planned |
| Wishlist | Planned |
| Arabic translations and RTL | Planned |
| Production Tabby integration | Pending |
| Payment webhook idempotency | Pending |
| Returns and refunds | Pending |
| VAT and invoice configuration | Pending |
| Automated unit, integration and E2E tests | Pending |
| Production CI/CD | Pending |
| Production monitoring | Pending |
| Disaster recovery rehearsal | Pending |

The roadmap is subject to ongoing business requirements and technical validation.

---

## 10. Git and Version Control

The source code is maintained in a private GitHub repository:

https://github.com/Misbah-code/bazaria-store

Main development branch:

```text
main
```

### Save Future Development Changes

```powershell
git add .
git commit -m "Describe your changes"
git push
```

Check the current repository status:

```powershell
git status
```

Check the latest commit:

```powershell
git log -1 --oneline
```

Keep the repository private unless public access is intentionally approved.

---

## 11. Backup Strategy

GitHub stores the application source code and database migration history. It does not automatically back up the live PostgreSQL records or excluded uploaded images.

Maintain separate backups for:

1. PostgreSQL database records.
2. Product and application-uploaded images.
3. Secure environment configuration.
4. Application source code and migrations.

Test restoration periodically rather than relying only on successful backup creation.

---

## 12. Project Status

The current local development environment has passed the following checks:

- Frontend TypeScript validation.
- Backend TypeScript validation.
- Frontend production build.
- Backend production build.
- PostgreSQL container health check.
- Prisma migration status check.

The frontend build completed successfully, although some build-time API fetch attempts returned `ECONNREFUSED` because the API was not reachable during that build.

These checks do not constitute full end-to-end, payment, security or production acceptance testing.

**Current stage:** MVP development and feature enhancement.

---

## 13. Project Ownership

**Project:** Bazaria.store  
**Repository:** https://github.com/Misbah-code/bazaria-store  
**Market:** United Arab Emirates  
**Architecture:** Next.js + NestJS + PostgreSQL  
**Development status:** Active

---

*Bazaria.store – Building a flexible foundation for modern online retail.*
