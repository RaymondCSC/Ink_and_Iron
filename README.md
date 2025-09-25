# Ink_and_Iron
https://utoronto.zoom.us/j/85043206116

Meeting ID: 850 4320 6116
Passcode: 202509

# Ink & Iron

A privacy-first book request and donations platform serving incarcerated readers across Canada. Built for transparency, speed, and strict facility-rule compliance.

---

## ✨ At a Glance

- **Public**: Home · Request Books · Track Request · Facility Directory · Donate · FAQ · Contact · Policies (EN/FR)
- **Private**: Volunteer workspace · Admin console
- **Core promise**: Simple requests, automatic rule checks, fast fulfillment, crystal-clear status tracking.

---

## 🗺️ Sitemap & Page Behaviours

### Public

- **Home**
  - Hero with mission + “Request Books” / “Donate” CTAs  
  - How-it-works (3 steps), live impact counters (fulfilled, avg days), partner logos  
  - Language toggle (EN/FR)

- **Request Books**
  - Form fields: full name, inmate ID#, facility (autocomplete), unit (opt), genres/titles, notes, consent ✅  
  - **Live facility rule checks** (paperback-only, max items, prohibited genres)  
  - Success screen: **Public Request ID** + link to **Track Request**  
  - Privacy blurb (what we store & duration)

- **Track Request**
  - Inputs: Public Request ID + last name  
  - Timeline: _Received → Matched → Shipped → Delivered/Refused_  
  - If **Shipped**: carrier + tracking number  
  - If **Refused**: short reason + “What to try next”

- **Facility Directory**
  - Search + filters (province, paperback-only, last-verified date)  
  - Card view: mailing address, rules summary, contact, last verified  
  - Detail page with full rules & change history snapshot

- **Donate**
  - Tabs: **Books** (dynamic wishlist + pledge) · **Funds** (Stripe one-time)  
  - Thank-you screen on completion

- **FAQ**
  - Sections: Requesting · Donations · Facility Rules · Privacy & Data  
  - Anchor links for quick jump

- **Contact**
  - Form (name, email, message type) + response-time note + alt email

- **Policies**
  - Privacy · Terms of Use · Accessibility

- **Errors**
  - 404 / fallback with helpful links (Home, Request, Track)

### Private (Role-Based)

- **Volunteer**
  - Login (NextAuth email/password), Forgot password  
  - **Queue**: table of incoming requests (age, facility, genres); filters (facility, age, flagged); actions: Claim/Unclaim, View  
  - **Request Detail**: PII-minimized summary, inline facility rules, actions:
    - Match from Inventory (search title/genre)
    - Add to Purchase List
    - Generate Packing List (PDF)
    - Enter Tracking (carrier + #)
    - Update status: Matched/Shipped/Delivered/Refused (+ reason)
  - **Inventory (read / limited write)**: search title, author, format, qty; propose admin update

- **Admin**
  - **Dashboard**: KPIs (open requests, avg fulfillment time, refusal rate)  
  - **Requests**: full list, edit states  
  - **Facilities**: list + Add/Edit (name, address, province, contact, rules JSON, last verified) + version history  
  - **Inventory**: CRUD (title, author, format, condition, genre, bin, qty)  
  - **Donations**: Stripe logs + book pledges; mark received  
  - **Users & Roles**: add/remove volunteers, set roles, force PW reset  
  - **Audit Log**: who/what/when (entity, action, diff)

---

## 🧱 Tech Stack (opinionated)

- **Web**: Next.js 14, TypeScript, React Server Components, i18n (EN/FR)
- **UI**: Tailwind CSS, Radix UI, shadcn/ui
- **Forms**: React Hook Form + Zod
- **Auth**: NextAuth (email/password; role-based guards)
- **DB**: Postgres + Prisma (Row-Level Security optional)
- **Payments**: Stripe (donations)
- **Docs/PDF**: server-rendered packing lists (PDFKit)
- **Jobs/Queues**: lightweight job runner (e.g., Inngest or custom CRON) for reminders & nightly rule verifications
- **Infra**: Vercel (web) + Neon/Supabase (Postgres) + Stripe + Resend (email)

> Swap components to match your environment if needed.

---

## 🔐 Data Model (high-level)

```mermaid
erDiagram
  User ||--o{ Session : "auth"
  User ||--o{ Role : "user_roles"
  Role ||--o{ Permission : "rbac"

  Facility ||--o{ FacilityRule : "rules[]"
  Facility {
    uuid id
    string name
    string province
    string mailing_address
    string contact_email
    date   last_verified
  }
  FacilityRule {
    uuid id
    uuid facility_id
    jsonb rules_json  // paperbackOnly, maxItems, prohibitedGenres, etc.
    date  effective_at
    uuid  edited_by
  }

  Request ||--o{ RequestItem : "items[]"
  Request {
    uuid id
    string public_id       // shown to requester
    string recipient_name
    string recipient_last_name
    string inmate_id
    uuid   facility_id
    string unit
    text   notes
    enum   status          // RECEIVED|MATCHED|SHIPPED|DELIVERED|REFUSED
    boolean consent
    uuid   claimed_by      // volunteer
    timestamptz created_at
  }
  RequestItem {
    uuid id
    uuid request_id
    string title
    string author
    string genre
    enum   source          // INVENTORY|PURCHASE
  }

  Inventory {
    uuid id
    string title
    string author
    enum   format          // PAPERBACK only enforced by rule check
    string condition
    string genre
    string bin
    int    qty
  }

  Shipment {
    uuid id
    uuid request_id
    string carrier
    string tracking_number
    timestamptz shipped_at
  }

  Donation {
    uuid id
    enum type              // BOOKS|FUNDS
    jsonb payload          // stripe_event or pledge detail
    boolean received
  }

  AuditLog {
    uuid id
    string entity
    uuid   entity_id
    string action
    jsonb  diff
    uuid   actor_id
    timestamptz at
  }
