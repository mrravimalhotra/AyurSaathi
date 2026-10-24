# Addendum: AyurSaathi PRD

Detail that belongs downstream (UX, architecture, epics), not in the PRD.

## Decided technical choices (owner)
- Stack: Next.js, Vercel, Supabase (Postgres, Auth, Storage). Built with Claude Code and BMAD.
- Hosting region: India, Mumbai preferred. To verify availability for database projects and latency to Europe (spike S-3). A region cannot be changed without migrating to a new project.
- Patient sign-in: emailed one-time link or code, no password. Add a typed-code fallback because mail scanners can consume a single-use link.
- Email provider: Resend, with a verified domain. Deferred for the prototype; use a development mail setup.
- Notifications: in-app and email only. No WhatsApp sending, no web push.
- Upload types and size: PDF, JPG, PNG, HEIC, up to 15 MB.
- Languages: English only, text in resource files.

## Core versus per-clinic split (draft, to confirm at architecture)
- **Core:** auth and roles, clinic isolation, patient record and episodes, documents, notifications, journey phases.
- **Per-clinic Clinic Settings:** branding, terminology, Check-in questions, Flag Rules, structured clinical fields, diet and medicine templates, follow-up schedules, information pack content.
- Open: whether a Clinic may rename or skip a Phase. Recommended: no for now.

## Architecture inputs
`docs/architecture.md` (data model, authorisation matrix, flows, ADR-01 to ADR-20), `docs/architecture-review.md` (gaps fixed, spike findings: S-2 database scheduler preferred, S-3 and S-4 partly verified). Required tables added in review: `payments`, `consultation_requests`. Email uniqueness should be per Clinic.

## UX inputs
`docs/ux/mockups.html` (12 screens, invented data). Phone first for Patients; responsive for Staff (BR-12). Status is shown in text as well as colour.

## Build order (owner)
Foundation, then Arrival and Care, then Enquiry, Assessment and Planning, then Continuity. Walking skeleton first. Isolation tests are written with each table, not afterwards.

## Source of decisions
`docs/parked-decisions.md` Part A (items marked Resolved).

## Tenancy decision (architecture, 2026-10-24, owner)
Deployment per clinic: one Supabase project and one Vercel deployment per clinic, same codebase. Tables still carry `clinic_id` and every policy checks it. FR-4, FR-6 and FR-48 stand: the isolation suite seeds two Clinic rows in one database and proves the policies, which keeps pooling clinics later possible.
