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

## Epic 2: Patient records and onboarding

The coordinator adds a patient in three steps (details, consent, review and invite), saves drafts, is warned of duplicates, and staff can list, search, filter and move patients between phases or start a new episode for a returning patient. Covers FR-9 (list, search and filter), FR-10, FR-11, FR-13, FR-14, FR-15, FR-16, FR-47. The Invite itself is sent in Epic 3; the needs-attention block is built in Epic 3. The `patients` module is the only writer of `patients`, `episodes`, `phase_events` and `consents`; the `onboarding` module owns only `onboarding_drafts` and calls the `patients` module's exported functions (AR8).

### Story 2.1: Patient list with phase, search and filter

As a coordinator or doctor,
I want to see my clinic's patients with their current phase and find one quickly,
So that I can open the right record in a few taps.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** `patients` and `episodes` tables exist, owned by the `patients` module, each with `clinic_id`, row-level security and policies for Staff, with a Patient able to read only their own row through `app.user_patient_id()` (AR3, AR4, AR8)
**And** pgTAP tests prove Patient A cannot read or write Patient B's rows, Staff of Clinic X cannot read Clinic Y's, and a Patient cannot write a patient row, and the coverage check passes (FR-4, FR-5, AR18)

**Given** the demo seed
**When** it runs
**Then** invented patients across all six phases exist for the demo clinic, with no real names, and a second run changes nothing (FR-48, NFR1)

**Given** a signed-in Staff user
**When** they open Patients
**Then** a list shows each patient with name, a phase chip (number and name), one status badge (Nothing due for now) and last activity, and the whole row is the target (FR-9, UX-DR6, UX-DR13)
**And** with no patients the screen says "No patients yet. Add the first patient." with an Add patient button (UX-DR21)

**Given** the list
**When** the user types in search or picks a phase filter
**Then** results narrow by name, email or phone, and by phase, returning only patients of the user's clinic (FR-9)
**And** on a laptop pressing "/" focuses the search field (UX-DR26)

**Given** a patient row
**When** it is opened
**Then** a patient record page shows an Overview with name, contact details, nationality, the current phase chip and the record tabs (Overview, Before arrival, Arrival, Care, After, Documents), the later tabs showing "Nothing here yet" (FR-9)
**And** on a laptop at 1024px or wider the list sits at 360px beside the record, and on a phone the record opens full screen (UX-DR10, UX-DR24)

### Story 2.2: Add a patient

As a coordinator,
I want to add a new patient with the few details I always have,
So that their record exists and I can start their journey.

**Acceptance Criteria:**

**Given** the Patients list
**When** the coordinator taps Add patient
**Then** a dedicated flow opens, separate from the list, with a "Step 1 of N" progress word, and the step count is driven by configuration so later stories can add steps (FR-13, UX-DR14)

**Given** step 1
**When** the coordinator fills name, email, phone and nationality as required fields
**Then** the patient can be created with an optional photo, date of birth, passport number, emergency contact name and phone (FR-13)
**And** the starting phase can be chosen between Enquiry (default), Assessment and Planning

**Given** a missing or invalid field
**When** the form is submitted
**Then** each message is specific and in plain words, for example "Enter the phone number with country code, for example +43 1 234 5678." and "Date of birth cannot be in the future." (FR-13)
**And** an emergency contact name without a phone asks for the phone, the first invalid field takes focus, and the input is kept (UX-DR21)

**Given** a valid form on the review screen
**When** the coordinator confirms
**Then** a patient row and a first episode are created through the `patients` module's exported function in one action that returns the typed Result and uses an idempotency key, so a double tap creates one patient (AR7, AR14)
**And** the new patient appears in the list and opens on Overview, with nobody emailed and no sign-in account created yet (FR-13)

**Given** a Doctor or Admin
**When** they use Add patient
**Then** it works, and a Patient role cannot reach the flow (FR-3)
**And** the same flow works on phone and laptop with large touch targets and keyboard access (NFR2, UX-DR23)

### Story 2.3: Save an onboarding draft and resume it

As a coordinator,
I want to save an unfinished onboarding and come back to it,
So that an interruption does not lose what I typed.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** an `onboarding_drafts` table exists, owned by the `onboarding` module, with `clinic_id`, row-level security and a policy that lets Staff of the clinic read and write their clinic's drafts and nobody else, with pgTAP tests (AR8, AR18)

**Given** an onboarding in progress
**When** the coordinator taps Save draft, which is always visible, or tries to leave
**Then** the draft is saved, and leaving prompts "Save as draft?" (FR-14, UX-DR14)
**And** a draft creates no patient, no sign-in account and no Invite (FR-14)

**Given** saved drafts
**When** the coordinator opens Patients
**Then** a "Drafts (N)" entry lists them with name and the date saved, and tapping one resumes at the step where it stopped with the input restored (FR-14)

**Given** a draft
**When** the coordinator discards it
**Then** a confirmation names the draft, and after confirming it is deleted (UX-DR26)

**Given** a draft that is later completed
**When** the patient is created
**Then** the draft is removed in the same action and holds no files, because documents attach only to a saved patient (AR15)

### Story 2.4: Duplicate patient warning

As a coordinator,
I want to be warned when someone with the same email, phone or passport number already exists,
So that I do not create a second record for the same person.

**Acceptance Criteria:**

**Given** the details step
**When** the coordinator leaves the email, phone or passport field
**Then** the system checks the clinic's existing patients for a match on that value (FR-15)

**Given** a match
**When** it is found
**Then** a warning shows the existing patient's name and phase with "Open that record" and "Continue anyway" (FR-15)
**And** choosing Open that record leaves the draft saved and opens the existing record

**Given** the same email in a different clinic's database
**When** the check runs
**Then** no match is shown, because the check reads only the user's own clinic (FR-4)
**And** a pgTAP test proves a Staff user of Clinic X cannot see Clinic Y patients through the check

**Given** an email typed in different capitalisation
**When** the check runs
**Then** it still matches, and an email already taken shows "A patient with this email already exists. Open their record instead." (FR-15)

### Story 2.5: Record consent during onboarding

