---
status: draft
stepsCompleted: ['step-01-validate-prerequisites', 'step-02-design-epics']
inputDocuments:
  - _bmad-output/planning-artifacts/prds/prd-AyurSaathi-2026-10-22/prd.md
  - _bmad-output/planning-artifacts/prds/prd-AyurSaathi-2026-10-22/addendum.md
  - _bmad-output/planning-artifacts/architecture/architecture-AyurSaathi-2026-10-24/ARCHITECTURE-SPINE.md
  - _bmad-output/planning-artifacts/ux-designs/ux-AyurSaathi-2026-10-31/DESIGN.md
  - _bmad-output/planning-artifacts/ux-designs/ux-AyurSaathi-2026-10-31/EXPERIENCE.md
---

# AyurSaathi - Epic Breakdown

## Overview

This document provides the complete epic and story breakdown for AyurSaathi, decomposing the requirements from the PRD, UX Design if it exists, and Architecture requirements into implementable stories.

## Requirements Inventory

### Functional Requirements

FR-1: Staff sign-in. Staff can sign in with email and password.
FR-2: Patient sign-in by link or code. A Patient can sign in using an emailed single-use link, or a code typed on the same screen if the link fails. No password.
FR-3: Roles. The system can restrict each screen and action to Patient, Coordinator, Doctor or Admin.
FR-4: Clinic isolation. Every clinic-owned record belongs to exactly one Clinic, and a user can read or write only records of their own Clinic.
FR-5: Patient isolation. A Patient can read only their own record, Shared Notes and Shared Documents, and can write only their own flight details, Check-in answers, Consultation Requests and uploads.
FR-6: Isolation test suite. The system can run an automated suite that exercises FR-4 and FR-5 against every clinic-owned table and the document store, as Patient A, Patient B, Staff of Clinic X and Staff of Clinic Y. This is the prototype's second acceptance criterion (the first is the demo journey, SM-1; this one is SM-2 in section 7).
FR-7: Installable app. Staff and Patients can install the app on a phone home screen, and use it on a laptop browser.
FR-8: Clinic Settings. Admin can set the Clinic's name, branding and terminology labels. The Doctor can set Check-in questions and Flag Rules. Ayurvedgram is the seeded Clinic. `[ASSUMPTION: split by role as in the Glossary.]`
FR-9: Patient list. Staff can list Patients with their current Phase, filter by Phase and search by name, email or phone.
FR-10: Episodes and phase moves. Staff can move an Episode forward or back between Phases, and the system records who, when, and an optional note.
FR-11: Returning Patient. Staff can start a new Episode for an existing Patient at Assessment or Planning, without re-entering personal details or Documents.
FR-12: Patient home. A Patient can see a journey bar of the six Phases with the current Phase marked, and a card for what matters today.
FR-13: Onboard a Patient. Staff can create a Patient with name, email, phone and nationality (required) and photo, date of birth, passport number and emergency contact (optional).
FR-14: Save draft. Staff can save an unfinished onboarding as a draft and resume it later.
FR-15: Duplicate warning. Staff are warned when the email, phone or passport number matches an existing Patient in the Clinic.
FR-16: Consent step. The onboarding flow includes a Consent step as step 2, recording the Consent text version, the time and who gave it. `[ASSUMPTION: the prototype uses sample wording labelled "not legal text".]`
FR-17: Upload documents. Staff and Patients can upload PDF, JPG, PNG or HEIC files up to 15 MB each, with Shared or Staff-only visibility.
FR-18: Documents tab. A Patient record has a Documents tab listing all Documents with kind and visibility.
FR-19: Invite. After onboarding, the system can send the Patient an Invite email with a single-use link and a code.
FR-20: Log an enquiry. Staff can log an enquiry with date, channel (WhatsApp, email, phone, other), summary, treatment interest and who handled it.
FR-21: Log a Quotation. Staff can log each Quotation with version, date sent, amount and currency, validity and status.
FR-22: Log an Assessment. The Doctor can log an Assessment with date, method (in person, WhatsApp call, phone, video, email), Doctor, findings and outcome, marked Shared or Staff-only.
FR-23: Record the Programme. Staff can record the Programme and approximate cost linked to the accepted Quotation, with a status (provisional, confirmed, refined on arrival).
FR-24: Record payments received. Staff can record payments received (deposit, balance, other) with amount, currency, date and method. No online payments.
FR-25: Flight details. Staff or the Patient can enter flight number and arrival date and time.
FR-26: Pickup. Staff can enter pickup details (driver name and phone, car, plate, meeting point, time), visible to the Patient.
FR-27: Accommodation. Staff can enter Accommodation and check-in details, visible to the Patient.
FR-28: Arrival-day card. A Patient can see an arrival-day card on the home screen with flight, who meets them and where they stay.
FR-29: "I have landed" and "I need help". A Patient can tap "I have landed" or "I need help", and the Coordinator sees an alert.
FR-30: Flight-edit alert. When a Patient edits flight details, the Coordinator receives an alert.
FR-31: Post-arrival findings and Notes. Doctor can record post-arrival findings and Notes, each marked Shared or Staff-only.
FR-32: Prescribed medication. Doctor can record medicines with name, dose, schedule, start date and duration.
FR-33: Build and publish a Day Plan. Staff can build a Day Plan from treatments, diet, medicines and accommodation, copy yesterday's plan, and publish it to the Patient.
FR-34: Record daily treatments given. Staff can record treatments actually given on a day.
FR-35: Patient day view. A Patient can see the Published Day Plan's schedule and diet, and the current medicines, with a way to tick medicines taken.
FR-36: Daily Check-in. A Patient can answer a daily Check-in about whether medicines were taken and how the treatment is going. `[ASSUMPTION: five questions as a default; the questions are a Clinic Setting.]`
FR-37: Review Queue. Doctor can open a Review Queue of Check-ins, Flagged first, with the reason for each Flag.
FR-38: Sample Flag Rules. The system can raise a Flag on a Check-in using Flag Rules from Clinic Settings. The prototype ships a Sample Flag Rule set, labelled "sample, not clinical". `[ASSUMPTION: sample rules exist only so the demo can show a queue; the real rules come from the Doctor, PK-09.]`
FR-39: Review a Check-in. Doctor can add a Note, change a medicine and mark a Check-in reviewed from the same screen.
FR-40: Log departure assistance. Staff can log departure travel assistance.
FR-41: Schedule follow-up Check-ins. Staff can schedule follow-up Check-ins for a Patient, which appear to the Patient at the scheduled date and time, interpreted in the Patient's time zone.
FR-42: Answer a follow-up Check-in. A Patient can report how they feel, confirm medicines taken and flag diet issues.
FR-43: Log Consultations. Doctor or Coordinator can log WhatsApp and phone Consultations given after the Patient is home, with date, channel and summary.
FR-44: Request an extra Consultation. A Patient can request an extra Consultation with a preferred time and reason, and Staff can approve or decline it.
FR-45: In-app inbox. A user can see their notifications in an in-app inbox, such as a Published Day Plan, an Invite, a follow-up Check-in or an alert.
FR-46: Email notifications. The system can send email notifications for the same events. In the prototype delivery uses a development mail setup. Provider and sending domain are configured later.
FR-47: Patient time zone. Staff can record a Patient's time zone, and the system displays that Patient's flight, Check-in and reminder times in it.
FR-48: Demo seed. The system can load a clean demo data set of invented Patients, Staff and two Clinics, covering all six Phases, so UJ-1 to UJ-6 and the isolation suite can be run from a clean start.

