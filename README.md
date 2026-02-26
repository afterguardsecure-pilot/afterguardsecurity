# AfterGuard — Secure Death Care Platform

> **Protecting families at life's most vulnerable moment.**

[![Live Site](https://img.shields.io/badge/Live%20Site-afterguardsecurity.com-gold?style=flat-square)](https://afterguardsecurity.com)
[![Status](https://img.shields.io/badge/Status-Active%20Development-green?style=flat-square)]()
[![Built With](https://img.shields.io/badge/Built%20With-HTML%20%7C%20CSS%20%7C%20JavaScript%20%7C%20Supabase-blue?style=flat-square)]()
[![License](https://img.shields.io/badge/License-MIT-lightgrey?style=flat-square)]()

---

## About

AfterGuard is a secure, HIPAA-aligned estate management and family communication platform built for the death care industry. It connects grieving families directly to funeral homes, attorneys, and estate executors through an encrypted, centralized portal — removing the confusion, vulnerability, and fragmentation that too often defines the post-loss experience.

This project was founded and built by **Ishaan Samantray**, a Bioengineering student at **Cornell University**, out of a belief that families deserve more than a filing cabinet when navigating one of the hardest moments of their lives. AfterGuard is an early-stage startup currently in active development and open to funeral home pilot partners.

> *"I built this because I want families to be able to connect with each other and protect what matters most — even in the worst moments."*
> — Ishaan Samantray, Founder

---

## The Problem

When someone passes away, their family is left to navigate an overwhelming and fragmented process:

- Death certificates, wills, insurance policies, and legal documents are scattered across multiple locations
- Sensitive personal information — Social Security numbers, financial records, medical history — is passed around via email and phone with no security
- Funeral homes have no standardized, secure channel to communicate with families
- Grief scams and identity theft targeting the recently bereaved are a documented and growing threat
- Family members in different cities or countries have no shared, secure space to coordinate

AfterGuard solves all of this in one platform.

---

## What AfterGuard Does

AfterGuard provides every estate with its own **encrypted portal** — a private, secure space where:

- Documents are stored and organized with AES-256 encryption
- Funeral homes connect directly with verified, secure access
- Family members are invited with role-based permissions (view-only or full access)
- All communications are encrypted end-to-end
- Every action is logged in a tamper-evident audit trail
- A guided estate checklist walks families through every required step

---

## Features

### 🔒 Military-Grade Encryption
All data is encrypted at rest and in transit using AES-256. Built on Supabase's secure infrastructure with Row Level Security enforced at the database level — users can only ever access data they are explicitly authorized to see.

### 👨‍👩‍👧 Role-Based Family Access
Invite specific family members, attorneys, or funeral home staff to each estate portal with granular access controls. Assign view-only or full access, set relationships, and revoke permissions at any time.

### 🏛️ Verified Funeral Home Network
Funeral homes can create accounts and connect directly to family portals through a verified, background-checked network. No third-party intermediaries, no confusion about where documents should go.

### 📂 Centralized Document Vault
Upload death certificates, wills, insurance policies, property deeds, bank records, and more to an organized, searchable vault with a full version and upload history.

### 💬 Secure Messaging
All communications between family members, funeral home staff, legal counsel, and other authorized parties happen through an encrypted messaging layer built directly into each estate portal.

### ✅ Guided Estate Checklist
Step-by-step checklists tailored to each estate's situation ensure that nothing is missed during an already overwhelming time. Every completed step is audit-logged.

### 🕯️ Digital Vigil — Private Memorial Space *(Exclusive Feature)*
AfterGuard is the only platform in the death care space that bridges administrative estate management with the emotional, human side of grief. Every portal includes a **Digital Vigil** — a private, password-protected memorial space where families can:

- Light virtual candles and drag them around a living memorial — visible to all invited family members in real time
- Add memories, photos, and stories to a growing chronological timeline
- Write **Words of Light** — inspirational quotes and messages that appear in cursive on a glowing memorial wall
- Store entries in a **Last Words Vault** — sealed messages from the deceased that unlock on specific dates or milestones
- Everything is password-protected and AES-256 encrypted — only invited family can enter

### 📋 Full Audit Log
Every action taken within a portal — uploads, downloads, logins, invitations, permission changes — is logged with a timestamp and user ID. Tamper-evident, exportable, and available for legal or compliance review.

---

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Vanilla HTML, CSS, JavaScript |
| Fonts | Cormorant Garamond, DM Mono (Google Fonts) |
| Authentication | Supabase Auth (email/password + email verification) |
| Database | Supabase PostgreSQL with Row Level Security (RLS) |
| File Storage | Supabase Storage (AES-256 encrypted buckets) |
| Hosting | GitHub Pages |
| Security | Row Level Security, HIPAA-aligned data handling |

---

## Project Structure

```
afterguardsecurity/
│
├── index.html                  # Public landing page
├── afterguard-auth.html        # Sign in / Create account
├── confirm.html                # Email verification landing
├── memorial.html               # Digital Vigil — public demo
│
├── vigil-security.html         # Dashboard overview (auth required)
├── estate-records.html         # Estate portal management + document vault
├── family-portals.html         # Family member invitations + access control
├── alerts.html                 # Security alerts
├── threats.html                # Threat monitoring
├── threat-intel.html           # Threat intelligence feed
├── access-control.html         # Access management
├── audit-log.html              # Full audit trail
├── staff-roles.html            # Staff and role management
│
├── freetouselockimage.png
├── freetousefamilyimage.jpg
├── freetousefuneralhomeimage.png
├── freetousedocumentimage.jpg
├── freetousemessagingimage.jpg
├── freetouseestate_image.png
├── blankgravestonefreetouse.jpg
├── flickering_candle_md_nwm_v2.gif
│
└── README.md
```

---

## Database Schema

AfterGuard uses Supabase PostgreSQL with the following core tables, all protected by Row Level Security:

### `estates`
Stores one record per deceased person's portal.

| Column | Type | Description |
|---|---|---|
| `id` | uuid | Primary key |
| `owner_id` | uuid | References `auth.users` |
| `deceased_name` | text | Full name of the deceased |
| `file_number` | text | Auto-generated portal file number (e.g. AG-2026-4821) |
| `date_of_passing` | date | Date of death |
| `funeral_home` | text | Associated funeral home name |
| `status` | text | `active`, `pending`, or `closed` |
| `notes` | text | Optional notes |
| `created_at` | timestamp | Auto-set on creation |

### `documents`
One record per uploaded file.

| Column | Type | Description |
|---|---|---|
| `id` | uuid | Primary key |
| `estate_id` | uuid | References `estates` |
| `uploaded_by` | uuid | References `auth.users` |
| `file_name` | text | Original filename |
| `file_path` | text | Path in Supabase Storage |
| `doc_type` | text | Document category |
| `notes` | text | Optional description |
| `created_at` | timestamp | Upload timestamp |

### `estate_members`
One record per person invited to a portal.

| Column | Type | Description |
|---|---|---|
| `id` | uuid | Primary key |
| `estate_id` | uuid | References `estates` |
| `user_id` | uuid | Inviting user |
| `member_name` | text | Invitee full name |
| `member_email` | text | Invitee email |
| `role` | text | `family`, `executor`, `attorney`, `funeral_home`, `other` |
| `relationship` | text | Relationship to the deceased |
| `access_level` | text | `view` or `full` |
| `phone` | text | Optional phone number |
| `invited_at` | timestamp | Invitation timestamp |

### `memorial_entries`
One record per candle, memory, or quote in the Digital Vigil.

| Column | Type | Description |
|---|---|---|
| `id` | uuid | Primary key |
| `estate_id` | uuid | References `estates` |
| `author_id` | uuid | References `auth.users` |
| `entry_type` | text | `memory`, `quote`, or `candle` |
| `content` | text | Text content |
| `photo_path` | text | Optional photo in Supabase Storage |
| `created_at` | timestamp | Entry timestamp |

### `audit_events`
One record per user action — tamper-evident activity log.

| Column | Type | Description |
|---|---|---|
| `id` | uuid | Primary key |
| `estate_id` | uuid | Associated estate (nullable) |
| `user_id` | uuid | Acting user |
| `event` | text | Human-readable description of the action |
| `ip_address` | text | Optional IP logging |
| `created_at` | timestamp | Action timestamp |

---

## Supabase Setup

If you are setting up AfterGuard from scratch, follow these steps:

### 1. Create your Supabase project
Go to [supabase.com](https://supabase.com), create a new project, and copy your project URL and anon public key.

### 2. Run the database schema
In the Supabase SQL Editor, run the following:

```sql
-- Core tables
create table estates (
  id uuid default gen_random_uuid() primary key,
  owner_id uuid references auth.users(id),
  deceased_name text,
  file_number text,
  date_of_passing date,
  funeral_home text,
  notes text,
  status text default 'active',
  created_at timestamp default now()
);

create table documents (
  id uuid default gen_random_uuid() primary key,
  estate_id uuid references estates(id),
  uploaded_by uuid references auth.users(id),
  file_name text,
  file_path text,
  doc_type text,
  notes text,
  created_at timestamp default now()
);

create table estate_members (
  id uuid default gen_random_uuid() primary key,
  estate_id uuid references estates(id),
  user_id uuid references auth.users(id),
  member_name text,
  member_email text,
  role text,
  relationship text,
  access_level text default 'view',
  phone text,
  invited_at timestamp default now()
);

create table memorial_entries (
  id uuid default gen_random_uuid() primary key,
  estate_id uuid references estates(id),
  author_id uuid references auth.users(id),
  entry_type text,
  content text,
  photo_path text,
  created_at timestamp default now()
);

create table audit_events (
  id uuid default gen_random_uuid() primary key,
  estate_id uuid references estates(id),
  user_id uuid references auth.users(id),
  event text,
  ip_address text,
  created_at timestamp default now()
);
```

### 3. Enable Row Level Security
```sql
alter table estates enable row level security;
alter table documents enable row level security;
alter table estate_members enable row level security;
alter table memorial_entries enable row level security;
alter table audit_events enable row level security;

create policy "Users can manage their own estates" on estates for all using (auth.uid() = owner_id);
create policy "Users can manage their own documents" on documents for all using (estate_id in (select id from estates where owner_id = auth.uid()));
create policy "Users can see their own memberships" on estate_members for all using (user_id = auth.uid());
create policy "Users can manage memorial entries" on memorial_entries for all using (estate_id in (select id from estates where owner_id = auth.uid()));
create policy "Users can see their own audit events" on audit_events for all using (user_id = auth.uid());
```

### 4. Create Storage buckets
In Supabase → Storage, create two private buckets:
- `estate-documents` — for death certificates, wills, legal docs
- `memorial-photos` — for Digital Vigil memory photos

Then run:
```sql
create policy "Users can upload their own documents" on storage.objects for insert with check (bucket_id = 'estate-documents' and auth.uid() is not null);
create policy "Users can read their own documents" on storage.objects for select using (bucket_id = 'estate-documents' and auth.uid() is not null);
create policy "Users can upload memorial photos" on storage.objects for insert with check (bucket_id = 'memorial-photos' and auth.uid() is not null);
create policy "Users can read memorial photos" on storage.objects for select using (bucket_id = 'memorial-photos' and auth.uid() is not null);
```

### 5. Update your credentials
In each HTML file, replace the Supabase URL and anon key with your own project's values.

---

## Running Locally

AfterGuard is a fully static frontend — no build step, no package manager, no Node.js required.

```bash
git clone https://github.com/YOUR_USERNAME/afterguardsecurity.git
cd afterguardsecurity
```

Then open `index.html` in your browser, or use a simple local server:

```bash
# Python
python3 -m http.server 3000

# Node (if you have it)
npx serve .
```

Navigate to `http://localhost:3000` to view the site locally.

---

## Roadmap

The following features are actively planned or in development:

- [ ] **Email invitations** — send real invite emails to family members via Supabase Edge Functions + Resend
- [ ] **Real-time sync** — live updates across all family members' portals using Supabase Realtime
- [ ] **Digital Vigil persistence** — save candles, memories, and quotes to the database so they persist across sessions
- [ ] **Last Words Vault** — time-locked encrypted messages from the deceased that unlock on specific dates
- [ ] **Funeral home dashboard** — a dedicated view for funeral home accounts to manage all connected family portals
- [ ] **Two-factor authentication** — TOTP-based 2FA for all accounts
- [ ] **PDF export** — generate a printable, formatted memorial document and estate summary
- [ ] **Mobile app** — React Native companion app for on-the-go portal access
- [ ] **Attorney integration** — dedicated access layer for legal counsel with document signing workflows
- [ ] **Stripe payments** — billing integration for Family Pro and Enterprise plans
- [ ] **Automated compliance reports** — exportable HIPAA-aligned audit reports

---

## Current Status

AfterGuard is an **early-stage startup** currently in active frontend and backend development. We are:

- ✅ Live at [afterguardsecurity.com](https://afterguardsecurity.com)
- ✅ Authentication and user accounts fully functional (Supabase Auth)
- ✅ Estate portal creation and document uploads working
- ✅ Family member invitation system built
- ✅ Digital Vigil demo live at [afterguardsecurity.com/memorial.html](https://afterguardsecurity.com/memorial.html)
- ⚙️ Database backend progressively being wired to all portal pages
- ⚙️ Email invitation system in development
- 🔜 Seeking funeral home pilot partners (see below)

---

## Pilot Program

We are actively looking for **funeral homes to pilot AfterGuard for free**.

If you run or work at a funeral home and are interested in being one of our first pilot partners, we would love to connect. The pilot is completely free — no cost, no commitment. In exchange, we ask for honest feedback to help us identify bugs and improve the experience before our full release.

**To express interest:** Email [aftercaresecure@gmail.com](mailto:aftercaresecure@gmail.com) with the subject line:

> *Cornell student building free software to protect grieving families. Interested in piloting?*

---

## Contributing

AfterGuard is currently a solo student project. If you are a developer, designer, or death care professional who is interested in contributing or collaborating, please reach out.

For bug reports or feature suggestions, please open a GitHub Issue.

---

## Security

AfterGuard takes security seriously. If you discover a vulnerability, please do not open a public issue. Instead, email [aftercaresecure@gmail.com](mailto:aftercaresecure@gmail.com) directly.

All data is:
- Encrypted at rest using AES-256 via Supabase
- Encrypted in transit via TLS
- Protected by Row Level Security policies at the database layer
- Stored in HIPAA-aligned infrastructure

---

## License

This project is licensed under the MIT License. See `LICENSE` for details.

---

## Contact

**Ishaan Samantray**
Bioengineering, Cornell University
Founder, AfterGuard

📧 [aftercaresecure@gmail.com](mailto:aftercaresecure@gmail.com)
🌐 [afterguardsecurity.com](https://afterguardsecurity.com)

---

<div align="center">
  <sub>Built with care by a Cornell student who believes technology should protect people — especially at their most vulnerable.</sub>
</div>