As a coordinator,
I want to record that the patient has agreed to the clinic keeping their information,
So that consent is captured at the start with the wording the clinic uses.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** a `consents` table exists, owned by the `patients` module, with `clinic_id`, the consent text version, the time, who recorded it, how it was given, and a nullable withdrawn time, with row-level security and pgTAP tests, where a Patient can read only their own consents (FR-16, AR3, AR18)

**Given** the onboarding flow
**When** it runs
**Then** Consent is step 2 and the step count becomes three (Details, Consent, Review and invite) (FR-16, UX-DR14)

**Given** step 2
**When** it is shown
**Then** it displays the clinic's current consent text from settings with a visible "Sample wording. Not legal text." badge, and a tick box with the words of what is being agreed (FR-16, AR9)
**And** the patient cannot be created until the box is ticked, with a message that says why

**Given** a patient is created
**When** the consent is saved
**Then** it stores the text version, the timestamp, who ticked it and how it was given (in person or by phone)
**And** the consent text of that version stays readable later even if the clinic updates the wording

**Given** a draft saved at step 2
**When** it is resumed
**Then** the consent tick is not carried over and must be given again at the time of creation (FR-16)

### Story 2.6: Move an episode between phases

As a coordinator or doctor,
I want to move a patient's episode forward or back between the six phases,
So that the record always shows where the patient is in the journey.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** a `phase_events` table exists, owned by the `patients` module, with row-level security, and `episodes.phase` is writable only through the SQL function `move_phase`, which writes the history row in the same transaction (FR-10, AR14)
**And** pgTAP tests prove a direct update of `episodes.phase` is refused for every role (AR18)

**Given** the patient's Overview
**When** Staff choose a new phase
**Then** a confirmation names the patient and the new phase, an optional note can be added, and after confirming the phase chip updates (FR-10, UX-DR26)
**And** moving to any phase, forward or back, is allowed (assumption recorded in the spine)

**Given** a move
**When** it completes
**Then** a history entry records who moved it, when, from which phase to which, and the note, and the Overview lists the history in date order (FR-10)

**Given** two staff members move the same episode nearly together
**When** both submit
**Then** both are recorded in order and the final phase is that of the later move, with no lost history (FR-10)

**Given** a Patient role
**When** they attempt to call `move_phase`
**Then** it is refused (FR-3, AR17)

### Story 2.7: Start a new episode for a returning patient

As a coordinator,
I want to start a new visit for a patient who has been treated before,
So that their record and details carry over and nothing is re-entered.

**Acceptance Criteria:**

**Given** a patient with an earlier episode
**When** Staff choose Start new episode on Overview
**Then** the choices for the starting phase are Assessment or Planning only, with no Enquiry option (FR-11, BR-04)

**Given** a new episode is started
**When** it is created
**Then** the patient's name, contact details, nationality and consents are unchanged and not asked for again (FR-11)
**And** the earlier episode stays visible, marked closed with its closing date, and the new episode shows as current (FR-11)

**Given** a patient with several episodes
**When** Overview is shown
**Then** episodes are listed newest first, each with its own phase chip and phase history, and each moves through phases independently (FR-10, FR-11)

**Given** a list of patients
**When** a returning patient is searched for
**Then** the single patient is found once, not once per episode (FR-9)
**And** the new episode starts through `move_phase` so its first history entry exists, with pgTAP coverage (AR14)

### Story 2.8: Patient time zone and time display

As a coordinator or patient,
I want times shown in the patient's own time zone with the clinic time beside it,
So that flights and check-ins are never misread across countries.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** `patients.timezone` stores an IANA zone and `clinics.default_timezone` stores the clinic's zone, set to Asia/Kolkata in the demo seed (FR-47, AR11)

**Given** a new patient
**When** the coordinator does not set a zone
**Then** the patient defaults to the clinic's zone, and the details step offers a searchable zone field with the country's likely zone pre-selected from nationality (FR-47)

**Given** a stored instant
**When** a screen shows it to a viewer
**Then** it displays as "Thu 12 Nov, 14:35 CET (Pune 19:05)" when the viewer's zone differs from the clinic's, and without the brackets when it does not (FR-47, UX-DR20)
**And** all instants remain `timestamptz` UTC in storage (AR11, NFR4)

**Given** unit tests
**When** they run for patients in Europe, India, the US West Coast and across a daylight-saving change
**Then** every case converts and displays correctly, and a check-in's `local_date` helper returns the date in the patient's zone (FR-47, AR11)

## Epic 3: Invite, patient sign-in and alerts

A patient receives an invite, opens it on a phone, signs in by link or code with no password, and sees their journey Home. Notifications work through the in-app inbox and email, and staff see the needs-attention block. Covers FR-2, FR-9 (needs-attention block), FR-12, FR-19, FR-45, FR-46. The `notifications` module owns `notifications` and `alerts`; the `access` module owns `invites`. All notification writes go through `app.emit_event`, and the service-role key is read only in `lib/privileged` (AR6, AR12).

### Story 3.1: Notification outbox and the in-app inbox for staff

As a staff member,
I want to see updates addressed to me in an inbox,
So that events that matter reach me inside the app.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** a `notifications` table exists, owned by the `notifications` module, with `clinic_id`, recipient auth user id, event type, subject, `dedupe_key`, payload, status, scheduled time and read state, with row-level security so a user reads only their own rows (AR12, FR-45)
**And** pgTAP tests prove a user cannot read another user's notifications, Staff of Clinic X cannot read Clinic Y's, and a Patient reads only their own (AR18)

**Given** the SQL function `app.emit_event(type, recipient_user_id, subject, dedupe_key, payload)`
**When** it is called
**Then** it accepts only event types from a closed enumeration, writes one notification per recipient, and treats a repeated `dedupe_key` as a no-op (AR12)
**And** a role-wide event fans out to one row per user holding that role in the clinic
**And** the function runs as invoker or, where definer, states its reason, sets an empty `search_path`, lives in a private schema and has `EXECUTE` revoked from public, `anon` and `authenticated` (AR17)