### NonFunctional Requirements

NFR1: Data. Invented data only in code, seeds, tests and screenshots. No real patient data until the gate before real patient data is passed (legal review, audit log, staff MFA, isolation suite, confirmed region, engaged sponsor and doctor).
NFR2: Responsive. Coordinator and Doctor can do every task on phone or laptop with the same data. No device-only features (BR-12).
NFR3: Language. English only. UI text lives in resource files so languages can be added later.
NFR4: Time. All times stored in UTC. Patient time zone is stored and times display in local time.
NFR5: Privacy. No personal health data in application logs, error reports or analytics.
NFR6: Security. Access rules are enforced in the database. The browser never holds the service key.
NFR7: Reliability. Scheduled jobs are idempotent. Retried actions do not duplicate.
NFR8: Accessibility. Status is never shown by colour alone. Patient screens target WCAG 2.2 AA.

### Additional Requirements

AR1: Starter template. Start from the official Next.js `with-supabase` example, trimmed: pin `next` and the Supabase packages instead of `latest`; migrate Tailwind 3.4 to 4 (or fall back); bump `eslint-config-next` for Next 16; replace `lib/supabase` with `lib/db`; keep `proxy.ts` and `getClaims`; remove sample auth pages that allow public sign-up. This is Epic 1 Story 1.
AR2: Toolchain. Node 24 LTS, Next.js 16.4.3, React 19.3.1, TypeScript 5.x pinned (7.x is a later upgrade), Zod 4.6.7, Vitest 5.0.5, Playwright 1.64.1, Supabase CLI 2.122.0, @supabase/supabase-js 2.118.0, @supabase/ssr 0.12.7. Verify at scaffold; fall back as the spine says.
AR3: AD-1. Every table in an exposed schema has row-level security and clinic-and-role policies; none uses an unconditional `true`. CI scans migrations for tables without policies and for unconditional policies.
AR4: AD-2. One Supabase project and one Vercel deployment per clinic from one codebase, selected by environment variables. Every clinic-owned table carries `clinic_id` and every policy checks it before role. Two Clinic rows only in local and test databases.
AR5: AD-3. An auth hook puts `app_role` and `clinic_id` in the token from `app_metadata`, never overwriting `role`. `app_role` is one of patient, coordinator, doctor, admin. Policies read claims only through `app.user_role()`, `app.user_clinic()`, `app.user_patient_id()`, `app.is_staff()`. Server code uses `getClaims`. Access tokens expire in 10 minutes or less and `app.user_role()` requires an active profile. `proxy.ts` refreshes the session.
AR6: AD-4. The service-role key is read only in `lib/privileged`, server-only, only for creating and inviting auth users, user administration, and sending notifications; set only in the Production scope; never `NEXT_PUBLIC_`. Each privileged function takes `clinic_id` from the verified token and checks the caller's role first. The sender route accepts only signed calls from the database scheduler.
AR7: AD-5. Every mutation is a server action in its module with a shared Zod schema and the typed Result `{ ok, data }` or `{ ok:false, code, message, fieldErrors }` with codes validation_failed, not_found, forbidden, conflict, rate_limited, upload_rejected, unavailable. Retried actions use the shared `idempotency_keys` table through one helper.
AR8: AD-6. One owner module per table (access, settings, patients, onboarding, documents, enquiry, assessment, planning, arrival, care, continuity, notifications). Other modules use the owner's exported functions or the named SQL functions. An import-boundary lint rule fails the build on cross-module internals.
AR9: AD-7. Branding, terminology, Check-in questions, Flag Rules, consent text versions and templates live in `clinic_settings`, versioned and validated by Zod, read only through `modules/settings`. Write policies split by section: Admin writes branding and terminology; Doctor writes Check-in questions and Flag Rules. Flag evaluation is one SQL function with no clinical thresholds in code.
AR10: AD-8. Notes, Assessments and Documents carry `visibility` of `shared` or `staff_only`. Day Plans are Patient-visible only when published. A checked-in `supabase/capability-matrix.json` is read by policies and pgTAP. Every view is `security_invoker = true`, has `anon` grants revoked and is covered by tests. Patient policies exclude rows with `deleted_at`.
AR11: AD-9. `timestamptz` UTC everywhere; Patient IANA time zone stored; a Check-in `local_date` is the date in the Patient's zone at `scheduled_for`.
AR12: AD-10. All notification and alert writes go through `app.emit_event(type, recipient_user_id, subject, dedupe_key, payload)` with a closed event enum; recipients are auth user ids for Patients and Staff; role events fan out per user; Alerts are rows in `alerts` owned by `notifications`; `arrival_events` owned by `arrival`. `pg_cron` runs hourly, creates due Check-ins and notifications idempotently, and calls the sender route through `pg_net` with a signed header; three delivery attempts; email bodies carry no health content.
AR13: AD-11. `check_ins` is owned by `care` with `kind` (daily or follow_up), `template_id`, `local_date`, `answers jsonb`, `flags`, `reviewed_by`, `reviewed_at`; unique key `(episode_id, kind, template_id, local_date)`; `continuity` owns `follow_up_schedules` and calls `care`'s `create_due_check_in`.
AR14: AD-12. Multi-table changes are single SQL functions: `move_phase`, `publish_day_plan`, `review_check_in`, `emit_event`. `episodes.phase` is writable only through `move_phase`, which writes `phase_events` in the same transaction.
AR15: AD-13. Private buckets only; path `<clinic_id>/<patient_id>/<episode_id or general>/<document_id>.<ext>`; storage policies join to `documents`; size and MIME limits at bucket level; upsert disallowed; server re-checks content type; `nosniff` and attachment disposition; download links per click, about 60 seconds; HEIC converted in the browser; only PDF, JPG, PNG up to 15 MB stored.
AR16: AD-14. Public sign-up disabled; token hook gives no role by default. Invites are rows in `invites` with a hashed token bound to email, clinic, role and Patient; the link opens a page requiring a button press (POST) or a typed code; short expiry; uniform responses; resend cooldown and rate limit; redirect allowlist; claims from `app_metadata` only.
AR17: AD-15. Claim helpers run as invoker. Any `SECURITY DEFINER` function states its reason, sets an empty `search_path`, lives in a private schema and has `EXECUTE` revoked from public, `anon` and `authenticated` unless deliberately callable. Scheduled functions take no client parameters.
AR18: AD-16. pgTAP tests via `supabase test db` run every table, view, exposed function and bucket as Patient A, Patient B, Staff of Clinic X, Staff of Clinic Y, a demoted user with an old token, and a Patient against `staff_only` rows. A check lists every such object and fails the build if one has no test. A few Playwright tests repeat key cases through the app.
AR19: AD-17. Schema changes are forward-fix SQL migrations. `clinics.json` lists clinic project references (no secrets). Release routine: CI passes, migrations applied to every project in the manifest, then deploy. Seed is invented and idempotent.
AR20: AD-18. Log identifiers and event names only, to standard output; errors carry a reference ID; no analytics. The service worker is network-only for authenticated routes, caches only the app shell, clears caches on sign-out.
AR21: AD-19. Strict content security policy and frame, referrer and permissions headers. Sign-in, invite, resend and upload endpoints are rate limited and produce `rate_limited`.
AR22: AD-20. Audit log and staff MFA are not in the prototype but must not be blocked: all writes pass server actions and SQL functions, and rows carry `created_by` and `updated_at`.
AR23: CI/CD. GitHub Actions run lint, typecheck, unit tests, migration check, policy and test-coverage checks, pgTAP and Playwright. Environments: local (Supabase CLI plus Mailpit), pull-request preview, hosted clinic project and deployment.
AR24: PWA. A minimal service worker and web manifest (Serwist; package and build mode to verify at scaffold: `@serwist/turbopack` or `@serwist/next` with `next build --webpack`).
AR25: Mail. Local Mailpit for development; a sandbox SMTP for the hosted prototype (provider and domain are configured later by the owner). Hosting region India (Mumbai preferred), to verify at account creation.

