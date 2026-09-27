# AgroTrack

A fullstack agricultural logistics platform connecting Farmers, Buyers, Aggregators, and Admins in Nigeria, from produce dispatch to delivery.

## Features

- **Role-based dashboards** — Separate Farmer, Buyer, Aggregator, and Admin dashboards, each with its own layout and permissions.
- **Phone + OTP authentication** — Users register and log in with their phone number and a one-time password, no separate passwords to manage.
- **Secure session handling** — JWT issued on OTP verification, stored as an httpOnly, Secure, SameSite=None cookie, with a dedicated logout endpoint that clears it.
- **Server-side route protection** — A single edge-level guard (`proxy.ts`) verifies the JWT and matches role to path before any dashboard bytes are served, covering all four dashboards from one place.
- **OTP security hardening** — Enumeration-safe request/verify responses, timing-attack padding, phone-based cooldown (60s) and daily cap (5/day), plus IP-based rate limiting (10/hour).
- **Dispatch management** — Full dispatch status-transition system (Active → In Transit → Arrived → Completed) wired across all dashboards, with required aggregator assignment on creation and a destination-state field shared via a common enum.
- **Avatar uploads** — Cloudinary-based avatar upload system with automatic cleanup of replaced assets.
- **Type-safe forms** — All forms built with react-hook-form + Zod validation.

## Tech Stack

- **Frontend**: Next.js
- **Backend**: Node, Express + TypeScript, Prisma ORM, Postgres DB
- **Auth**: Phone/OTP + JWT (httpOnly cookies), edge middleware route guard
- **Storage**: Cloudinary

## OTP Delivery — Development Note

OTPs are generated and logged to the console in development rather than sent via live SMS. Production SMS delivery via **SendChamp** is in progress, chosen over alternatives like Termii for better regional cost-efficiency in Nigeria.

## Status

Core dispatch flow, role-based dashboards, and OTP-based auth (with security hardening) are implemented. Inventory write-path and full admin stats are still in progress.