**Given** a staff member with notifications
**When** they open More, Updates
**Then** the inbox lists them newest first, unread ones marked "New" in words, and opening one marks it read (FR-45, UX-DR21)
**And** an empty inbox says "No updates yet." and a user sees only their own notifications (FR-45)

**Given** the demo seed
**When** it runs
**Then** one invented notification exists for the demo Coordinator so the inbox can be demonstrated (FR-48)

### Story 3.2: Needs-attention block on Today

As a coordinator or doctor,
I want Today to list what needs my attention,
So that I act on the right thing first.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** an `alerts` table exists, owned by the `notifications` module, with `clinic_id`, event type, patient, summary, created time and a resolved time, with row-level security and pgTAP tests (AR12, AR18)
**And** alerts are raised only through `app.emit_event` (AR12)

**Given** unresolved alerts for the clinic
**When** a Staff user opens Today
**Then** a "Needs attention (N)" block lists them, each row with an icon, a plain sentence, the patient name, the time and one "Open" button, unresolved above resolved (FR-9, UX-DR12)
**And** Open goes to the patient record and does not resolve the alert by itself (UX-DR12)

**Given** an alert is resolved by its destination action
**When** the user returns to Today
**Then** it moves to the resolved group and the count drops (FR-9)

**Given** no alerts
**When** Today loads
**Then** it says "Nothing needs attention." (UX-DR21)
**And** the block works the same on phone and laptop, with a loading skeleton while it loads (NFR2, UX-DR21)

**Given** the demo seed
**When** it runs
**Then** one invented alert for the demo clinic exists so the block can be demonstrated before real alert sources arrive in later epics (FR-48)
**And** a Patient cannot read any alert and Staff of Clinic X cannot read Clinic Y's, proven by pgTAP (FR-4, FR-5)

### Story 3.3: Email delivery of notifications by the database scheduler

As a patient or staff member,
I want important updates to also reach my email,
So that I do not have to keep the app open to know something happened.

**Acceptance Criteria:**

**Given** pending notifications
**When** the hourly scheduled job runs in the database
**Then** it calls the sender route through `pg_net` with a signed header, and the route accepts only signed calls and answers an unsigned call with a refusal (AR12, AR6)
**And** the sender is the only code that reads pending notifications with the service-role key, inside `lib/privileged`, which takes no clinic from input (AR6)

**Given** a pending email notification
**When** the sender delivers it
**Then** the email has a subject and body with no health content, only a prompt to open the app, and the status becomes sent (FR-46, AR12)
**And** locally the message appears in Mailpit

**Given** a failed send
**When** the sender retries
**Then** up to three attempts are made with increasing delay, each failure records its error text, and after the last the status is failed (FR-46)
**And** the in-app notification still exists after a failed email (FR-46)

**Given** the scheduler runs twice for the same window
**When** both complete
**Then** no notification is sent twice and a pgTAP or integration test proves it (AR12, NFR7)

**Given** an email provider not yet configured
**When** the app runs in the prototype
**Then** it sends through the development mail setup, and the provider and domain are changed only by configuration (FR-46, AR25)

### Story 3.4: Rate limits and browser hardening

As a patient or staff member,
I want the sign-in and invite pages protected against repeated guessing,
So that nobody can break into an account by trying again and again.

**Acceptance Criteria:**

**Given** the sign-in, invite, resend and upload endpoints
**When** a client exceeds the limit
**Then** the endpoint answers with the `rate_limited` result and a message saying when to try again (AR21, AR7)
**And** the limit applies per email address and per network address, and a legitimate user under the limit is unaffected

**Given** any page
**When** it loads
**Then** a strict content security policy and frame, referrer and permissions headers are set (AR21)
**And** an automated check fails if a response is missing the headers

**Given** a repeated request for a link
**When** it comes within the cooldown window
**Then** it is refused and the message shows the seconds left (UX-DR21)
**And** the cooldown applies whether or not the email exists, so the response does not reveal that (AR16)

**Given** unit tests
**When** they run
**Then** they cover under-limit, at-limit, over-limit and the window resetting (AR21)

### Story 3.5: Send an invite to a patient

As a coordinator,
I want to send a patient an invite from their record,
So that they can open their plan on their own phone.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** an `invites` table exists, owned by the `access` module, storing a hashed token, the email, `clinic_id`, role patient, the patient, an expiry and a used time, with row-level security so only Staff of the clinic can create or read invites, and pgTAP tests (AR16, AR18)

**Given** a patient record
**When** Staff press Send invite on Overview, or choose "Send invite now" at the end of onboarding
**Then** an invite is created through `lib/privileged`, which creates the patient's sign-in account with `app_role` patient and links it to the patient record, taking clinic and role from the invite row and never from input (AR6, AR16, FR-19)
**And** an email with a single-use link and a code is queued through `app.emit_event`, and Overview shows the invite status "Sent" with the time (FR-19)

**Given** an invite already sent
**When** Staff press Resend
**Then** a new invite replaces the old, the old link stops working, and the cooldown and rate limit apply (FR-19, AR16)

**Given** onboarding
**When** the coordinator finishes
**Then** the success screen shows the invite status and an "Add documents now" card that is disabled with the words "Documents come next" until the Documents epic is built (UX-DR14)
**And** a Patient role cannot send invites (FR-3)

**Given** an invite expiry
**When** it passes
**Then** the link is refused with the message "That link has expired. Ask your clinic for a new one." `[ASSUMPTION: 24 hours]` (FR-19)

### Story 3.6: Redeem an invite and sign in by link or code

As a patient,
I want to open my invite and sign in without a password,
So that I can see my information without learning a new system.

**Acceptance Criteria:**

**Given** the invite email
**When** the patient opens the link on a phone
**Then** a page shows "Open your AyurSaathi account" with one button, and pressing the button redeems the invite and signs the patient in (FR-2, AR16)
**And** merely loading the link, as a mail scanner would, does not use it up, proven by a test that requests the page by GET and then redeems (AR16)

**Given** the link fails or has been used
**When** the patient is shown the sign-in screen
**Then** it offers a six-digit code field using one-time-code autofill, with the words "Type the code from the email" (FR-2, UX-DR27)
**And** the message for a used or expired link is "That link has already been used or has expired. Type the code from the email, or ask for a new link." (FR-2, UX-DR21)