### UX Design Requirements

UX-DR1: Design tokens. Implement the DESIGN.md colour tokens for light and dark themes (surface, ink, primary, highlight, status, phase) as theme variables; theme follows the system setting with a user override.
UX-DR2: Typography. Self-host Atkinson Hyperlegible Next (UI and body) and Source Serif 4 (display and title). Patient body 18px/28px, staff body 16px/24px; labels wrap and never truncate; usable at 200% text zoom.
UX-DR3: Spacing, radius and elevation tokens (4-48px scale, 8/12/16/full radii; tonal depth, shadows only under the bottom bar and sheets).
UX-DR4: Buttons. Primary (56px patient, 48px staff, one per screen), secondary (outlined teal), destructive (outlined critical, behind a confirmation). Disabled state shows the reason.
UX-DR5: Cards and inputs. Card with one heading; input 48px with label above, helper text, and error text with icon and the words of the fix, linked to the field.
UX-DR6: Phase chip and journey bar. Chip shows number and name; journey bar is a compact "Step N of 6" line with segments on phone and six steps on laptop; completed steps say "Done", current says "Now".
UX-DR7: Status badge. Icon plus word on a tinted fill for Done, Needs review, Not yet confirmed, Staff-only, Sample, Failed; never colour alone.
UX-DR8: Staff-only marker and Visibility toggle. A lock icon and the words "Staff-only" on the item itself; two-option toggle "Shared with patient" or "Staff-only", default Staff-only, current choice stated in words.
UX-DR9: Bottom bar. Patient: Home, Plan, Documents, Check-in. Staff phone: Today, Patients, Review (Doctor) or Plans (Coordinator), More. Icon plus label always; current item marked; 56px (patient) targets.
UX-DR10: Sidebar. Staff laptop (1024px and up), 240px, same items plus Settings and the clinic name; list-and-detail split for Patients and Review Queue.
UX-DR11: Demo ribbon. A non-dismissible "Demo data. Not real patients." strip on every screen of the prototype.
UX-DR12: Alert row and needs-attention block on Today: icon, plain sentence, patient name, time, one "Open" action; unresolved above resolved.
UX-DR13: Patient list row: name, phase chip, one status badge (Needs review, Arriving today, Nothing due), last activity; whole row is the target; filter by phase; search with "/" focus on laptop.
UX-DR14: Onboarding stepper. Three steps (Details, Consent, Review and invite) with "Step N of 3"; on success an "Add documents now" card opens the Documents tab (documents attach to the saved patient, never to a draft); Save draft always visible; leave prompts; duplicate warning on blur of email, phone or passport; consent step shows the sample text with a "Sample wording. Not legal text." badge.
UX-DR15: Document uploader. Camera or file chooser; "Preparing photo…" while HEIC converts; per-file name, size, visibility toggle and Remove behind a confirmation; limits shown before choosing; rejection messages in plain words.
UX-DR16: Day Plan builder. Date strip, "Copy yesterday", items grouped Morning, Midday, Evening, Draft or Published badge, "Publish to patient" with a confirmation naming the patient and date; "Already published." on repeat.
UX-DR17: Medicine row. Name, dose, schedule and a "Taken" toggle that reads "Taken at 08:10"; patient can undo within 10 minutes.
UX-DR18: Check-in flow. One question per screen with "Question N of 5", large answer buttons, Back at every step, a review screen before Send; score anchors in words; free text with a 1,000-character counter.
UX-DR19: Review Queue UI. Flagged first with the rule in words and a "Sample rule" badge; review pane with answers, recent notes and medicines; Add note (Shared or Staff-only), Change medicine, Mark reviewed.
UX-DR20: Time display. "Thu 12 Nov, 14:35 IST" with the clinic time in brackets when the viewer's zone differs.
UX-DR21: State patterns. Loading skeletons with the word "Loading"; empty states with next action; field and action errors that keep input; forbidden; offline banner; session-expired return; link-or-code problem message and resend cooldown; check-in done and not-due states.
UX-DR22: Safety copy. Clinic phone and "in an emergency call your local emergency number" on Check-in, Plan footer and the "I need help" screen; check-in confirmation "Received. Your doctor reviews check-ins each day."; flagged status is never shown to the patient; sample flag rules labelled.
UX-DR23: Accessibility floor. 3px focus ring with 2px offset on every focusable element; live-region announcements for status changes; 48px minimum and 8px spacing of targets; 320px width and 200% text without horizontal scroll; focus to first error; journey bar read as "Step 4 of 6, Arrival, now".
UX-DR24: Responsive layouts. Under 600px single column with bottom bar; 600 to 1023px single column wider measure; 1024px and up sidebar and list-and-detail. Record tabs scroll horizontally on phone with an edge fade.
UX-DR25: Voice and tone. All microcopy in `messages/en.json` per the EXPERIENCE.md tables; consistent terms (check-in, Day Plan, Staff-only); no exclamation marks or urgency words.
UX-DR26: Interaction primitives. No long-press or hover-only controls; destructive actions confirm once naming the thing; keyboard reachability and shortcuts; reduced motion removes transitions; no carousels, countdowns, streaks or celebratory animation.
UX-DR27: Sign-in screens. Email entry then "Send link" with a six-digit code field using one-time-code autofill beside the instruction to open the email; invite redemption page with one button; install-help page.
UX-DR28: Settings screens. Clinic (branding and terminology, Admin), Clinical rules (Check-in questions and Flag Rules with the Sample badge, Doctor), People (Staff users and roles, Admin).

