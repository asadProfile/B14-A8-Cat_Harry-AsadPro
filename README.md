# StudioSpace

**Space to make. Time to create.**

StudioSpace is a full-stack, peer-to-peer marketplace for creative workspaces:
photo studios, sound stages, podcast rooms, music suites, art workshops and event
spaces, booked by the hour and approved by the people who run them.

> **Live site:** not deployed yet — after following the deployment guide in
> [`client/README.md`](client/README.md#deployment), add your URL here (for
> example `https://studiosspace.vercel.app`).

This repository contains both applications:

| Directory | Purpose | Docs |
| --- | --- | --- |
| [`client/`](client/) | Next.js 15 App Router front end | [client/README.md](client/README.md) |
| [`server/`](server/) | Express + MongoDB API | [server/README.md](server/README.md) |

## What it does

- **Discover** rooms with keyword, category, price, rating and newest filters;
  searches live in the URL so results can be shared.
- **Book** a date and time slot, see the subtotal, 5% service fee, deposit and
  total before requesting, and track the request through Pending → Confirmed →
  Completed (or Cancelled while pending).
- **Never double-book** — the API re-checks every request and approval against
  Confirmed bookings for the same room, date and hours.
- **Host** a space with a five-section listing form and image uploads, then manage
  requests, confirm or complete sessions, edit and delete listings.
- **Save** studios to a MongoDB-backed wishlist and download a PDF invoice for
  confirmed or completed bookings.
- **Sign in** with email/password or Google. Sessions use an HTTPOnly cookie and
  survive a hard reload on every private route.
- **Look good doing it** — responsive layouts, a warm editorial light theme and a
  matching dark theme, skeletons, custom 404/error pages, Sonner toasts and
  custom dialogs instead of native alerts.

## Tech stack

**Client:** Next.js 15 (App Router), React 19, TypeScript, Tailwind CSS, Radix
Dialog/Dropdown, Swiper, Sonner, jsPDF, lucide-react.

**Server:** Express 4, MongoDB + Mongoose 8, JWT in HTTPOnly cookies, bcrypt,
Zod validation, Multer + ImgBB uploads, Node test runner + Supertest.

## Quick start

```bash
# Terminal 1 — API (http://localhost:5000)
cd server
npm install
cp .env.example .env
npm run dev

# Terminal 2 — client (http://localhost:3000)
cd client
npm install
cp .env.example .env
npm run dev
```

Without a `MONGODB_URI`, the API starts an in-memory MongoDB and seeds the demo
dataset (14 studios, 42 reviews, 7 bookings) automatically. The client proxies
`/api` and `/uploads` to the API, keeping cookies first-party.

### Examiner credentials

| Role | Email | Password |
| --- | --- | --- |
| Creator + host | `examiner@studiosspace.com` | `Studio123` |
| Host | `host@studiosspace.com` | `Studio123` |

The examiner owns three listings, has requests waiting on the dashboard, a saved
wishlist and bookings in every status. The login form has a **Fill credentials**
shortcut.

## Checks

```bash
cd client && npm run build && npm run typecheck
cd server && npm test
```

The server test suite covers authentication, studio CRUD permissions, discovery
filters, booking pricing/overlap rules and review aggregation. All seeded content
is demonstration data; no real payments are processed.