**Given** a returning patient with no invite
**When** they enter their email on the sign-in screen
**Then** a new link and code are sent, the response is the same whether or not the email exists, and the cooldown and rate limit apply (FR-2, AR16, AR21)

**Given** a link or code
**When** it expires
**Then** it is refused, the patient can still sign in with a valid code until it expires, and the expiry period is stated on the screen and in the email `[ASSUMPTION: one hour]` (FR-2, NFR8)

**Given** a signed-in patient
**When** they request any clinic route
**Then** they receive "You do not have access to this page." with a link to their home (FR-3)
**And** public sign-up stays disabled and the redirect address is limited to the configured allowlist (AR16)

### Story 3.7: Patient Home with the journey bar and updates

As a patient,
I want a Home screen that shows where I am in my journey and what is new,
So that I know what happens next without searching WhatsApp.

**Acceptance Criteria:**

**Given** a signed-in patient
**When** Home loads
**Then** it shows a greeting, a compact "Step N of 6, Phase" line with a six-segment bar, completed steps marked "Done" and the current step "Now", and the journey bar reads to a screen reader as "Step 4 of 6, Arrival, now" (FR-12, UX-DR6, UX-DR23)
**And** a card for today shows what matters now, or "Nothing is planned for today." when there is nothing (FR-12)

**Given** the patient shell
**When** it renders
**Then** the bottom bar shows Home, Plan, Documents and Check-in with icons and labels and 56px targets, and Plan, Documents and Check-in show their empty states ("Your plan for this day has not been published yet.", "No documents yet.", "Your next check-in is not scheduled.") until their epics are built (UX-DR9, UX-DR21)

**Given** Updates on Home
**When** notifications exist for the patient
**Then** they list newest first with "New" in words, and opening one marks it read, with a Patient seeing only their own (FR-45, FR-5)
**And** the footer shows the clinic phone and "In an emergency, call your local emergency number." (UX-DR22)

**Given** a phone under 600px and a laptop
**When** Home is viewed
**Then** it is one column up to 560px wide, centred, at 18px body text and usable at 200% zoom without truncated labels (UX-DR2, UX-DR24, UX-DR23)
**And** the patient sees no clinic-area navigation and no other patient's data, proven by an end-to-end test with Patient A and Patient B (FR-5, AR18)

## Epic 4: Arrival

The clinic enters pickup and stay, the patient adds flight details and sees the arrival-day card, and taps I have landed or I need help. The coordinator is alerted. Covers FR-25, FR-26, FR-27, FR-28, FR-29, FR-30. The `arrival` module owns `flights`, `pickups`, `accommodations` and `arrival_events`; alerts are raised only through `app.emit_event` (AR8, AR12). This epic completes the walking skeleton and gives the needs-attention block its first real alerts.

### Story 4.1: Flight details

As a coordinator or patient,
I want to enter the patient's flight number and arrival time,
So that everyone knows when to expect the patient.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** a `flights` table exists, owned by the `arrival` module, with `clinic_id`, the episode, flight number, airport, arrival instant in UTC, who entered it and who last changed it, with row-level security and pgTAP tests (AR3, AR4, AR8, AR18)
**And** Staff can read and write flights of their clinic, a Patient can read and write only the flights of their own episode, and a Patient cannot read another patient's flight (FR-5, FR-25)

**Given** the patient record's Arrival tab
**When** Staff open it
**Then** a Flight section shows the flight number and arrival time in the viewer's local time with the clinic time in brackets when the zones differ, or "Not yet confirmed." (FR-25, UX-DR20)
**And** Staff can add or change the flight on phone or laptop (NFR2)

**Given** a signed-in patient
**When** they open Arrival details from Home
**Then** they can add or change their own flight number and arrival date and time (FR-25)

**Given** invalid input
**When** the form is submitted
**Then** a flight number not in airline-code-plus-number form shows "Enter the flight number as airline code and number, for example LX 148." and a missing time shows "Enter the arrival date and time." `[ASSUMPTION: flight number format check]` (FR-25)
**And** the entered time is stored in UTC using the patient's time zone and shown back correctly to a viewer in a different zone (FR-25, AR11)

### Story 4.2: Pickup details

As a coordinator,
I want to enter the car and driver who will meet the patient,
So that the patient knows who is meeting them.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** a `pickups` table exists, owned by the `arrival` module, with `clinic_id`, the episode, driver name and phone, car, plate, meeting point and pickup time, with row-level security and pgTAP tests (AR3, AR8, AR18)
**And** Staff write pickups, a Patient can only read the pickup of their own episode and cannot write one, and cannot read another patient's pickup (FR-26, FR-5)

**Given** the Arrival tab
**When** Staff enter and save pickup details
**Then** they show in a Pickup section and are visible to the patient (FR-26)
**And** a missing driver phone shows "Not yet confirmed." and does not block saving the rest (FR-26, UX-DR21)

**Given** a phone number
**When** it is saved
**Then** it must include a country code, with the message "Enter the phone number with country code, for example +91 98765 43210." (FR-26)

**Given** a change by Staff
**When** it is saved
**Then** a notification "Your pickup details were updated." is sent to the patient through `app.emit_event`, and the patient's Updates shows it (FR-26, AR12)

### Story 4.3: Accommodation and check-in details

As a coordinator,
I want to enter where the patient is staying and when they can check in,
So that the patient knows where to go.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** an `accommodations` table exists, owned by the `arrival` module, with `clinic_id`, the episode, place, room, check-in time and check-out time, with row-level security and pgTAP tests (AR3, AR8, AR18)
**And** Staff write accommodation, a Patient can only read their own episode's accommodation, and cannot read another patient's (FR-27, FR-5)

**Given** the Arrival tab
**When** Staff save accommodation details
**Then** they show in a Stay section and are visible to the patient (FR-27)
**And** a check-out earlier than check-in is refused with "Check-out must be after check-in." (FR-27)