### FR Coverage Map

FR-1: Epic 1 - Staff sign-in
FR-2: Epic 3 - Patient sign-in by link or code
FR-3: Epic 1 - Roles
FR-4: Epic 1 - Clinic isolation
FR-5: Epic 1 - Patient isolation
FR-6: Epic 1 - Isolation test suite
FR-7: Epic 1 - Installable app
FR-8: Epic 1 (Admin: branding and terminology) and Epic 6 (Doctor: check-in questions and flag rules) - Clinic Settings
FR-9: Epic 2 (patient list, search, filter) and Epic 3 (needs-attention block) - Patient list
FR-10: Epic 2 - Episodes and phase moves
FR-11: Epic 2 - Returning Patient
FR-12: Epic 3 - Patient home
FR-13: Epic 2 - Onboard a Patient
FR-14: Epic 2 - Save draft
FR-15: Epic 2 - Duplicate warning
FR-16: Epic 2 - Consent step
FR-17: Epic 7 - Upload documents
FR-18: Epic 7 - Documents tab
FR-19: Epic 3 - Invite
FR-20: Epic 8 - Log an enquiry
FR-21: Epic 8 - Log a Quotation
FR-22: Epic 8 - Log an Assessment
FR-23: Epic 8 - Record the Programme
FR-24: Epic 8 - Record payments received
FR-25: Epic 4 - Flight details
FR-26: Epic 4 - Pickup
FR-27: Epic 4 - Accommodation
FR-28: Epic 4 - Arrival-day card
FR-29: Epic 4 - "I have landed" and "I need help"
FR-30: Epic 4 - Flight-edit alert
FR-31: Epic 5 - Post-arrival findings and Notes
FR-32: Epic 5 - Prescribed medication
FR-33: Epic 5 - Build and publish a Day Plan
FR-34: Epic 5 - Record daily treatments given
FR-35: Epic 5 - Patient day view
FR-36: Epic 6 - Daily Check-in
FR-37: Epic 6 - Review Queue
FR-38: Epic 6 - Sample Flag Rules
FR-39: Epic 6 - Review a Check-in
FR-40: Epic 9 - Log departure assistance
FR-41: Epic 9 - Schedule follow-up Check-ins
FR-42: Epic 9 - Answer a follow-up Check-in
FR-43: Epic 9 - Log Consultations
FR-44: Epic 9 - Request an extra Consultation
FR-45: Epic 3 - In-app inbox
FR-46: Epic 3 - Email notifications
FR-47: Epic 2 - Patient time zone
FR-48: Epic 1 - Demo seed

