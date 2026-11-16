# Skill-Link

### A role-based service marketplace connecting customers, skilled workers, and organisations.

[![React](https://img.shields.io/badge/React-19-61DAFB?logo=react&logoColor=black)](https://react.dev/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.9-3178C6?logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![Vite](https://img.shields.io/badge/Vite-7-646CFF?logo=vite&logoColor=white)](https://vite.dev/)
[![NestJS](https://img.shields.io/badge/NestJS-11-E0234E?logo=nestjs&logoColor=white)](https://nestjs.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15%2B-4169E1?logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![Prisma](https://img.shields.io/badge/Prisma-ORM-2D3748?logo=prisma&logoColor=white)](https://www.prisma.io/)
[![Socket.IO](https://img.shields.io/badge/Socket.IO-4-010101?logo=socketdotio&logoColor=white)](https://socket.io/)

---

## Live Application

**Website:** [https://www.linkskill.org.in/](https://www.linkskill.org.in/)

Skill-Link is designed to bring customers, workers, and organisations into a single service marketplace. The platform combines worker discovery and job workflows with organisation product listings, reservations, identity verification, support, and operational administration.

> **Demo video:** A video walkthrough is available from the project team. The public video URL can be added here when shared.

---

## Table of Contents

- [Overview](#overview)
- [User Roles](#user-roles)
- [Features](#features)
- [Technology Stack](#technology-stack)
- [System Architecture](#system-architecture)
- [Repository Structure](#repository-structure)
- [Core Workflows](#core-workflows)
- [Backend API](#backend-api)
- [Database Design](#database-design)
- [Getting Started](#getting-started)
- [Environment Configuration](#environment-configuration)
- [Available Scripts](#available-scripts)
- [Security and Engineering Practices](#security-and-engineering-practices)
- [Project Documentation](#project-documentation)
- [Team and Attribution](#team-and-attribution)
- [Repository and Usage Notes](#repository-and-usage-notes)

---

## Overview

Skill-Link is a service marketplace built around four primary account roles:

- **Customers** can discover workers, post service jobs, browse organisation products, make reservations, and manage their wallet and support requests.
- **Workers** can create a professional profile, share skills and availability, discover jobs, manage assignments, communicate with customers, and submit KYC documents.
- **Organisations** can manage their business profile, publish products, handle incoming reservations, and manage organisation operations.
- **Administrators** can oversee users, jobs, reservations, KYC reviews, wallets, escrow controls, analytics, and support tickets.

The application is organised as a frontend and backend workspace. The frontend is a React + TypeScript single-page application. The backend is a NestJS API using PostgreSQL through Prisma ORM, with Socket.IO for authenticated real-time communication.

---

## User Roles

| Role | Main capabilities |
|---|---|
| Customer | Discover workers, create and track jobs, manage offers and contracts, browse products, reserve products, use wallet, and contact support |
| Worker | Maintain worker profile, browse available jobs, manage offers and assignments, chat about jobs, submit KYC documents, and use wallet |
| Organisation | Maintain organisation profile, create and manage products, process reservations, verify pickup OTPs, and manage wallet |
| Admin | View platform analytics, manage users and jobs, review KYC, oversee reservations and escrow, and handle support operations |

Role-based routes and backend role guards are used to separate access across the platform.

---

## Features

### 1. Authentication and Account Management

- User registration and login.
- Role-aware account onboarding and protected application routes.
- Google OAuth sign-in flow.
- Access-token and refresh-token handling.
- Email verification request and confirmation.
- Forgot-password and reset-password flows.
- Profile retrieval, update, and account deletion.
- Suspended-account handling in the frontend.

### 2. Customer Experience

- Customer dashboard and worker discovery.
- Worker profiles and skill information.
- Create, view, update, and cancel job postings.
- View offers received for a job.
- Job contracts with scope, cost, timing, schedule, and notes.
- Job-related chat with workers.
- Browse active organisation products.
- Create and track product reservations.
- View wallet balance and transaction history.
- Customer help centre and support tickets.

### 3. Worker Experience

- Worker dashboard and profile management.
- Skills, experience, biography, availability, and service-radius fields.
- Browse available jobs and filter by category.
- View job offers and manage assignments.
- Job detail and job-related communication.
- KYC document upload and submission for review.
- KYC status visibility.
- Worker wallet and support centre.

### 4. Organisation Operations

- Organisation profile and public organisation listing.
- Create, list, update, and deactivate products.
- Product image upload and management through Cloudinary.
- View incoming and pending reservations.
- Confirm or reject reservations.
- Generate and verify pickup OTPs.
- Reservation cancellation and expiry handling.
- Organisation wallet and support workflows.

### 5. Job Lifecycle and Collaboration

- Customer job creation and management.
- Worker job discovery and offer acceptance/rejection.
- Job assignment and status transitions.
- Job contracts between customers and workers.
- Job chat rooms and persisted chat messages.
- Scheduled lifecycle handling for stale open jobs.
- Real-time job and chat events through Socket.IO.

### 6. Reservations, Payments, Wallet, and Escrow

- Product reservation lifecycle: pending, confirmed, picked up, cancelled, and expired.
- Reservation expiry handling.
- Four-digit pickup OTP generation and verification.
- Payment status tracking.
- Escrow states: held, released, and refunded.
- Wallet balances and transaction ledger.
- Transactional database operations for related reservation, payment, and escrow updates.

**Payment integration note:** The repository contains a mock checkout flow and payment confirmation/failure handlers, including a Razorpay-oriented frontend callback flow. A production payment setup requires the relevant gateway configuration and verification; the presence of these code paths alone should not be interpreted as proof of live payment processing.

### 7. KYC and Trust Workflows

- Worker identity/document upload.
- Supported document categories include Aadhaar, PAN, driving licence, passport, profile photo, and skill certificate.
- Cloudinary-backed document storage.
- KYC submission and status tracking.
- Administrative KYC review and decision workflows.

### 8. Administration and Support

- Admin dashboard and analytics pages.
- User administration.
- Job and reservation oversight.
- KYC management.
- Escrow and wallet control views.
- Help centre and ticket detail workflows.
- Contact/inquiry endpoint.

### 9. Real-Time Communication

- Socket.IO gateway integrated with the NestJS backend.
- Authenticated socket connections using JWT.
- User, role, customer, worker, job, and chat-room channels.
- Job room join/leave events.
- Chat message persistence and broadcast to authorised room members.

---

## Technology Stack

### Frontend

| Technology | Purpose |
|---|---|
| React 19 | Component-based user interface |
| TypeScript | Static typing |
| Vite 7 | Development server and production bundling |
| Tailwind CSS 4 | Utility-first styling |
| shadcn/ui and Radix UI | Reusable accessible UI primitives |
| React Router 7 | Client-side routing and role-based route composition |
| Axios | HTTP communication and token refresh handling |
| Socket.IO Client | Real-time communication |
| Lucide React | Icons |
| Recharts | Dashboard and analytics visualisations |
| Motion | UI animation |
| Three.js | 3D/visual effects where used |
| date-fns | Date utilities |

### Backend

| Technology | Purpose |
|---|---|
| Node.js | JavaScript runtime |
| NestJS 11 | Modular backend framework |
| TypeScript | Backend language |
| PostgreSQL | Relational database |
| Prisma ORM | Database access, schema, and migrations |
| Socket.IO / NestJS WebSockets | Real-time events |
| Passport and JWT | Authentication |
| Google OAuth 2.0 | Google sign-in |
| class-validator / class-transformer | DTO validation and transformation |
| Swagger | API documentation |
| Cloudinary | Image and KYC document storage |
| Nodemailer / Resend | Email-delivery integrations |
| Helmet | HTTP security headers |
| Compression | HTTP response compression |
| NestJS Throttler | Request rate limiting |
| Jest / Supertest | Unit and end-to-end testing |

---

## System Architecture

```text
┌──────────────────────────────────────────────────────────┐
│                    React + TypeScript                    │
│                         Frontend                          │
│                                                          │
│  Landing / Auth / Customer / Worker / Organisation       │
│                Admin / Shared UI                         │
│                                                          │
│       Axios API Client       Socket.IO Client            │
└───────────────────────┬──────────────────────────────────┘
                        │
                HTTP + WebSocket
                        │
┌───────────────────────▼──────────────────────────────────┐
│                     NestJS Backend                       │
│                                                          │
│  Auth       Users       Workers       Organisations       │
│  Jobs       Products    Reservations  Payments            │
│  Escrow     KYC         Admin         Help / Contact      │
│  Realtime   Storage     Prisma                            │
│                                                          │
│  Guards · DTO Validation · Filters · Interceptors        │
│  Swagger · Rate Limiting · Helmet · Compression          │
└───────────────────────┬──────────────────────────────────┘
                        │ Prisma ORM
                        │
┌───────────────────────▼──────────────────────────────────┐
│                       PostgreSQL                         │
│                                                          │
│ Users · Customers · Workers · Organisations · Jobs      │
│ Offers · Contracts · Chat · Products · Reservations     │
│ Payments · Escrow · Wallet · KYC · Help Tickets          │
└──────────────────────────────────────────────────────────┘

External integrations:
- Cloudinary for uploaded media and KYC documents
- Google OAuth for authentication
- Email provider configuration for verification and recovery
```

---

## Repository Structure

```text
Skill-Link/
│
├── Frontend/
│   ├── public/                  # Public images, logos, and assets
│   ├── assets/                  # Brand assets
│   ├── src/
│   │   ├── app/                 # Auth context and route configuration
│   │   ├── components/          # Shared UI components
│   │   ├── features/
│   │   │   ├── admin/
│   │   │   ├── auth/
│   │   │   ├── customer/
│   │   │   ├── help/
│   │   │   ├── organisation/
│   │   │   ├── products/
│   │   │   └── worker/
│   │   ├── layouts/
│   │   ├── pages/
│   │   │   ├── admin/
│   │   │   ├── auth/
│   │   │   ├── company/
│   │   │   ├── customer/
│   │   │   ├── landing/
│   │   │   ├── legal/
│   │   │   ├── organisation/
│   │   │   ├── platform/
│   │   │   └── worker/
│   │   ├── services/            # API and Socket.IO clients
│   │   └── shared/              # Shared components, hooks, utilities
│   ├── package.json
│   ├── vite.config.ts
│   └── vercel.json
│
├── Backend/
│   ├── docs/                    # MVP and phase planning documents
│   ├── prisma/
│   │   ├── migrations/          # PostgreSQL schema migrations
│   │   ├── schema.prisma
│   │   └── seed.ts
│   ├── src/
│   │   ├── admin/
│   │   ├── auth/
│   │   ├── common/
│   │   ├── contact/
│   │   ├── escrow/
│   │   ├── help/
│   │   ├── jobs/
│   │   ├── kyc/
│   │   ├── organisations/
│   │   ├── payments/
│   │   ├── ping/
│   │   ├── prisma/
│   │   ├── products/
│   │   ├── realtime/
│   │   ├── reservations/
│   │   ├── storage/
│   │   ├── users/
│   │   ├── workers/
│   │   ├── app.module.ts
│   │   └── main.ts
│   ├── docker-compose.yml
│   ├── prisma.config.ts
│   └── package.json
│
└── README.md
```

---

## Core Workflows

### Job Workflow

```text
Customer creates job
        │
        ▼
Job is posted and visible to eligible workers
        │
        ▼
Workers discover the job and submit/respond to offers
        │
        ▼
Customer reviews offers and selects a worker
        │
        ▼
Job contract and job-related chat support coordination
        │
        ▼
Job progresses through its lifecycle
        │
        ▼
Completion / cancellation and associated payment-escrow handling
```

### Reservation Workflow

```text
Customer reserves an organisation product
        │
        ▼
Reservation: PENDING
        │
        ├── Organisation rejects / cancellation ──► CANCELLED
        │
        ▼
Organisation confirms reservation
        │
        ▼
Reservation: CONFIRMED + pickup OTP generated
        │
        ▼
Organisation verifies customer's OTP
        │
        ▼
Reservation: PICKED_UP
        │
        ▼
Escrow release / wallet transaction
```

An expiry task handles reservations that pass their configured expiry time. The backend service enforces allowed reservation state transitions.

---

## Backend API

The backend uses the global API prefix:

```text
/api/v1
```

| Module | Route group | Main responsibilities |
|---|---|---|
| Authentication | `/auth` | Register, login, refresh, logout, verification, password recovery, Google OAuth, profile |
| Users | `/users` | User-related operations |
| Workers | `/workers` | Worker listing and worker profile |
| Organisations | `/organisations` | Public organisation listing and organisation profile |
| Products | `/products` | Product catalogue, CRUD, and image management |
| Jobs | `/jobs` | Job posting, discovery, offers, contracts, assignments, and chat |
| Reservations | `/reservations` | Reservation lifecycle, confirmation, cancellation, and pickup |
| KYC | `/kyc` | Document upload, submission, and status |
| Payments | `/payments` | Checkout callbacks and wallet |
| Admin | Admin module routes | Platform operations and moderation |
| Help | Help module routes | Support ticket workflows |
| Contact | Contact module routes | Public inquiries |

### API Documentation

In development mode, Swagger UI is configured at:

[http://localhost:3000/api/docs](http://localhost:3000/api/docs)

The OpenAPI JSON is exposed at:

`/api/docs/json`

Swagger is intentionally registered only when the backend is not running in production mode.

### Standard API Response Shape

Successful responses are wrapped by the global response interceptor:

```json
{
  "success": true,
  "statusCode": 200,
  "data": {}
}
```

Error responses use a structured error shape:

```json
{
  "success": false,
  "statusCode": 404,
  "message": "Resource not found",
  "error": "NotFoundException",
  "path": "/api/v1/resource/id",
  "timestamp": "..."
}
```

---

## Database Design

PostgreSQL is accessed through Prisma ORM. The schema includes the following main domain areas:

| Domain | Representative models |
|---|---|
| Identity | User, RefreshToken, EmailVerificationToken, PasswordResetToken |
| Marketplace roles | Customer, Worker, Organisation |
| Jobs | Job, JobOffer, JobContract |
| Communication | ChatRoom, ChatMessage |
| Catalogue | Product, ProductImage |
| Reservations | Reservation |
| Finance | Payment, Escrow, Wallet, WalletTransaction |
| Trust and verification | WorkerDocument, KycRequest |
| Support | HelpTicket |

Important enums include user roles, job status, offer and contract status, reservation status, payment status, escrow status, KYC status, and help-ticket status.

Prisma migrations are stored in `Backend/prisma/migrations`.

---

## Getting Started

### Prerequisites

- Node.js compatible with the project dependencies.
- npm.
- Docker Desktop (recommended for local PostgreSQL) or an accessible PostgreSQL instance.
- Git.

### 1. Clone the Repository

```bash
git clone https://github.com/visheshmalhotraTHECODER/Skill-Link.git
cd Skill-Link
```

### 2. Start PostgreSQL

The backend includes a Docker Compose configuration.

```bash
cd Backend
docker compose up -d
```

Set the PostgreSQL user, password, and database values in the backend environment file before starting the database.

### 3. Configure and Start the Backend

```bash
cd Backend
cp .env.example .env
npm install
npm run db:generate
npm run db:migrate
npm run db:seed
npm run start:dev
```

The backend runs on the configured `PORT` (the project documentation uses port `3000`).

### 4. Configure and Start the Frontend

Open a second terminal:

```bash
cd Frontend
npm install
```

Create a `.env` file in the Frontend directory:

```env
VITE_API_URL=http://localhost:3000
```

The API client appends `/api/v1` automatically when it normalises the configured base URL.

Start the frontend:

```bash
npm run dev
```

Vite prints the local frontend URL in the terminal (typically `http://localhost:5173`).

---

## Environment Configuration

### Backend — `Backend/.env`

Start from `Backend/.env.example`. The main configuration keys include:

| Variable | Purpose |
|---|---|
| `DATABASE` | PostgreSQL connection URL used by Prisma |
| `POSTGRES_USER` | Local Docker PostgreSQL username |
| `POSTGRES_PASSWORD` | Local Docker PostgreSQL password |
| `POSTGRES_DB` | Local Docker database name |
| `PORT` | Backend listen port |
| `NODE_ENV` | Runtime environment |
| `CORS_ORIGIN` | Comma-separated allowed frontend origins |
| `JWT_ACCESS_SECRET` | Access-token signing secret |
| `JWT_ACCESS_EXPIRES_IN` | Access-token expiry |
| `JWT_REFRESH_EXPIRES_DAYS` | Refresh-token validity |
| `MAIL_MODE` | Email delivery mode |
| `MAIL_FROM` | Sender email address |
| `SMTP_HOST`, `SMTP_PORT`, `SMTP_USER`, `SMTP_PASS` | SMTP configuration |
| `GOOGLE_CLIENT_ID`, `GOOGLE_CLIENT_SECRET` | Google OAuth credentials |
| `GOOGLE_CALLBACK_URL` | Google OAuth callback URL |
| `FRONTEND_AUTH_CALLBACK_URL` | Frontend callback after Google authentication |
| `CLOUDINARY_CLOUD_NAME`, `CLOUDINARY_API_KEY`, `CLOUDINARY_API_SECRET` | Cloudinary configuration |
| `VERIFY_EMAIL_URL`, `RESET_PASSWORD_URL` | Frontend verification and reset links |

The example file also documents KYC and product upload folder variables, plus email expiry settings. Configure optional integrations only when using the corresponding feature.

Example PostgreSQL URL:

```env
DATABASE=postgresql://postgres:your_password@localhost:5432/skilllink?schema=public
```

### Frontend — `Frontend/.env`

```env
VITE_API_URL=http://localhost:3000
```

**Never commit real secrets, API keys, OAuth credentials, database passwords, or production environment files.** The repository includes ignore rules for environment files; keep local secrets out of Git.

---

## Available Scripts

### Frontend

| Command | Description |
|---|---|
| `npm run dev` | Start Vite development server |
| `npm run build` | Run TypeScript project builds and create production bundle |
| `npm run lint` | Run ESLint |
| `npm run preview` | Preview the production bundle locally |

### Backend

| Command | Description |
|---|---|
| `npm run start:dev` | Start NestJS in watch mode |
| `npm run build` | Build the backend |
| `npm run start:prod` | Start the built backend |
| `npm run db:generate` | Generate Prisma Client |
| `npm run db:migrate` | Apply development migrations |
| `npm run db:seed` | Seed the database |
| `npm run db:studio` | Open Prisma Studio |
| `npm test` | Run unit tests |
| `npm run test:e2e` | Run end-to-end tests |
| `npm run test:cov` | Run tests with coverage |

---

## Security and Engineering Practices

The backend configuration includes:

- JWT authentication and role-based guards.
- DTO validation with whitelist and non-whitelisted property rejection.
- Global exception filtering and standard response transformation.
- Helmet security headers.
- HTTP response compression.
- Request throttling.
- Prisma transactions for related data updates.
- Authenticated Socket.IO connections and room access checks.
- Environment-based configuration for secrets and integrations.

Production deployments should configure real secrets, allowed CORS origins, external integrations, database backups, and payment-provider verification. The local Swagger UI is disabled in production by the current bootstrap configuration.

---

## Project Documentation

- [Frontend README](./Frontend/README.md) — frontend setup, feature structure, and UI foundation.
- [Frontend shadcn guide](./Frontend/SHADCN.md) — component conventions and usage.
- [Backend README](./Backend/README.md) — backend quick start, API contract, modules, and team notes.
- [Backend docs](./Backend/docs/) — project planning and phase documentation.
- [Prisma schema](./Backend/prisma/schema.prisma) — database models and relations.
- [Prisma migrations](./Backend/prisma/migrations/) — database migration history.

---

## Team and Attribution

This repository is an authorised showcase copy of the Skill-Link project, published with permission from the original repository owner. The original project and module contributions remain attributed to their respective contributors; this repository copy does not claim that every original module was independently authored by the republisher.

The original backend team documentation records the following module ownership:

| Area | Ownership recorded in the source documentation |
|---|---|
| Authentication | Vidhit |
| Jobs, Workers, KYC | Udit |
| Organisations, Products, Reservations | Project owner / contributor |
| Escrow, Common utilities, Prisma | Shared |

**Original repository:** [Shankar-0707/Skill-Link](https://github.com/Shankar-0707/Skill-Link)  
**Showcase repository:** [visheshmalhotraTHECODER/Skill-Link](https://github.com/visheshmalhotraTHECODER/Skill-Link)  
**Live application:** [https://www.linkskill.org.in/](https://www.linkskill.org.in/)

---

## Repository and Usage Notes

- This repository preserves the project source layout and existing frontend/backend documentation.
- No root open-source licence file is included; the backend package metadata is marked `UNLICENSED`. Permission to showcase this copy should not be interpreted as a blanket open-source licence or permission to redistribute beyond the agreed scope.
- Keep contributor attribution and original project ownership references intact.
- For additional usage or redistribution permissions, coordinate with the original project owner.

---

<div align="center">

**Skill-Link — connecting customers, skilled workers, and organisations.**

Live: [www.linkskill.org.in](https://www.linkskill.org.in/)

</div>