**Given** a change by Staff
**When** it is saved
**Then** the patient is notified through `app.emit_event` with "Your stay details were updated." (FR-27, AR12)

### Story 4.4: Arrival-day card on the patient's Home

As a patient,
I want one card that shows my flight, who meets me and where I am staying,
So that I have everything I need on arrival day in one place.

**Acceptance Criteria:**

**Given** a patient whose episode has a flight or is in the Arrival phase
**When** Home loads
**Then** an arrival-day card shows the flight number and arrival time in the patient's local time with the Pune time in brackets, the driver's name and phone, the car and meeting point, and the place they stay (FR-28, UX-DR20)
**And** any field Staff have not entered shows "Not yet confirmed." and the card still shows what is known (FR-28, UX-DR21)

**Given** Staff change pickup or stay details
**When** the patient reloads Home
**Then** the card shows the new values (FR-28)

**Given** the card on a phone
**When** it is viewed at 200% zoom and at 320px width
**Then** no label is truncated and the exact values (flight number, phone, plate) are never abbreviated (UX-DR2, UX-DR23)

**Given** a patient with no flight, pickup or stay yet
**When** Home loads
**Then** the card is not shown and Home shows only the journey bar and today card (FR-28)

### Story 4.5: "I have landed" and "I need help"

As a patient,
I want to tell the clinic I have landed or that I need help with my pickup,
So that someone knows and can act.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** an `arrival_events` table exists, owned by the `arrival` module, with `clinic_id`, the episode, event type (landed or help), time and who recorded it, with row-level security and pgTAP tests (AR8, AR18)
**And** a Patient can create events only for their own episode and cannot read another patient's events (FR-5)

**Given** the arrival-day card
**When** the patient taps "I have landed"
**Then** an event is saved, a Coordinator alert and notification are raised through `app.emit_event` with a `dedupe_key`, and the screen says "Thank you. Your coordinator has been told." with the clinic phone (FR-29, AR12)
**And** tapping twice raises one alert, not two (FR-29, NFR7)

**Given** the patient taps "I need help with my pickup"
**When** the event is saved
**Then** the coordinators are alerted, and the screen shows the clinic phone and "For a medical emergency, call your local emergency number." (FR-29, UX-DR22)
**And** the screen states that this tells the coordinator about the pickup and is not for medical emergencies (UX-DR22, BR-06)

**Given** an alert
**When** it appears on Today
**Then** it shows the patient name, the event in words ("Landed" or "Needs help with pickup") and the time (FR-29, UX-DR12)
**And** a Coordinator can mark it handled on the Arrival tab and it moves to resolved (FR-9, FR-29)

### Story 4.6: Alert when the patient changes flight details

As a coordinator,
I want to be told when a patient changes their flight,
So that I can re-plan the pickup in time.

**Acceptance Criteria:**

**Given** a patient edits their flight number or arrival time
**When** the change is saved
**Then** an alert is raised for the coordinators naming the patient and showing the old and new values, through `app.emit_event` (FR-30, AR12)

**Given** Staff edit the same flight
**When** the change is saved
**Then** no alert is raised, because Staff made the change (FR-30)

**Given** the patient edits the flight several times within a short window
**When** the alerts are raised
**Then** repeated edits update the same unresolved alert rather than creating many, and the alert shows the latest change (FR-30, NFR7)

**Given** an alert
**When** the coordinator opens it
**Then** it goes to the Arrival tab's Flight section, and marking it handled resolves it (FR-9, FR-30)
**And** a pgTAP test proves a Patient cannot read alerts (FR-5)

### Story 4.7: Walk the arrival journey end to end

As Ravi, the owner,
I want to walk Anna's arrival journey from invite to landed in one repeatable run,
So that the walking skeleton is proven working, not assumed.

**Acceptance Criteria:**

**Given** a clean demo database and Mailpit
**When** the end-to-end test for UJ-1 runs
**Then** a coordinator creates a patient with an invite, the invite arrives in Mailpit, the patient redeems it on a phone-sized browser, Home shows the journey bar, the patient adds a flight, sees the pickup and stay the coordinator entered, taps "I have landed", and the coordinator's Today shows the alert (UJ-1, FR-1 to FR-30)
**And** the test also runs the failure case, where the link is used by a mail scanner first and the patient signs in with the typed code instead (UJ-1)

**Given** the run
**When** it completes
**Then** the isolation suite is run in the same job and passes, including Patient A against Patient B and Clinic X against Clinic Y for every table added in Epics 1 to 4 (FR-4, FR-5, FR-6)
**And** a short written demo script for the same journey is saved in `docs/demo/arrival.md` for Ravi to follow by hand

**Given** the demo script
**When** Ravi follows it on a phone and a laptop
**Then** every step works as written, and any step that does not is recorded as a defect before the next epic starts (NFR2)

## Epic 5: Plan and patient day

The Doctor records findings, notes and medicines. The coordinator builds, copies and publishes the Day Plan and records treatments given. The patient sees the schedule and diet, and ticks medicines taken. Covers FR-31, FR-32, FR-33, FR-34, FR-35. The `care` module owns `notes`, `medicines`, `medicine_intakes`, `day_plans`, `plan_items`, `treatments_given` and `check_ins` (AR8, AR13). Publishing is one SQL function, `publish_day_plan` (AR14). The app records and alerts; it never advises (BR-06).

### Story 5.1: Doctor's findings and notes

As a doctor,
I want to record post-arrival findings and notes and choose who can see each,
So that the clinical record is complete and the patient sees only what I choose to share.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** a `notes` table exists, owned by the `care` module, with `clinic_id`, the episode, a kind (finding or note), the text, the author, the time and `visibility` of `shared` or `staff_only`, with row-level security (AR8, AR10, AR3)
**And** pgTAP tests prove, using the capability matrix, that a Patient reads only `shared` notes of their own episode, never `staff_only` ones, never another patient's, and cannot write a note (FR-5, FR-31, AR18)

**Given** the Care tab on a patient record
**When** a Doctor adds a finding or note
**Then** the visibility toggle defaults to Staff-only, the current choice is stated in words ("Staff-only. The patient cannot see this." or "Shared with patient"), and a Staff-only note carries the lock marker on the item itself (FR-31, UX-DR8)