## Epic List

### Epic 1: Secure clinic app foundation
Clinic staff sign in to their own clinic's isolated app, installed on a phone or opened on a laptop, with the clinic's branding. Isolation is proven by tests that grow with every table, a demo data set loads, and the early technical risks (region, link delivery, phone uploads with HEIC and signed links) are checked before anything depends on them.
**FRs covered:** FR-1, FR-3, FR-4, FR-5, FR-6, FR-7, FR-8, FR-48
**Implementation notes:** Starts with the starter scaffold (AR1), CI, and the pgTAP harness with the coverage check (AR18). Includes the Admin part of FR-8; the Doctor part is in Epic 6. Includes feasibility stories for spikes S-3, S-4 and S-5 with no UI. Delivers: signed-in Today (empty), branding change, green isolation suite.

### Epic 2: Patient records and onboarding
The coordinator adds a patient in three steps (details, consent, review and invite), saves drafts, is warned of duplicates, and staff can list, search, filter and move patients between phases or start a new episode for a returning patient.
**FRs covered:** FR-9, FR-10, FR-11, FR-13, FR-14, FR-15, FR-16, FR-47
**Implementation notes:** FR-9 here covers the patient list, search and phase filter only; the needs-attention block is in Epic 3. The Invite button is prepared but sending arrives in Epic 3. Delivers: add a patient end to end on phone and laptop.

### Epic 3: Invite, patient sign-in and alerts
A patient receives an invite, opens it on a phone, signs in by link or code with no password, and sees their journey Home. Notifications work through the in-app inbox and email, and staff see the needs-attention block.
**FRs covered:** FR-2, FR-9, FR-12, FR-19, FR-45, FR-46
**Implementation notes:** Heaviest in architecture despite few FRs: invites table, hashed token, redeem page, lib/privileged, the outbox, pg_cron, pg_net, signed sender route, rate limits (AR6, AR12, AR16, AR21). Includes the needs-attention block of FR-9 and the alerts table. Delivers: invite in Mailpit, patient signs in, Home shown.

### Epic 4: Arrival
The clinic enters pickup and stay, the patient adds flight details and sees the arrival-day card, and taps I have landed or I need help. The coordinator is alerted.
**FRs covered:** FR-25, FR-26, FR-27, FR-28, FR-29, FR-30
**Implementation notes:** Completes the walking skeleton and gives the needs-attention block its first real alerts.

### Epic 5: Plan and patient day
The Doctor records findings, notes and medicines. The coordinator builds, copies and publishes the Day Plan and records treatments given. The patient sees the schedule and diet, and ticks medicines taken.
**FRs covered:** FR-31, FR-32, FR-33, FR-34, FR-35
**Implementation notes:** Uses publish_day_plan as one SQL function (AR14). Delivers: published plan, a ticked medicine.