**Given** a Coordinator
**When** they open the Care tab
**Then** they read Shared notes only, cannot see Staff-only ones, and the add-note control is not shown (FR-3, FR-31)
**And** a direct write of a note by a Coordinator is refused by policy (FR-3, AR10)

**Given** an Admin
**When** they open the Care tab
**Then** they read Shared notes only `[ASSUMPTION: least privilege until the owner confirms Admin access to Staff-only notes]` (FR-31, AR10)

**Given** a shared note
**When** it is saved
**Then** the patient is notified "Your doctor added a note." through `app.emit_event` with no note text in the email (FR-31, AR12)

### Story 5.2: Prescribe and change medicines

As a doctor,
I want to record the medicines I prescribe and change a dose without losing the history,
So that the patient sees the current course and the clinic keeps the record.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** a `medicines` table exists, owned by the `care` module, with `clinic_id`, the episode, name, dose, schedule, start date, duration in days, end date, prescriber and status, with row-level security and pgTAP tests (AR3, AR8, AR18)
**And** a Doctor writes medicines, a Coordinator and Admin read them, and a Patient reads only their own episode's medicines (FR-32, FR-5)

**Given** the Care tab
**When** a Doctor adds a medicine
**Then** name, dose, schedule, start date and duration are required, the end date is calculated, and each missing field has a specific message (FR-32)

**Given** a current medicine
**When** the Doctor changes its dose or schedule
**Then** the existing row is ended on that day and a new row is created, so the earlier dose stays in history (FR-32, FR-39)
**And** the patient is notified "Your medicines were updated." with no medicine names in the email (AR12)

**Given** a medicine whose duration has passed
**When** the lists are shown
**Then** it leaves the current course and appears under earlier medicines (FR-32)

**Given** a Coordinator
**When** they attempt to add or change a medicine
**Then** the control is not shown and a direct write is refused by policy (FR-3, FR-32)

### Story 5.3: Build a Day Plan and the Plans screen

As a coordinator,
I want to build a day's plan of treatments, meals, medicines and the stay for a patient,
So that the patient will know what happens tomorrow.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** `day_plans` and `plan_items` tables exist, owned by the `care` module, with `clinic_id`, one plan per episode per date (unique), a status of draft or published, and items of kind therapy, meal, medicine, review or other with a start time, title, detail and therapist name, with row-level security and pgTAP tests (AR3, AR8, AR18)
**And** a Patient can never read a draft plan, and reads a published plan of their own episode only (FR-5, FR-33, AR10)

**Given** the Care tab
**When** Staff choose a date and add items
**Then** items group under Morning, Midday and Evening, can be edited, reordered and deleted, and the plan shows a Draft badge with the date it was saved (FR-33, UX-DR16)
**And** the stay for that date is shown as a read-only line from the Accommodation section (FR-33, FR-27)

**Given** the Plans screen in the clinic area
**When** a Coordinator opens it
**Then** it lists patients currently in the Care phase with tomorrow's plan status (Not started, Draft or Published), and tapping one opens that plan (FR-33, UX-DR13)

**Given** the Day Plan builder on a phone and on a laptop
**When** the same plan is edited on each
**Then** the data and the actions are the same, and the date strip works by touch and by keyboard (NFR2, UX-DR23)

### Story 5.4: Copy yesterday and publish to the patient

As a coordinator,
I want to copy yesterday's plan and publish tomorrow's in one step,
So that a routine day takes a minute, not twenty.

**Acceptance Criteria:**

**Given** a patient with a plan for the previous date
**When** Staff choose Copy yesterday on a new date
**Then** yesterday's items are copied into a Draft for the chosen date with times and details, and the draft can be edited before publishing (FR-33)
**And** copying onto a date that already has a plan asks for confirmation and names what will be replaced (UX-DR26)

**Given** a Draft plan
**When** Staff choose Publish to patient
**Then** a confirmation names the patient and the date, and on confirming the SQL function `publish_day_plan` sets the status to published, records the time and creates the patient notification in one transaction (FR-33, AR14, AR12)
**And** the badge changes to "Published at 17:42" (UX-DR16)

**Given** the Publish action is submitted twice
**When** the second request arrives
**Then** no second notification is created and the screen says "Already published." (FR-33, AR7, NFR7)

**Given** a published plan that Staff edit and publish again
**When** it is published
**Then** the patient sees the new version and one notification "Your plan for Thursday 12 November was updated." is sent (FR-33)

**Given** a Doctor
**When** they build or publish a Day Plan
**Then** they can, and a Patient role cannot call `publish_day_plan` (FR-3, AR17)
**And** a pgTAP test covers the function as an exposed object (AR18)

### Story 5.5: Record treatments given

As a coordinator,
I want to record the treatments actually given each day,
So that the record shows what happened as well as what was planned.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** a `treatments_given` table exists, owned by the `care` module, with `clinic_id`, the episode, the date, an optional link to the planned item, treatment, therapist name, duration in minutes and notes, with row-level security and pgTAP tests (AR3, AR8, AR18)

**Given** a published Day Plan
**When** Staff open it after the day
**Then** each planned therapy offers "Record as given", prefilled and editable, and a treatment not in the plan can be added (FR-34)
**And** a treatment given can differ from the one planned, and both are kept and shown side by side (FR-34)

**Given** a record
**When** it is saved
**Then** it stores the treatment, therapist name, duration and notes for that date (FR-34)
**And** a duration of zero or negative is refused with "Enter how many minutes the treatment took." (FR-34)

**Given** a Patient
**When** they read their record
**Then** they cannot read treatments-given notes, because the patient's day view shows the plan only, proven by pgTAP (FR-5, FR-34)

### Story 5.6: The patient's Plan tab and day view

As a patient,
I want to see my schedule, meals and current medicines for the day,
So that I know what to expect without asking anyone.

**Acceptance Criteria:**

**Given** a published Day Plan for the patient's episode
**When** the patient opens Plan
**Then** the day view shows the date, then the schedule grouped Morning, Midday and Evening, the meals, and the current medicines, at 18px with exact times in the patient's local time and the Pune time in brackets (FR-35, UX-DR2, UX-DR20)
**And** a date switcher moves between days that have a published plan (FR-35)

**Given** no published plan for a date
**When** the patient opens it
**Then** the screen says "Your plan for this day has not been published yet. Your coordinator will publish it." and shows no draft information (FR-35, UX-DR21)

**Given** the medicines section
**When** it is shown
**Then** it lists the current course only, each with name, dose and schedule, and a "Show earlier medicines" button reveals the history (FR-32, FR-35)
**And** the footer shows the clinic phone and the emergency line, and nothing on the screen explains what a medicine or a score means medically (UX-DR22, BR-06)

**Given** two patients
**When** each opens Plan
**Then** each sees only their own plan, proven by an end-to-end test with Patient A and Patient B (FR-5, AR18)

### Story 5.7: Tick medicines as taken

As a patient,
I want to mark each medicine as taken,
So that the clinic knows I followed my plan and I do not lose track.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** a `medicine_intakes` table exists, owned by the `care` module, with `clinic_id`, the medicine, the date, the slot, the time taken and the source (patient or staff), with row-level security and pgTAP tests (AR3, AR8, AR18)
**And** a Patient can write intakes only for their own medicines and cannot read another patient's (FR-5, FR-35)

**Given** the day view
**When** the patient taps "Taken" on a medicine
**Then** the row reads "Taken at 08:10" in words, not only a tick, and the time and source are stored (FR-35, UX-DR17)
**And** the patient can undo within 10 minutes and not after (UX-DR17)

**Given** Staff open the patient's record
**When** they view the day
**Then** they see which medicines were taken and can record one on the patient's behalf, with source staff (FR-35)

**Given** the same medicine tapped twice quickly
**When** both requests arrive
**Then** one intake exists (FR-35, NFR7)

**Given** the demo journey for UJ-2
**When** the end-to-end test runs
**Then** the coordinator copies yesterday's plan and publishes it, the patient sees it on a phone-sized browser and taps Taken, and the coordinator sees the intake, with the isolation suite passing for every table added in this epic (UJ-2, FR-6)

## Epic 6: Check-in and doctor review

The patient answers a daily check-in. The Doctor reviews check-ins flagged first, adds notes, changes medicines and marks them reviewed, and can edit the check-in questions and flag rules. Covers FR-36, FR-37, FR-38, FR-39 and the Doctor part of FR-8. `check_ins` is one table owned by `care`, with a unique key of episode, kind, template and local date; every flag is written only by the flag-evaluation function; review is one SQL function (AR13, AR14). The app records and alerts. It never interprets answers medically, never tells a patient they were flagged, and applies only rules the Doctor sets (BR-06).

### Story 6.1: The patient's daily check-in

As a patient,
I want to answer a short check-in about my medicines and how I feel,
So that my doctor knows how my treatment is going.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** a `check_ins` table exists, owned by the `care` module, with `clinic_id`, the episode, a kind (daily or follow_up), the questions version it was answered against, the Patient's local date, answers, flags, who reviewed and when, and a unique key on episode, kind, questions version and local date, with row-level security (AR13, AR3, AR8)
**And** a SQL function `create_due_check_in` creates one check-in idempotently and is the only way a check-in row is created (AR13, AR14, NFR7)

**Given** a patient in the Care phase
**When** they open Check-in on or after 06:00 in their local time on a day with no check-in yet `[ASSUMPTION: daily window opens at 06:00 local]`
**Then** that day's check-in is created once and shown as "Question 1 of 5", one question per screen, with large answer buttons, a progress word and a Back button at every step (FR-36, UX-DR18)
**And** opening the tab twice or on two devices creates one check-in (FR-36, NFR7)

**Given** the five sample questions
**When** the patient answers
**Then** the medicines question takes Yes, Partly or No, the score questions take 1 to 5 with words at each end ("Poor" to "Very good"), and the free-text answer is limited to 1,000 characters with a counter `[ASSUMPTION: these answer formats and limits]` (FR-36)
**And** continuing without an answer says "Choose an answer to continue." (FR-36, UX-DR21)

**Given** the last question
**When** the patient reaches the review screen and taps Send
**Then** the answers are saved once, and submitting twice does not create two check-ins (FR-36, AR7)
**And** the screen says "Received. Your doctor reviews check-ins each day." with the clinic phone and the line "For urgent help, call the clinic. In an emergency, call your local emergency number." (FR-36, UX-DR22)

**Given** an already submitted check-in, another patient's, or a staff user
**When** a write is attempted
**Then** it is refused by policy, so a submitted check-in cannot be edited and Patient A cannot read or write Patient B's, proven by pgTAP (FR-5, AR18)
**And** when no check-in is due the tab says "Your next check-in is Friday 13 November at 08:00." in the patient's local time (UX-DR21, UX-DR20)

### Story 6.2: Flag evaluation with sample rules

As a doctor,
I want check-ins marked by rules I set, not rules built into the app,
So that the clinic's judgement, not the software's, decides what needs attention.

**Acceptance Criteria:**

**Given** the flag rules stored in the clinic's settings
**When** a check-in is submitted
**Then** one SQL function evaluates the answers against the rules, writes the flag and the reasons in plain words, and does so in the same transaction as the submission (FR-38, AR9, AR13)
**And** the function contains no clinical threshold of its own, so with an empty rule set no check-in is ever flagged (FR-38, BR-06)

**Given** the sample rule set from the seed
**When** a check-in has medicines answered "No" or any score of 2 or less
**Then** it is flagged with the reason "Medicines: No" or "Sleep: 2 of 5", and the set is labelled "Sample rules. Not clinical advice." wherever it is shown (FR-38, UX-DR22) `[ASSUMPTION: sample rules exist only so the demo can show a queue; the real rules come from the Doctor]`

**Given** a change to the rules in the settings data
**When** the next check-in is submitted
**Then** its evaluation follows the new rules with no code change (FR-38)