### Epic 6: Check-in and doctor review
The patient answers a daily check-in. The Doctor reviews check-ins flagged first, adds notes, changes medicines and marks them reviewed, and can edit the check-in questions and flag rules.
**FRs covered:** FR-36, FR-37, FR-38, FR-39, FR-8
**Implementation notes:** Includes the Doctor part of FR-8 as the last story, after check-ins run from seeded configuration. One check_ins table owned by care (AR13). review_check_in is one SQL function (AR14).

### Epic 7: Documents
Staff and patients add and view documents safely, with passport scans and records stored privately, shared or staff-only, and phone photos accepted.
**FRs covered:** FR-17, FR-18
**Implementation notes:** Documents attach only to a saved patient. Uses the risk learned in the Epic 1 feasibility stories (AR15).

### Epic 8: Before arrival: enquiry, assessment, planning
Staff log the enquiry and quotations, the Doctor logs the assessment, and staff record the programme and payments, so the patient history is complete from the first contact.
**FRs covered:** FR-20, FR-21, FR-22, FR-23, FR-24
**Implementation notes:** Each step moves the episode phase through move_phase.

### Epic 9: Continuity
After departure the clinic logs departure assistance and schedules follow-up check-ins, the patient answers them and can request an extra consultation, and consultations are logged.
**FRs covered:** FR-40, FR-41, FR-42, FR-43, FR-44
**Implementation notes:** Follow-up check-ins reuse the care check_ins table through create_due_check_in (AR13). Includes the pg_cron idempotency test.


## Epic 1: Secure clinic app foundation

Clinic staff sign in to their own clinic's isolated app, installed on a phone or opened on a laptop, with the clinic's branding. Isolation is proven by tests that grow with every table, a demo data set loads, and the early technical risks are checked before anything depends on them. Covers FR-1, FR-3, FR-4, FR-5, FR-6, FR-7, FR-8 (Admin part), FR-48.

### Story 1.1: Scaffold the app from the trimmed starter

As Ravi, the builder,
I want the app scaffolded from the official Next.js and Supabase starter with versions pinned,
So that every later story builds on one running, reproducible base.

**Acceptance Criteria:**

**Given** an empty repository branch
**When** the scaffold is created from the official `with-supabase` example
**Then** `next`, `react`, `@supabase/supabase-js` and `@supabase/ssr` are pinned to exact versions (no `latest`) and Node 24 LTS is set in the project settings
**And** the sample sign-up and password pages that allow public sign-up are removed, and `lib/supabase` is replaced by `lib/db` (AR1)

**Given** the scaffold
**When** `npm run lint`, `npm run typecheck` and `npm run build` are run
**Then** all three pass with no errors
**And** `proxy.ts` is present and refreshes the session by calling `getClaims`, never `getSession` (AR5)

**Given** a clean clone and a local Supabase started with the Supabase CLI
**When** a developer follows the README's three commands
**Then** the app starts on localhost and shows a public landing page
**And** environment variables are read from a documented `.env.example`; no secret is committed and the service-role key is not exposed to the browser (AR6)

**Given** the folder layout in the architecture spine
**When** the scaffold is inspected
**Then** `app/(public)`, `app/(patient)`, `app/(clinic)`, `app/api/jobs`, `modules/`, `lib/`, `messages/en.json`, `supabase/migrations`, `supabase/tests`, `supabase/seed.sql` and `clinics.json` exist
**And** where a pinned version does not build (Tailwind 4, TypeScript, Serwist), the fallback chosen is recorded in the README with the reason

### Story 1.2: CI and the isolation test harness

As Ravi, the builder,
I want continuous checks that fail the build when a table has no access policy or no isolation test,
So that no later story can ship an unprotected table by accident.

**Acceptance Criteria:**

**Given** a pull request
**When** CI runs
**Then** it runs lint, typecheck, unit tests, a migration check and the database tests (AR23)
**And** a failed step fails the pull request

**Given** the migrations folder
**When** the policy check runs
**Then** it fails if any table in an exposed schema has row-level security disabled or has no policy
**And** it fails if any policy uses an unconditional `true` (AR3)

**Given** the database tests (`supabase test db` with pgTAP)
**When** the coverage check runs
**Then** it lists every table, view, exposed function and bucket in the database
**And** it fails the build if any has no isolation test (AR18)

**Given** a deliberately unprotected fixture table and a table with no test, kept only in a test fixture
**When** the checks run against the fixture
**Then** each check fails with a message naming the offending object
**And** a clean fixture passes, proving the checks detect real problems

**Given** the harness
**When** a test author needs to act as a user
**Then** helper functions exist to run a statement as an anonymous user, Patient A, Patient B, Staff of Clinic X, Staff of Clinic Y and a demoted user with an old token
**And** the helpers are documented in `supabase/tests/README.md` (FR-6)

### Story 1.3: Design foundation and the demo shell

As a staff member or patient,
I want every screen to carry the AyurSaathi look and the demo notice,
So that the app feels consistent and invented data cannot be mistaken for real.

**Acceptance Criteria:**

**Given** the app in a browser
**When** any page loads
**Then** the colour, type, spacing and radius tokens from `DESIGN.md` are applied as theme variables, in light and dark themes following the system setting (UX-DR1, UX-DR3)
**And** the Atkinson Hyperlegible Next and Source Serif 4 fonts are self-hosted, with body text 18px for patient routes and 16px for clinic routes (UX-DR2)