**Given** a flagged check-in
**When** the patient views their own check-in or any screen
**Then** no flag, reason or word implying concern is shown to the patient (FR-38, UX-DR22)
**And** pgTAP tests prove a Patient cannot read the flags column and the evaluation function is covered as an exposed object (AR18)

**Given** unit tests
**When** they run for each answer type and for an empty rule set, a rule with a missing question and a score at the boundary
**Then** every case passes (FR-38)

### Story 6.3: The Doctor's Review Queue

As a doctor,
I want a queue of check-ins with the flagged ones first,
So that I look at the patients who need me before the rest.

**Acceptance Criteria:**

**Given** submitted check-ins
**When** a Doctor opens Review on a phone or the Review Queue on a laptop
**Then** the list shows flagged check-ins first, then by time, each with the patient name, the check-in kind and time, a "Needs review" badge with the reason in words and a "Sample rule" badge when the sample rules raised it (FR-37, UX-DR19)
**And** a Doctor sees only check-ins of their own clinic (FR-4, FR-37)

**Given** an empty queue
**When** it loads
**Then** it says "Nothing to review right now." and while loading shows a skeleton with the word "Loading" (UX-DR21)

**Given** a check-in is flagged on submission
**When** it is saved
**Then** an alert is raised for the Doctors through `app.emit_event` with a `dedupe_key`, and it shows in the needs-attention block on Today with the patient name and time (FR-9, FR-37, AR12)

**Given** a Coordinator or Admin
**When** they open the queue
**Then** they can read it but not review, and a Patient cannot see it (FR-3, FR-5)

**Given** a laptop at 1024px or wider
**When** the queue is shown
**Then** the list sits at 360px beside the review pane, and on a phone each row opens the pane full screen, with the same actions on both (NFR2, UX-DR10, UX-DR24)

### Story 6.4: Review a check-in

As a doctor,
I want to read a check-in, add a note, change a medicine and mark it reviewed from one screen,
So that I do not have to leave the queue to act.

**Acceptance Criteria:**

**Given** a check-in in the queue
**When** the Doctor opens it
**Then** the review pane shows the answers in words, the patient's recent notes and current medicines, and the actions Add note, Change medicine and Mark reviewed (FR-39, UX-DR19)

**Given** Add note
**When** the Doctor writes it
**Then** the visibility toggle defaults to Staff-only with the words "Staff-only. The patient cannot see this.", and choosing "Shared with patient" is stated in words (FR-31, FR-39, UX-DR8)

**Given** Change medicine
**When** the Doctor changes a dose
**Then** it uses the medicine-change function from Story 5.2 so the earlier dose stays in history (FR-32, FR-39)

**Given** Mark reviewed
**When** the Doctor confirms
**Then** the SQL function `review_check_in` records who and when, saves any note and medicine change and resolves the related alert, all in one transaction, so a failure part-way leaves nothing half-done (FR-39, AR14)
**And** the row leaves the queue and the Today count drops (FR-39, FR-9)

**Given** Mark reviewed submitted twice
**When** the second request arrives
**Then** it does nothing new and the screen says "Already reviewed." (FR-39, AR7, NFR7)

**Given** the patient's next visit to the app
**When** a shared note or changed medicine exists
**Then** the patient sees the shared note and the current medicine, and never a Staff-only note (FR-31, FR-32, FR-5)
**And** a Coordinator calling `review_check_in` is refused, proven by pgTAP (FR-3, AR17, AR18)

### Story 6.5: The Doctor edits check-in questions and flag rules

As a doctor,
I want to set the check-in questions and the flag rules for my clinic,
So that the check-in asks what I care about and flags what I decide.

**Acceptance Criteria:**

**Given** a Doctor
**When** they open More, Settings, Clinical rules
**Then** they can edit the questions (text, answer type, order, add and remove within limits) and the flag rules (for example "medicines is No", "any score is 2 or less") through a plain form, each validated by its schema (FR-8, UX-DR28, AR9)
**And** the page carries the "Sample rules. Not clinical advice." badge while the sample set is in use (UX-DR22)

**Given** the Doctor saves their own rule set
**When** it is stored
**Then** the badge changes to "Set by the clinic's doctor on 12 November" and the new rules apply to the next check-in only, without changing any check-in already answered (FR-8, FR-38)
**And** each check-in keeps the version of the questions it was answered against, so old answers stay readable (FR-36, AR13)

**Given** an invalid set, for example no questions or a rule that names a question that does not exist
**When** the Doctor saves
**Then** it is refused with a message that says what to fix and the input is kept (FR-8, UX-DR21)

**Given** an Admin or Coordinator
**When** they request the Clinical rules screen or call the save
**Then** the screen is hidden from their navigation and the write is refused by policy, as Story 1.4's tests assert for this section (FR-8, FR-3, AR9)

**Given** a laptop and a phone
**When** the Doctor edits the same set on each
**Then** the data and the actions are the same (NFR2)

### Story 6.6: Walk the check-in and review journey

As Ravi, the owner,
I want to walk Dr. A's morning review from the patient's check-in to the reviewed note in one repeatable run,
So that the whole care loop is proven working.

**Acceptance Criteria:**

**Given** a clean demo database
**When** the end-to-end test for UJ-3 runs
**Then** a patient in Care submits a check-in answering "No" to medicines, the Doctor's Today shows the alert, the Review Queue lists it first with its reason, the Doctor adds a shared note, changes a medicine and marks it reviewed, and the patient then sees the shared note and the changed medicine (UJ-3, FR-36 to FR-39)
**And** the same run confirms the patient never sees a flag and a Coordinator cannot review (BR-06, FR-3)

**Given** the run
**When** it completes
**Then** the isolation suite passes for every table added in Epics 5 and 6, including Patient A against Patient B and Clinic X against Clinic Y, and the coverage check finds no untested object (FR-4, FR-5, FR-6, AR18)
**And** a written demo script for the care loop is saved in `docs/demo/care.md` for Ravi to follow by hand

**Given** the demo script
**When** Ravi follows it on a phone and a laptop
**Then** every step works as written, and any step that does not is recorded as a defect before the next epic starts (NFR2)

<!-- NEXT EPIC -->