**Given** any page
**When** it renders
**Then** a "Demo data. Not real patients." ribbon shows at the top and cannot be dismissed (UX-DR11)

**Given** the shared components
**When** a primary button, secondary button, destructive button, card and input are rendered
**Then** each matches the sizes and states in `DESIGN.md` (56px patient and 48px staff buttons, label above the input, error text with an icon and the words of the fix) (UX-DR4, UX-DR5)
**And** each has a visible focus ring of 3px with a 2px offset in both themes (UX-DR23)

**Given** text at 200% zoom and a 320px-wide screen
**When** the demo shell page is viewed
**Then** no horizontal scroll appears and no label is truncated (NFR8, UX-DR23)

**Given** the microcopy rules
**When** a developer adds text
**Then** the string lives in `messages/en.json` and an automated check fails on a hard-coded UI string in a component (NFR3, UX-DR25)

### Story 1.4: Clinic record and settings store

As an Admin,
I want my clinic's name, branding and clinical configuration stored as settings,
So that nothing specific to one clinic lives in code and the clinic's rules can be edited later.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** `clinics` and `clinic_settings` tables exist, owned by the `settings` module, each with `clinic_id`, row-level security and policies that check the clinic before the role (AR3, AR4, AR8)
**And** `clinic_settings` holds versioned sections (branding, terminology, check-in questions, flag rules, consent text versions, templates), each validated by a Zod schema on read and write (AR9)

**Given** the seed
**When** it runs
**Then** one clinic, "Ayurvedgram (demo)", exists with default terminology, five sample check-in questions, a sample flag-rule set labelled "Sample rules. Not clinical advice." and sample consent wording labelled "Sample wording. Not legal text." (FR-8, FR-16, FR-38 groundwork)
**And** running the seed twice leaves the same data (FR-48)

**Given** two clinic rows in the test database
**When** Staff of Clinic X read `clinic_settings`
**Then** they receive no rows of Clinic Y and cannot write them (FR-4)

**Given** the write policies
**When** an Admin writes the branding or terminology sections
**Then** the write succeeds
**And** an Admin writing the check-in questions or flag rules is refused, a Doctor writing the flag rules succeeds, and a Coordinator writing any section is refused (FR-8)

**Given** a settings read from application code
**When** any module needs clinic content
**Then** it reads through `modules/settings` only, and a lint rule fails the build on a direct query of `clinic_settings` elsewhere (AR8)
**And** pgTAP tests for every case above exist and the coverage check from Story 1.2 passes

### Story 1.5: Staff sign-in and roles

As a coordinator, doctor or admin,
I want to sign in with my email and password and land in the right area,
So that I reach only what my role allows.

**Acceptance Criteria:**

**Given** a staff account
**When** the user enters the correct email and password
**Then** they are signed in and land on the clinic area (FR-1)
**And** public sign-up is disabled and the token hook gives no role to anyone not provisioned by an Admin (AR16)

**Given** a wrong password
**When** the user submits
**Then** a plain message says the email or password is not right, with the same message whether or not the email exists, and the input is kept (FR-1)

**Given** a signed-in user
**When** the token is issued
**Then** an auth hook adds `app_role` (one of patient, coordinator, doctor, admin) and `clinic_id` from `app_metadata` without overwriting `role`, and tokens expire in 10 minutes or less (AR5)
**And** `app.user_role()`, `app.user_clinic()`, `app.user_patient_id()` and `app.is_staff()` are the only helpers policies use, run as invoker, and read claims only (AR17)

**Given** a user whose profile is disabled or whose role was changed
**When** they use an old token
**Then** `app.user_role()` treats them as having no role and access ends at once, proven by a pgTAP case (AR5)

**Given** a Patient role
**When** they request any clinic route
**Then** they receive "You do not have access to this page." with a link to their home and no detail about records (FR-3)

**Given** a Coordinator
**When** they attempt to write a Note or a Medicine through the database
**Then** the write is refused by policy, per the capability matrix in `supabase/capability-matrix.json` (FR-3, AR10)
**And** the `profiles` table has policies and isolation tests (AR18)

### Story 1.6: Clinic area shell and an empty Today

As a coordinator or doctor,
I want a navigation shell that works on my phone and my laptop and a Today screen,
So that I always know where I am and what to open next.

**Acceptance Criteria:**

**Given** a signed-in staff user on a phone under 600px
**When** the clinic area loads
**Then** a bottom bar shows Today, Patients, Review (Doctor) or Plans (Coordinator), and More, each with an icon and a label, the current item marked with a bar and bold label (UX-DR9)

**Given** a laptop at 1024px or wider
**When** the clinic area loads
**Then** a 240px sidebar shows the same items plus Settings and the clinic name, with a list-and-detail layout available to later screens (UX-DR10, UX-DR24)
**And** Admin sees People and Clinic settings under More; Coordinator and Doctor do not see items they cannot use (UX-DR28)

**Given** the Today screen
**When** there is nothing to show
**Then** it says "Nothing needs attention." with the clinic name from settings (UX-DR21)
**And** it shows a loading skeleton with the word "Loading" while data loads (UX-DR21)

**Given** the same staff user on phone and laptop
**When** they perform the available actions
**Then** the same data and the same actions are present on both (NFR2)
**And** keyboard users can reach every item with Tab and see the focus ring (UX-DR23, UX-DR26)

### Story 1.7: Admin sets clinic branding and terminology

As an Admin,
I want to set my clinic's name, branding and terminology labels,
So that the app speaks my clinic's language without anyone changing code.

**Acceptance Criteria:**

**Given** a signed-in Admin
**When** they open More, Settings, Clinic
**Then** they can edit the clinic name, brand colours within accessible limits and terminology labels, each validated by its schema (FR-8)

**Given** a changed terminology label
**When** the Admin saves
**Then** the new label shows on the screens that use it on the next load, with no code change (FR-8, BR-11)
**And** no screen text names Ayurvedgram except through Clinic Settings (FR-8)

**Given** a brand colour that fails the contrast check for text on its background
**When** the Admin tries to save
**Then** the save is refused with a message naming the colour and the required contrast (NFR8)

**Given** a Coordinator or Doctor
**When** they request the Clinic settings screen or call the save
**Then** they are refused, with the screen hidden from their navigation and the write refused by policy (FR-8, FR-3)
**And** a failed save keeps the Admin's input and says what to do next (UX-DR21)

### Story 1.8: Installable app and offline shell

As a patient or staff member,
I want to add the app to my phone's home screen and still see a clear message when I am offline,
So that it opens like an app and never shows stale health information.

**Acceptance Criteria:**

**Given** a phone browser
**When** the user opens the app
**Then** a web manifest and a minimal service worker make it installable (FR-7, AR24)
**And** the package and build mode for the service worker (the Serwist package and `next build --webpack` or Turbopack variant) is chosen by a working build and recorded in the README

**Given** the service worker
**When** it caches files
**Then** it caches only the app shell, authenticated routes are network-only, and caches are cleared on sign-out (AR20)

**Given** the user is offline
**When** they open a page
**Then** the shell loads with "You are offline. Connect to see your information." and no health data is shown (UX-DR21)

**Given** first sign-in
**When** the user finishes
**Then** an "Add to home screen" help page explains how, with steps for iPhone and Android (UX-DR27)
**And** the service worker never stores a response from an authenticated route, proven by a test (AR20)

### Story 1.9: Demo seed and isolation fixtures

As Ravi, the builder,
I want a repeatable demo data set of invented people and two clinics,
So that I can demonstrate every journey and the tests have realistic fixtures.

**Acceptance Criteria:**

**Given** a clean local database
**When** the seed runs
**Then** it creates, from invented data only, one demo clinic with a Coordinator, a Doctor and an Admin, and, in the test database only, a second clinic with its own staff (FR-48, AR4)
**And** every name, email, phone and passport number is invented (NFR1)

**Given** the seed
**When** it runs a second time
**Then** the data is unchanged and no duplicates appear (FR-48)

**Given** the isolation harness from Story 1.2
**When** the fixtures are loaded
**Then** Patient A, Patient B, Staff of Clinic X and Staff of Clinic Y exist for the tests, with patients' rows added by later epics as their tables arrive (FR-5, FR-6)

**Given** a hosted clinic project
**When** the seed is applied there
**Then** only the one demo clinic is created and never the second clinic (AR4)
**And** the seed command refuses to run if the target is not marked as a demo environment (NFR1)

### Story 1.10: Feasibility check: region and sign-in link delivery

As Ravi, the owner,
I want to know that the planned hosting region and the emailed sign-in link work before building on them,
So that a wrong assumption is found now, not after several epics.

**Acceptance Criteria:**

**Given** access to the Supabase organisation
**When** the available regions for new projects are queried
**Then** whether Mumbai is offered for a new database project is recorded, with the alternative chosen if it is not (AR25, spike S-3)

**Given** a development project in the chosen region and a sandbox SMTP
**When** a sign-in link and code are requested for a test email address
**Then** delivery time, link expiry, resend cooldown and whether a mail scanner can consume the link are recorded (spike S-4, AR16)
**And** the latency from Europe and from Pune to the project is measured and recorded

**Given** the results
**When** the story completes
**Then** a short findings note in `docs/spikes/` states each result and any change to the architecture it implies
**And** no screen or table is added by this story

*Prerequisites that only Ravi can supply: Supabase organisation access and sandbox SMTP credentials.*

### Story 1.11: Feasibility check: phone uploads, HEIC and signed links

As Ravi, the owner,
I want to know that photos from an iPhone and an Android phone can be uploaded and opened safely,
So that the Documents epic does not hit a surprise late.

**Acceptance Criteria:**

**Given** a private storage bucket with size and type limits and upsert disallowed
**When** a JPEG, a PNG, a PDF and an iPhone HEIC photo are uploaded from a phone
**Then** the result of each is recorded, including whether in-browser conversion of HEIC to JPEG works and how long it takes (spike S-5, AR15)

**Given** a stored file
**When** a download link is created per click
**Then** the link works within about 60 seconds and fails after that (AR15)
**And** a file in another folder cannot be fetched by a different test user

**Given** the results
**When** the story completes
**Then** a findings note in `docs/spikes/` records the working approach, the oldest phone tested and any change to Epic 7
**And** no user-facing screen is added by this story

<!-- NEXT EPIC -->
