---
status: draft
stepsCompleted: ['step-01-validate-prerequisites', 'step-02-design-epics', 'step-03-create-stories', 'step-04-final-validation']
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

AR26: Definition of done for every story. Policies and pgTAP isolation tests ship in the same change as any new table, view, function or bucket (AR16, AR18); the demo seed is extended with invented rows so the journey can be walked (FR-48); every UI string lives in `messages/en.json` (NFR3); status is never colour alone and focus, targets and 200% zoom meet the accessibility floor (NFR8, UX-DR23); no health data is logged (NFR5); the typed Result and idempotency rules of AR7 are followed; every patient route passes the automated accessibility check; events are raised only by triggers and named SQL functions; patients write only through named SQL functions, never directly to a table.

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
UX-DR20: Time display. "Thu 12 Nov, 14:35 CET (Pune 19:05)", where the bracketed city label and zone come from Clinic Settings, shown when the viewer's zone differs from the clinic's. Arrival times are shown in the arrival airport's local time.
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
**Implementation notes:** Starts with the starter scaffold (AR1), CI, and the pgTAP harness with the coverage check (AR18). Includes the Admin part of FR-8; the Doctor part is in Epic 6. Includes the isolation harness and capability matrix, automated accessibility checks, feasibility stories for spikes S-3, S-4 and S-5 with no UI, Admin management of staff users, and the per-clinic release routine (AR19). Delivers: signed-in Today (empty), branding change, staff management, green isolation suite.

### Epic 2: Patient records and onboarding
The coordinator adds a patient in three steps (details, consent, review and invite), saves drafts, is warned of duplicates, and staff can list, search, filter and move patients between phases or start a new episode for a returning patient.
**FRs covered:** FR-9, FR-10, FR-11, FR-13, FR-14, FR-15, FR-16, FR-47
**Implementation notes:** FR-9 here covers the patient list, search and phase filter only; the needs-attention block is in Epic 3. Also covers the episode lifecycle (one open episode), correcting and removing patients. Sending the Invite arrives in Epic 3. Delivers: add a patient end to end on phone and laptop.

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

As a builder,
I want the app scaffolded from the official Next.js and Supabase starter with versions pinned,
So that every later story builds on one running, reproducible base.

**Acceptance Criteria:**

**Given** an empty repository branch
**When** the scaffold is created from the official `with-supabase` example
**Then** `next`, `react`, `@supabase/supabase-js` and `@supabase/ssr` are pinned to exact versions (no `latest`) and Node 24 LTS is set in the project settings, with TypeScript pinned to 5.x, Zod, Vitest, Playwright and the Supabase CLI at the versions in the architecture spine (AR2)
**And** the sample sign-up and password pages that allow public sign-up are removed, and `lib/supabase` is replaced by `lib/db` (AR1)

**Given** the scaffold
**When** `npm run lint`, `npm run typecheck` and `npm run build` are run
**Then** all three pass with no errors
**And** `proxy.ts` is present and refreshes the session by calling `getClaims`, never `getSession` (AR5)

**Given** a clean clone and a local Supabase started with the Supabase CLI
**When** a developer follows the README's three commands
**Then** the app starts on localhost and shows a public landing page
**And** environment variables are read from a documented `.env.example`; no secret is committed and the service-role key is not exposed to the browser (AR6, NFR6)
**And** a `/api/health` route answers that the app is running and returns no data (BRD NFR-10)

**Given** the folder layout in the architecture spine
**When** the scaffold is inspected
**Then** `app/(public)`, `app/(patient)`, `app/(clinic)`, `app/api/jobs`, `modules/`, `lib/`, `messages/en.json`, `supabase/migrations`, `supabase/tests`, `supabase/seed.sql` and `clinics.json` exist
**And** where a pinned version does not build (Tailwind 4, TypeScript, Serwist), the fallback chosen is recorded in the README with the reason

### Story 1.2: CI pipeline, policy checks and code rules

As a builder,
I want continuous checks that fail the build when a table is unprotected or code breaks the project's rules,
So that later stories cannot ship an unsafe table or leak health data by accident.

**Acceptance Criteria:**

**Given** a pull request
**When** CI runs
**Then** it runs lint, typecheck, unit tests and a migration check, and a failed step fails the pull request (AR23)

**Given** the migrations folder
**When** the policy check runs
**Then** it fails if any table in an exposed schema has row-level security disabled or no policy, or if any policy uses an unconditional `true` (AR3)
**And** a deliberately unprotected fixture table, kept only in a test fixture, makes the check fail with a message naming the table, while a clean fixture passes

**Given** the write-path rule
**When** lint runs
**Then** it fails if any file other than `modules/*/actions.ts`, `lib/privileged/*` and SQL migrations calls `.insert`, `.update`, `.upsert`, `.delete` or `.rpc` on the database client (AR7, AR22)
**And** an import-boundary rule fails the build when a module imports another module's internals instead of its exported functions (AR8)

**Given** the logging rule
**When** lint runs
**Then** `console.*` is banned in application code, and the only logger accepts an event name and a record of ids, so a request body, patient field or health value cannot be logged (NFR5, AR20)

**Given** the audit-ready conventions
**When** the migration check runs
**Then** it fails if a clinic-owned table lacks `created_at` or `updated_at`, or if a clinical or logistics table lacks `created_by` (AR22)

### Story 1.3: Isolation test harness, coverage check and capability matrix

As a builder,
I want a test harness that acts as each kind of user and refuses to pass while any object is untested,
So that isolation is proven for every table as it is added, not assumed.

**Acceptance Criteria:**

**Given** the database tests (`supabase test db` with pgTAP)
**When** a test author needs to act as a user
**Then** helper functions set the token claims (`app_role`, `clinic_id`, patient) directly in the test session for an anonymous user, Patient A, Patient B, Staff of Clinic X, Staff of Clinic Y and a demoted user, so tests need no sign-in (FR-6)
**And** the helpers are documented in `supabase/tests/README.md`

**Given** the coverage check
**When** it runs in CI
**Then** it lists every table, view, exposed function and storage bucket and fails the build if any has no isolation test, naming the object (AR18)
**And** a fixture with one untested table proves the check fails

**Given** `supabase/capability-matrix.json`
**When** it is created
**Then** it holds the PRD role table (each data area against Patient, Coordinator, Doctor, Admin with none, read or write) and a generator produces pgTAP expectations from it (AR10)
**And** CI fails when a policy's behaviour in the tests disagrees with the matrix, so policies, tests and the PRD cannot drift

### Story 1.4: Design foundation, demo shell and accessibility checks

As a staff member or patient,
I want every screen to carry the AyurSaathi look, the demo notice and an accessible baseline,
So that the app is consistent, legible and cannot be mistaken for a real system.

**Acceptance Criteria:**

**Given** the app in a browser
**When** any page loads
**Then** the colour, type, spacing and radius tokens from `DESIGN.md` are applied as theme variables, in light and dark themes, following the system setting unless the user chose otherwise (UX-DR1, UX-DR3)
**And** Atkinson Hyperlegible Next and Source Serif 4 are self-hosted, with body text 18px on patient routes and 16px on clinic routes (UX-DR2)

**Given** any page
**When** it renders
**Then** a "Demo data. Not real patients." ribbon shows at the top and cannot be dismissed (UX-DR11)

**Given** the shared components
**When** a primary, secondary and destructive button, a card and an input are rendered
**Then** each matches `DESIGN.md` (56px patient and 48px staff buttons, label above the input, error text with an icon and the words of the fix) and has a 3px focus ring with a 2px offset in both themes (UX-DR4, UX-DR5, UX-DR23)

**Given** text at 200% zoom and a 320px-wide screen
**When** the demo shell is viewed
**Then** no horizontal scroll appears and no label is truncated (NFR8, UX-DR23)

**Given** an unexpected error on any screen
**When** it occurs
**Then** the message reads "Something went wrong. Your information is safe. Try again. Reference: ABC123." with a reference ID, and no data, stack trace or field value is shown or logged (NFR5, UX-DR21)

**Given** a developer adds UI text
**When** lint runs
**Then** the string must come from `messages/en.json`, and a hard-coded UI string in a component fails the check (NFR3, UX-DR25)

**Given** the Playwright suite
**When** it runs in CI
**Then** an automated accessibility check (axe-core) runs on every patient route that exists and fails CI on any serious or critical violation; each later story's routes are added to it (NFR8, UX-DR23)

### Story 1.5: Clinic record and settings store

As an Admin,
I want my clinic's details, branding, terminology and clinical configuration stored as settings,
So that nothing specific to one clinic lives in code and each part can be edited by the right role.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** `clinics` and `clinic_settings` tables exist, owned by the `settings` module, each with `clinic_id`, row-level security and policies that check the clinic before the role (AR3, AR4, AR8)
**And** `clinic_settings` holds versioned sections validated by Zod on read and write: contact (clinic phone in international format, display city label, default time zone), branding, terminology (including the six phase names), daily check-in questions, follow-up check-in questions, flag rules, consent text versions and templates (AR9, BR-11)

**Given** the claim helper functions
**When** this story is applied
**Then** `app.user_role()`, `app.user_clinic()`, `app.user_patient_id()` and `app.is_staff()` exist as invoker functions that read only the token claims, and this story's policies use them (AR5, AR17)

**Given** the seed
**When** it runs
**Then** one clinic, "Ayurvedgram (demo)", exists with an invented phone number, the city label "Pune", the zone Asia/Kolkata, default terminology, five sample daily questions, a sample follow-up set covering how the patient feels, medicines taken and diet issues, a sample flag-rule set labelled "Sample rules. Not clinical advice." and sample consent wording labelled "Sample wording. Not legal text." (FR-8, FR-16, FR-38 groundwork, FR-42 groundwork)

**Given** the section policies from the capability matrix
**When** each role writes each section
**Then** Admin writes contact, branding, terminology and consent text; Doctor writes both question sets and flag rules; a Coordinator writes nothing; every section has a pgTAP case per role (FR-8, AR10)
**And** Staff read every section, a Patient reads contact, branding, terminology, both question sets and the current consent text, and a Patient never reads flag rules (FR-5, BR-06)

**Given** two users save the same section at the same time
**When** the second save arrives
**Then** it carries the section version it was edited from and is refused with `conflict` if the version moved, and the second user keeps their input (AR7)

**Given** two clinic rows in the test database
**When** Staff of Clinic X read `clinic_settings`
**Then** they receive no rows of Clinic Y and cannot write them, proven by pgTAP (FR-4)
**And** application code reads settings only through `modules/settings` (AR8)

### Story 1.6: Staff sign-in and roles

As a coordinator, doctor or admin,
I want to sign in with my email and password and land in the clinic area,
So that I reach only what my role allows.

**Acceptance Criteria:**

**Given** a staff account
**When** the user enters the correct email and password
**Then** they are signed in and land on the clinic area (FR-1)
**And** public sign-up is disabled, the token hook gives no role to an account not provisioned by an Admin, and Supabase Auth's rate limits for password sign-in are configured and documented (AR16, AR21)

**Given** a wrong password
**When** the user submits
**Then** a plain message says the email or password is not right, with the same message whether or not the email exists, and the input is kept (FR-1)

**Given** a signed-in user
**When** the token is issued
**Then** an auth hook adds `app_role` (patient, coordinator, doctor or admin) and `clinic_id` from `app_metadata` without overwriting `role`, and access tokens expire in 10 minutes or less (AR5)
**And** this story extends `app.user_role()` to require an active profile, so a disabled user's old token is refused at once, proven by a pgTAP case (AR5)

**Given** a signed-in account with no role
**When** it reaches the app
**Then** it sees "You do not have access to this page." with a sign-out button and nothing else (FR-3)

**Given** a seeded test account with the patient role
**When** it requests any clinic route
**Then** it receives "You do not have access to this page." with no detail about records (FR-3)
**And** the `profiles` table has policies and isolation tests, and the session ends when the user signs out (AR18)

### Story 1.7: Clinic area shell and an empty Today

As a coordinator or doctor,
I want a navigation shell that works on my phone and my laptop and a Today screen,
So that I always know where I am and what to open next.

**Acceptance Criteria:**

**Given** a signed-in staff user on a phone under 600px
**When** the clinic area loads
**Then** a bottom bar shows Today and More, each with an icon and a label, the current item marked with a bar and a bold label (UX-DR9)
**And** each later story that adds a screen registers its own navigation item for the roles allowed (Patients in 2.1, Review in 6.3 for Doctors, Plans in 5.3 for Coordinators, Settings for Admins), so no role ever sees a dead link (UX-DR28)

**Given** a laptop at 1024px or wider
**When** the clinic area loads
**Then** a 240px sidebar shows the same items and the clinic name, ready for list-and-detail screens (UX-DR10, UX-DR24)

**Given** More
**When** it opens
**Then** it offers Settings, with the theme choice (System, Light or Dark, remembered on that device) and Sign out, which ends the session (UX-DR1)

**Given** the Today screen
**When** there is nothing to show
**Then** it says "Nothing needs attention." with the clinic name from settings, and shows a skeleton with the word "Loading" while it loads (UX-DR21)
**And** on a throttled mobile connection typical of the clinic's phones it becomes usable within about 3 seconds (BRD NFR-03)

**Given** the same staff user on a phone and a laptop
**When** they use the available actions
**Then** the same data and actions are present on both, every item is reachable by Tab, and the focus ring shows (NFR2, UX-DR23, UX-DR26)

### Story 1.8: Admin sets clinic details, branding and terminology

As an Admin,
I want to set my clinic's name, contact details, branding and terminology, including the phase names,
So that the app speaks my clinic's language and shows the right phone number without anyone changing code.

**Acceptance Criteria:**

**Given** a signed-in Admin
**When** they open More, Settings, Clinic
**Then** they can edit the clinic name, phone, display city label, default time zone, brand colours and terminology labels, including the six phase names, each validated (name and labels 1 to 40 characters, phone in international format) (FR-8, BR-11)

**Given** a changed label or phase name
**When** the Admin saves
**Then** the new wording shows wherever it is used on the next load, including the phase chips and journey bar, with no code change, proven by a test that renames a phase (FR-8, BR-11)
**And** no screen text names Ayurvedgram or Pune except through Clinic Settings (FR-8)

**Given** a brand colour
**When** the Admin saves
**Then** it is refused if text on it fails the contrast check against either the light or the dark theme surface, with a message naming the colour and the required contrast (NFR8)

**Given** a Coordinator or Doctor
**When** they request the Clinic settings screen or call the save
**Then** the screen is not in their navigation and the write is refused by policy (FR-8, FR-3)
**And** a failed or conflicting save keeps the Admin's input and says what to do next (UX-DR21)

### Story 1.9: Installable app and offline shell

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

### Story 1.10: Demo seed and isolation fixtures

As a builder,
I want a repeatable demo data set of invented people and two clinics,
So that I can demonstrate every journey and the tests have realistic fixtures.

**Acceptance Criteria:**

**Given** a clean local database
**When** the seed runs
**Then** it creates, from invented data only, one demo clinic with a Coordinator, a Doctor and an Admin, and, in the test database only, a second clinic with its own staff (FR-48, AR4)
**And** every name, email, phone and passport number is invented (NFR1)

**Given** the seed
**When** it runs a second time
**Then** it inserts only rows that are missing and never duplicates, and a separate `seed:reset-demo` command restores every demo row to its canonical state before a demo (FR-48)

**Given** the isolation harness from Story 1.3
**When** the fixtures are loaded
**Then** Patient A, Patient B, Staff of Clinic X and Staff of Clinic Y exist for the tests, with patients' rows added by later epics as their tables arrive (FR-5, FR-6)

**Given** a hosted clinic project
**When** the seed is applied there
**Then** only the one demo clinic is created and never the second clinic (AR4)
**And** the seed command refuses to run if the target is not marked as a demo environment (NFR1)

### Story 1.11: Feasibility check: region and sign-in link delivery

As a product owner,
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

### Story 1.12: Feasibility check: phone uploads, HEIC and signed links

As a product owner,
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

### Story 1.13: Admin manages staff users

As an Admin,
I want to add staff, set their role, disable and re-enable them, and help them back in when they forget their password,
So that only the right people can use the clinic area.

**Acceptance Criteria:**

**Given** an Admin
**When** they open More, Settings, People
**Then** a list shows each staff member's name, email, role and whether the account is Active or Disabled (FR-3, UX-DR28)

**Given** the Add staff form
**When** the Admin enters a name, an email and a role (coordinator, doctor or admin)
**Then** the account is created through `lib/privileged` with the clinic taken from the Admin's verified token, never from input, and the role and clinic stored in `app_metadata` (AR6, AR5)
**And** the new staff member receives an email to set their own password (locally in Mailpit), and the Admin can resend it
**And** an email already used by any account, staff or patient, is refused with `conflict` and a plain message (FR-1)

**Given** a staff member's role is changed, or the account is disabled or re-enabled
**When** the Admin confirms, with a confirmation that names the person
**Then** policy checks follow the change at once, an old token no longer works (pgTAP), and the person's app refreshes its token and navigation on the next request instead of showing actions that would fail (AR5, AR18)
**And** the last Admin cannot be demoted or disabled and an Admin cannot change their own role, each with a message that says why (FR-3)
**And** records written by a disabled user keep their author, shown as "Former staff: <name>"

**Given** a staff member who forgot their password
**When** they choose "Forgot password" on the staff sign-in screen
**Then** a reset email is sent with the same response whether or not the email exists, a cooldown on repeats, and no reset is sent to patient accounts (FR-1, AR16)

**Given** a Coordinator or Doctor
**When** they request People or call its actions
**Then** the screen is not in their navigation and the writes are refused by policy, and Staff of Clinic X cannot list or change Staff of Clinic Y, proven by pgTAP on `profiles` (FR-3, FR-4, AR10)

### Story 1.14: Release routine and clinic manifest

As a builder,
I want one repeatable routine that updates every clinic's database before its app, without breaking a clinic part-way,
So that clinic projects never drift apart.

**Acceptance Criteria:**

**Given** `clinics.json`
**When** it is read
**Then** it lists each clinic's name, Supabase project reference and deployment name and contains no secret (AR19)

**Given** a release
**When** the release command runs
**Then** for each clinic in turn it checks CI passed, applies pending migrations, then deploys that clinic's app, and on a failure it stops, names the clinic that failed and lists which clinics are already released (AR19)
**And** a dry-run option lists what would change for each clinic without changing anything

**Given** migrations
**When** they are written
**Then** each one must keep the previous app version working (expand first, remove later), so a clinic whose database was migrated but whose app was not deployed still works, checked by running the previous app's tests against the migrated schema in CI (AR19)

**Given** the migrations folder
**When** CI runs
**Then** a check fails any change to a migration file that has already been released, because changes are forward-fix only (AR19)

**Given** a manifest with one clinic and one with two
**When** the dry run is executed against each
**Then** both work, so adding a second clinic needs no change to the routine, and the steps are documented in the README for someone other than Ravi to follow (AR2, AR19)

## Epic 2: Patient records and onboarding

The coordinator adds a patient in three steps (details, consent, review and invite), saves drafts, is warned of duplicates, and staff can list, search, filter, correct and move patients between phases or start a new episode for a returning patient. Covers FR-9 (list, search and filter), FR-10, FR-11, FR-13, FR-14, FR-15, FR-16, FR-47. The Invite is sent in Epic 3; the needs-attention block is built in Epic 3; documents and the patient photo are added after creation in Epic 7. The `patients` module is the only writer of `patients`, `episodes`, `phase_events` and `consents`; the `onboarding` module owns only `onboarding_drafts` and calls the `patients` module's exported functions (AR8). A patient has at most one open episode; every patient-facing screen reads that open episode only.

### Story 2.1: Patient list with phase, search and filter

As a coordinator or doctor,
I want to see my clinic's patients with their current phase and find one quickly,
So that I can open the right record in a few taps.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** `patients` and `episodes` tables exist, owned by the `patients` module, each with `clinic_id`, row-level security, Staff policies, and a Patient able to read only their own rows through `app.user_patient_id()` (AR3, AR4, AR8)
**And** `episodes` has a `closed_at` time and a unique rule allowing at most one open episode per patient, and a helper `app.current_episode()` returns the caller's open episode for patient-facing policies and screens (FR-11)
**And** pgTAP tests prove Patient A cannot read or write Patient B's rows, Staff of Clinic X cannot read Clinic Y's, and a Patient cannot write a patient or episode row, and the coverage check passes (FR-4, FR-5, AR18)

**Given** the demo seed
**When** it runs
**Then** invented patients across all six phases exist for the demo clinic, with no real names (FR-48, NFR1)

**Given** a signed-in Staff user
**When** they open Patients, which this story adds to the navigation
**Then** a list shows each patient with name, a phase chip (number and the clinic's phase name) and last activity, and the whole row is the target; status badges are added by later stories (FR-9, UX-DR6, UX-DR13)
**And** with no patients the screen says "No patients yet. Add the first patient." (UX-DR21)

**Given** the list
**When** the user types in search or picks a phase filter
**Then** results narrow by name, email or phone (phone matched on digits only, `%` and `_` treated as plain characters), and by phase, returning only patients of the user's clinic (FR-9)
**And** on a laptop pressing "/" focuses search (UX-DR26)

**Given** a patient row
**When** it is opened
**Then** the record shows an Overview with name, contact details, nationality and current phase, and the tabs Overview, Before arrival, Arrival, Care, After and Documents, the later tabs showing "Nothing here yet" (FR-9)
**And** on a laptop the list sits at 360px beside the record, and on a phone the record opens full screen (UX-DR10, UX-DR24)

### Story 2.2: Add a patient

As a coordinator,
I want to add a new patient with the few details I always have,
So that their record exists and I can start their journey.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** a `phase_events` table exists, owned by the `patients` module, with row-level security and pgTAP tests, and the SQL function `start_episode(patient, phase)` creates an episode and its first phase event in one transaction (AR14)
**And** the migration adds a first phase event for every episode that already exists, so no episode lacks history (FR-10)

**Given** the Patients list
**When** the coordinator taps Add patient
**Then** a dedicated flow opens, separate from the list, with "Step 1 of 2" (Details, then Review), its step count driven by configuration so Story 2.5 can add the consent step (FR-13, UX-DR14)

**Given** the details step
**When** the coordinator fills name, email, phone and nationality
**Then** the patient can also be given a date of birth, passport number and emergency contact name and phone, and a starting phase of Enquiry (default), Assessment or Planning (FR-13)
**And** the photo and documents are added after creation from the "Add documents now" card (Epic 7), so the form takes no file

**Given** a missing or invalid field
**When** the coordinator continues
**Then** each message is specific, for example "Enter the phone number with country code, for example +43 1 234 5678." and "Date of birth cannot be in the future.", an emergency contact name without a phone asks for the phone, the first invalid field takes focus and the input is kept (FR-13, UX-DR21)

**Given** the review step
**When** the coordinator confirms
**Then** the patient is created through the `patients` module and `start_episode`, with an idempotency key so a double tap creates one patient, and the record opens on Overview with nobody emailed and no sign-in account created (AR7, AR14, FR-13)
**And** Doctors and Admins can use the flow, a Patient cannot reach it, and it works on phone and laptop (FR-3, NFR2)

### Story 2.3: Save an onboarding draft and resume it

As a coordinator,
I want an unfinished onboarding saved and resumable,
So that an interruption does not lose what I typed.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** an `onboarding_drafts` table exists, owned by the `onboarding` module, with `clinic_id`, a version number and row-level security letting only Staff of the clinic read and write it, with pgTAP tests (AR8, AR18)

**Given** an onboarding in progress
**When** the coordinator moves between steps, taps Save draft (always visible) or tries to leave
**Then** the draft is saved automatically on each step change, explicitly on Save draft, and leaving prompts "Save as draft?" (FR-14, UX-DR14)
**And** a draft creates no patient, no account and no Invite, and holds no file (FR-14, AR15)

**Given** saved drafts
**When** the coordinator opens Patients
**Then** "Drafts (N)" lists them with the name, or "Unnamed draft", and the date saved, and opening one resumes at its step with input restored (FR-14)

**Given** two staff edit the same draft
**When** the second saves from an older version
**Then** the save is refused with `conflict` and a message, and the second user keeps their input (AR7)

**Given** a draft
**When** it is discarded, completed or untouched for 30 days
**Then** discarding asks for confirmation naming the draft; completing removes the draft in the same action, failing with `not_found` if it was discarded meanwhile; and drafts untouched for 30 days are deleted by the daily job, because they hold personal data `[ASSUMPTION: 30 days]` (FR-14, UX-DR26)

### Story 2.4: Duplicate patient check

As a coordinator,
I want to be stopped from reusing an email and warned about a matching phone or passport,
So that I do not create a second record for the same person.

**Acceptance Criteria:**

**Given** the patients table
**When** this story is applied
**Then** email is unique per clinic regardless of capitalisation, phone numbers are stored in international format and passport numbers in capitals without spaces, so matches compare like with like (FR-15)

**Given** the details step
**When** the coordinator leaves the email, phone or passport field, and again when the patient is created
**Then** the system checks the clinic's patients for a match (FR-15)

**Given** an email match
**When** it is found
**Then** creation is blocked with "A patient with this email already exists. Open their record instead." and an Open that record link, because email is the patient's sign-in identity (FR-15)

**Given** a phone or passport match
**When** it is found
**Then** a warning shows the existing patient's name and phase with "Open that record" and "Continue anyway" (FR-15)

**Given** the same email in another clinic's database
**When** the check runs
**Then** no match is shown, because the check reads only the user's own clinic, proven by pgTAP (FR-4)

### Story 2.5: Record consent during onboarding

As a coordinator,
I want to record that the patient has agreed to the clinic keeping their information, and record a withdrawal if they change their mind,
So that consent is captured at the start with the wording the clinic uses.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** a `consents` table exists, owned by the `patients` module, with `clinic_id`, the consent text version, the time, who recorded it, how it was given, and a withdrawn time, with row-level security and pgTAP tests, where a Patient reads only their own consents (FR-16, AR3, AR18)

**Given** the onboarding flow
**When** it runs
**Then** Consent becomes step 2 and the steps are Details, Consent, Review and invite ("Step 2 of 3") (FR-16, UX-DR14)

**Given** step 2
**When** it is shown
**Then** it displays the clinic's current consent text with a "Sample wording. Not legal text." badge and a tick box stating what is agreed, and the patient cannot be created until it is ticked (FR-16, AR9)
**And** if the clinic has no consent text, onboarding stops with "Consent wording is not set. Ask your Admin." (FR-16)

**Given** a patient is created
**When** the consent is saved
**Then** it stores the version that was displayed, refusing with `conflict` if the wording changed in the meantime, plus the time, who ticked it and how it was given; that version's text stays readable later (FR-16)
**And** a draft resumed at step 2 does not carry the tick over (FR-16)

**Given** a patient withdraws consent
**When** Staff record the withdrawal with its date and how it was given
**Then** the withdrawn time is set and the record shows a "Consent withdrawn" banner to Staff; what processing must then stop is decided in the legal review before real data (FR-16, BRD NFR-06)

### Story 2.6: Move an episode between phases

As a coordinator or doctor,
I want to move a patient's episode forward or back between the six phases,
So that the record always shows where the patient is in the journey.

**Acceptance Criteria:**

**Given** the SQL function `move_phase(episode, expected_current_phase, new_phase, note)`
**When** it is applied
**Then** `episodes.phase` is writable only through it and it writes the history row in the same transaction; a direct update of `episodes.phase` is refused for every role, proven by pgTAP (FR-10, AR14)

**Given** the patient's Overview
**When** Staff choose a new phase
**Then** a confirmation names the patient and the new phase, an optional note can be added, and after confirming the phase chip updates; any phase forward or back is allowed (FR-10, UX-DR26)

**Given** another user moved the same episode since the screen loaded
**When** Staff confirm
**Then** the move is refused with `conflict` and the message "This patient was just moved to Care by <name>.", and nothing changes (FR-10, AR7)

**Given** a move to the phase the episode is already in, or a move of a closed episode
**When** it is submitted
**Then** it is refused with a plain message (FR-10)

**Given** a move
**When** it completes
**Then** history shows who, when, from which phase to which and the note, in date order (FR-10)
**And** what each phase allows is stated where it matters: daily check-ins run only while in Care (Epic 6) and follow-up schedules only while in Continuity (Epic 9) (FR-10)

### Story 2.7: Start a new episode for a returning patient

As a coordinator,
I want to start a new visit for a patient who has been treated before,
So that their record carries over and nothing is re-entered.

**Acceptance Criteria:**

**Given** a patient with an earlier episode
**When** Staff choose Start new episode on Overview
**Then** the starting phase is Assessment or Planning only, with no Enquiry option (FR-11, BR-04)

**Given** a new episode is started
**When** it is created through `start_episode`
**Then** the previous open episode is closed with today's date in the same transaction, so there is never more than one open episode, and an idempotency key makes a double tap create one episode (FR-11, AR7, AR14)
**And** the patient's details and earlier documents are unchanged and not asked for again (FR-11)

**Given** the clinic's consent wording changed since the patient last agreed
**When** the new episode is started
**Then** Staff are asked to record consent to the current wording before continuing (FR-16)

**Given** a patient with several episodes
**When** Overview is shown
**Then** episodes are listed newest first, each with its own phase and history, the closed ones marked closed with their closing date, and search finds the patient once (FR-9, FR-11)

### Story 2.8: Patient time zone and time display

As a coordinator or patient,
I want times shown clearly in the right time zone with the clinic's time beside it,
So that flights and check-ins are never misread across countries.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** `patients.timezone` stores an IANA zone, and the clinic's default zone and display city label come from Clinic Settings (FR-47, AR11, BR-11)

**Given** a new patient
**When** the coordinator does not choose a zone
**Then** it defaults to the clinic's zone; the zone field pre-selects a zone only for a nationality with a single zone and asks for an explicit choice for countries with several (FR-47)

**Given** a stored instant
**When** a screen shows it to a viewer
**Then** it reads "Thu 12 Nov, 14:35 CET (Pune 19:05)" with the city label from settings when the viewer's zone differs from the clinic's, and without the brackets when it does not (FR-47, UX-DR20)
**And** instants are stored as `timestamptz` UTC (AR11, NFR4)

**Given** a local time that does not exist or occurs twice because of a daylight-saving change
**When** it is entered
**Then** a missing time moves forward to the first valid time and a repeated time takes the first occurrence, and the screen shows the resolved time before saving (FR-47)
**And** unit tests cover Europe, India, the US West Coast and both daylight-saving changes, and a `local_date` helper returns the date in a given zone (AR11)

### Story 2.9: Correct a patient's details

As a coordinator,
I want to correct a patient's details after the record is created,
So that a typo in a phone number, email or time zone does not stay on the record.

**Acceptance Criteria:**

**Given** a patient's Overview
**When** Staff choose Edit details
**Then** they can change name, email, phone, nationality, date of birth, passport number, emergency contact and time zone with the same validation as Story 2.2 and the duplicate checks of Story 2.4 (FR-13, FR-15, FR-47)

**Given** two staff edit the same patient
**When** the second saves from an older version
**Then** the save is refused with `conflict` and the second user keeps their input (AR7)

**Given** a change of time zone
**When** it is saved
**Then** times not yet passed (future check-ins and reminders) are computed in the new zone from then on, and past records are unchanged (FR-47)

**Given** a change of email before the patient has a sign-in account
**When** it is saved
**Then** the new email is used for the next invite; a change after the account exists is handled in Epic 3 (FR-13)
**And** a Patient cannot edit their own record here, proven by pgTAP (FR-5)

### Story 2.10: Remove a patient created by mistake

As a coordinator or admin,
I want to remove a patient record that was created in error,
So that duplicates and test entries do not clutter the list.

**Acceptance Criteria:**

**Given** a patient with no invite sent and no clinical, logistics or payment records
**When** a Coordinator or Admin chooses Remove patient and confirms by typing the patient's name
**Then** the record is hidden from the list, search and every policy, with `deleted_at` set and the row kept (FR-9, UX-DR26)

**Given** a patient with an invite or any clinical, logistics or payment record
**When** a Coordinator tries to remove them
**Then** removal is refused with a message saying an Admin must do it, and an Admin can remove it after a second confirmation (FR-3)

**Given** a removed patient
**When** any role queries any table
**Then** none of their rows are returned to patients, and Staff see them only through an Admin "Removed patients" list, proven by pgTAP (FR-5, AR10)

## Epic 3: Invite, patient sign-in and alerts

A patient receives an invite, opens it on a phone, signs in by link or code with no password, and sees their journey Home. Notifications work through the in-app inbox and email, and staff see the needs-attention block. Covers FR-2, FR-9 (needs-attention block), FR-12, FR-19, FR-45, FR-46. The `notifications` module owns `notifications` and `alerts`; the `access` module owns `invites`. Events are raised only by database triggers and named SQL functions, never called by a client (AR12). The service-role key is read only in `lib/privileged` (AR6). No email, to a patient or to staff, ever carries a patient name, flag reason, field value or other health content.

### Story 3.1: Notification outbox, event triggers and the staff inbox

As a staff member,
I want to see updates addressed to me in an inbox,
So that events that matter reach me inside the app.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** a `notifications` table exists, owned by the `notifications` module, with `clinic_id`, recipient auth user id, event type, subject, `dedupe_key`, payload, status, scheduled time and read state, with row-level security so a user reads and marks read only their own rows (AR12, FR-45)
**And** pgTAP tests prove a user cannot read or insert another user's notifications and Staff of Clinic X cannot read Clinic Y's (AR18)

**Given** the SQL function `app.emit_event(type, recipient, subject, dedupe_key, payload, mode)`
**When** it is applied
**Then** it is a definer function in a private schema with an empty `search_path`, its `EXECUTE` is revoked from `public`, `anon` and `authenticated`, and it is called only from database triggers and named SQL functions listed in a comment beside it, so no client can raise or forge an event, proven by a pgTAP case where a patient calling it is refused (AR12, AR17)
**And** it accepts only event types from a closed list, uniqueness is on `(dedupe_key, recipient)`, mode `insert` ignores a repeated key and mode `update_unresolved` replaces the payload of an existing unresolved item with the same key

**Given** a role-wide event
**When** it is emitted
**Then** it fans out one row per active user holding that role in the clinic, and if none is active it goes to the clinic's Admins (AR12)
**And** an event for a patient who has no sign-in account yet is skipped without failing the action that caused it (AR12)

**Given** a staff member with notifications
**When** they open More, Updates, which this story adds
**Then** the inbox lists them newest first, unread ones marked "New" in words, opening one marks it read, and an empty inbox says "No updates yet." (FR-45, UX-DR21)

**Given** the demo seed
**When** it runs
**Then** one invented notification exists for the demo Coordinator (FR-48)

### Story 3.2: Needs-attention block on Today

As a coordinator or doctor,
I want Today to list what needs my attention,
So that I act on the right thing first.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** an `alerts` table exists, owned by the `notifications` module, with `clinic_id`, event type, target role, patient, summary, created time, resolved time and who resolved it, with row-level security so only Staff of the clinic read it and a Patient never does, proven by pgTAP (AR12, AR18, FR-5)

**Given** unresolved alerts
**When** a Staff user opens Today
**Then** a "Needs attention (N)" block lists the alerts for their role, each with an icon, a plain sentence, the patient name, the time and one "Open" button, unresolved above alerts resolved in the last 7 days (FR-9, UX-DR12)
**And** Open goes to the right place on the patient record and does not resolve the alert by itself

**Given** an alert
**When** its resolving action is done (defined by the story that raises it) or Staff choose Resolve
**Then** it moves to resolved with who resolved it and when, and the count drops (FR-9)

**Given** no alerts
**When** Today loads
**Then** it says "Nothing needs attention." and the block works the same on phone and laptop (NFR2, UX-DR21)

**Given** the demo seed
**When** it runs
**Then** one invented alert exists so the block can be demonstrated before real sources arrive in later epics (FR-48)

### Story 3.3: Send email notifications promptly

As a patient or staff member,
I want important updates to reach my email quickly,
So that I do not need to keep the app open to know something happened.

**Acceptance Criteria:**

**Given** a new notification of an email-worthy type (invite, sign-in, landed, help, request decision, check-in ready)
**When** it is created
**Then** the database calls the sender route at once through `pg_net` with a signed header, and the route accepts only signed calls and refuses unsigned ones (AR12, AR6)

**Given** the sender
**When** it picks up notifications
**Then** it claims each row so overlapping runs cannot send the same email twice, re-checks at send time that the recipient is still active and uses their current email, and records the attempt (AR12, NFR7)
**And** it is the only code that reads pending notifications with the service-role key, inside `lib/privileged` (AR6)

**Given** any event type
**When** its email is built
**Then** subject and body say only that there is an update and how to open the app, with no patient name, flag reason, field value or health content, proven by a unit test over every type in the closed list (FR-46, AR12)

**Given** the prototype
**When** emails are sent
**Then** they go through the development mail setup (Mailpit locally, sandbox SMTP when hosted), the provider and domain change only by configuration, and a developer command runs the sender on demand so end-to-end tests do not wait for a schedule (FR-46, AR25)

### Story 3.4: Retry sweep by the database scheduler

As a patient or staff member,
I want a failed email to be retried,
So that a passing outage does not lose an important update.

**Acceptance Criteria:**

**Given** `pg_cron`
**When** the hourly sweep runs
**Then** it calls the sender for notifications that failed or were not yet sent, through the same signed route (AR12)

**Given** a failed send
**When** retries happen
**Then** there are three attempts in all (immediately, then at the next two hourly sweeps), each failure records its error text, and after the third the status is failed (FR-46)
**And** the in-app notification exists whatever happens to the email (FR-46)

**Given** the sweep runs twice for the same window
**When** both complete
**Then** no email is sent twice, proven by an integration test (NFR7)
**And** the scheduled function takes no client parameters and cannot be called by `authenticated`, proven by pgTAP (AR17)

### Story 3.5: Rate limits and browser hardening

As a patient or staff member,
I want sign-in and invite pages protected against repeated guessing,
So that nobody can break into an account by trying again and again.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** a rate-limit table and helper exist, with row-level security and pgTAP tests, storing counts per email and per network address in the database rather than in server memory (AR21, AR18)

**Given** the patient link-and-code request and resend endpoints
**When** a client exceeds the limit
**Then** the endpoint answers with the `rate_limited` result and says when to try again, a legitimate user under the limit is unaffected, and the per-address limit allows for a whole clinic behind one network address (AR21, AR7)
**And** each later story that adds a public endpoint (invite, upload, consultation request) applies the helper in its own criteria

**Given** any page
**When** it loads
**Then** a strict content security policy and frame, referrer and permissions headers are set, and an automated check fails if a response lacks them (AR21)
**And** the policy permits only what the app needs; the photo conversion and storage upload stories extend it and test that uploads still work

**Given** a repeated request for a link
**When** it comes within the cooldown
**Then** it is refused with the seconds left, with the same response whether or not the email exists (UX-DR21, AR16)

### Story 3.6: Send an invite to a patient

As a coordinator,
I want to send a patient an invite from their record,
So that they can open their plan on their own phone.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** an `invites` table exists, owned by the `access` module, storing a hashed token, a hashed code, the email, `clinic_id`, the patient, an expiry, a status (Sent, Accepted, Expired, Email failed, Revoked) and an accepted time, with row-level security so only Staff of the clinic create or read invites, and pgTAP tests (AR16, AR18)

**Given** a patient record
**When** Staff press Send invite on Overview, or choose "Send invite now" at the end of onboarding
**Then** the invite is created by `lib/privileged` with the clinic taken from the Staff caller's verified token, the role fixed to patient and the patient checked to belong to that clinic, and no sign-in account is created yet (AR6, AR16, FR-19)
**And** the email is built and sent at once from `lib/privileged`, and the raw token and code exist only in that email, never in the database, the notification outbox or a log (AR16)

**Given** an invite
**When** Overview shows it
**Then** it shows the status in words with the time, and Send invite is replaced by "Signed in" once accepted (FR-19)

**Given** Resend
**When** Staff press it within the rate limit
**Then** a new token and code replace the old ones, the old link stops working, and the patient's email can be corrected first through Edit details (FR-19, AR21)

**Given** an invite
**When** 7 days pass without redemption
**Then** it expires and the link shows "That link has expired. Ask your clinic for a new one." (FR-19)
**And** the onboarding success screen shows the invite status and an "Add documents now" card disabled with "Documents come next" until Epic 7 (UX-DR14)

### Story 3.7: Redeem an invite

As a patient,
I want to open my invite and get into my account without a password,
So that I can see my information without learning a new system.

**Acceptance Criteria:**

**Given** the invite email
**When** the patient opens the link on a phone
**Then** a page shows "Open your AyurSaathi account" with one button, and merely loading the page, as a mail scanner would, does not use the invite, proven by a test that loads it and then redeems (FR-2, AR16)

**Given** the patient presses the button, or types the six-digit code from the email with one-time-code autofill
**When** the invite is valid
**Then** `lib/privileged` creates the patient's sign-in account at this moment, with `app_role` patient, the clinic and the patient taken only from the invite row, marks the invite Accepted, and signs the patient in by generating and verifying a one-time sign-in token on the server in the same request (FR-2, AR6, AR16)
**And** the invite can be redeemed only once, and the email it was sent to must not already belong to a staff account, otherwise redemption is refused with a message to contact the clinic

**Given** another user is signed in on that browser
**When** the patient redeems
**Then** the app asks to sign that user out first, naming the account, so a staff session is never replaced silently (AR16)

**Given** a used, revoked or expired invite
**When** it is opened
**Then** the patient sees "That link has already been used or has expired. Ask your clinic for a new one." (FR-2, UX-DR21)

### Story 3.8: Returning patients sign in by link or code

As a patient,
I want to sign in again later with my email,
So that I can come back to my plan, including after I have gone home.

**Acceptance Criteria:**

**Given** the patient sign-in screen
**When** a patient enters their email
**Then** a link and a six-digit code are sent only if the email belongs to an active patient account, and the response is the same in every case, including for a staff email, so the screen reveals nothing and gives staff no passwordless sign-in (FR-2, AR16)
**And** the cooldown and rate limit apply (AR21)

**Given** the link or the code
**When** it is used within one hour
**Then** the patient is signed in; after an hour, or once used, it is refused and the screen offers to send a new one (FR-2) `[ASSUMPTION: one hour]`

**Given** a link from a notification email to a specific screen, such as a follow-up check-in
**When** the patient is signed out
**Then** after signing in they land on that screen, with the destination taken only from an allowlist of app paths (AR16, UX-DR21)

**Given** a signed-in patient
**When** they request any clinic route
**Then** they receive "You do not have access to this page." with a link to their home (FR-3)

### Story 3.9: Revoke patient access and change a patient's email

As a coordinator or admin,
I want to cancel an invite sent to the wrong address and end a patient's access,
So that nobody other than the patient can read their record.

**Acceptance Criteria:**

**Given** an invite that is not yet accepted
**When** Staff choose Revoke invite and confirm
**Then** its status becomes Revoked and the link and code stop working at once (FR-19, AR16)

**Given** a patient with a sign-in account
**When** a Coordinator or Admin chooses Disable patient access and confirms by naming the patient
**Then** the account is disabled through `lib/privileged`, `app.user_role()` returns no role for it at once, existing sessions stop working within the token lifetime, and a pgTAP case proves an old token is refused (AR5, AR6)
**And** access can be re-enabled the same way

**Given** a patient whose email must change after the account exists
**When** Staff save the new email through Edit details
**Then** `lib/privileged` changes the sign-in account's email, pending invites to the old address are revoked, and the patient is told at both addresses that the email changed, without health content (FR-13, AR6)

**Given** a Patient
**When** they try any of these actions
**Then** they are refused (FR-3)

### Story 3.10: Patient Home with the journey bar and updates

As a patient,
I want a Home screen that shows where I am in my journey and what is new,
So that I know what happens next without searching WhatsApp.

**Acceptance Criteria:**

**Given** a signed-in patient with an open episode
**When** Home loads
**Then** it shows a greeting and a "Step N of 6, <phase name from settings>" line with a six-segment bar, completed steps marked "Done" and the current step "Now", read by a screen reader as "Step 4 of 6, Arrival, now" (FR-12, UX-DR6, UX-DR23)

**Given** the today card
**When** Home loads
**Then** it shows, by phase of the open episode: Enquiry, Assessment or Planning: "Your clinic is preparing your visit."; Arrival: the arrival details when entered (Epic 4) or "Your travel details will appear here."; Care: today's published plan summary and whether a check-in is due (Epics 5 and 6) or "Nothing is planned for today."; Continuity: the next follow-up date (Epic 9) (FR-12)
**And** a patient with no open episode sees "Your visit is complete. Your clinic will be in touch." instead of the journey bar (FR-12)

**Given** the patient shell
**When** it renders
**Then** the bottom bar shows Home, Plan, Documents and Check-in with icons, labels and 56px targets, and Plan, Documents and Check-in show their empty states until their epics are built (UX-DR9, UX-DR21)

**Given** Updates on Home
**When** notifications exist
**Then** they list newest first with "New" in words, opening one marks it read, and a patient sees only their own (FR-45, FR-5)
**And** the footer shows the clinic phone from settings and "In an emergency, call your local emergency number." (UX-DR22)

**Given** the Settings link in the Home header
**When** the patient opens it
**Then** they can choose the theme (System, Light or Dark) and Sign out, which ends the session and clears the app-shell cache (UX-DR1, AR20)
**And** Home is one column up to 560px, 18px body text, usable at 200% zoom, and passes the automated accessibility check; an end-to-end test proves Patient A never sees Patient B's data (UX-DR2, UX-DR23, UX-DR24, FR-5)

## Epic 4: Arrival

The clinic enters pickup and stay, the patient adds flight details and sees the arrival-day card, and taps I have landed or I need help. The coordinator is alerted. Covers FR-25, FR-26, FR-27, FR-28, FR-29, FR-30. The `arrival` module owns `flights`, `pickups`, `accommodations` and `arrival_events`; Coordinators and Admins write them, Doctors read them, per the PRD role table (AR8, AR10). Patients never write these tables directly: their changes go through named SQL functions, and alerts are raised by triggers through `app.emit_event` (AR12, AR14). All arrival times are entered and shown in the arrival airport's zone, which defaults to the clinic's zone, labelled with the city. This epic completes the walking skeleton.

### Story 4.1: Flight details

As a coordinator or patient,
I want to enter the patient's flight number and arrival time,
So that everyone knows when to expect the patient.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** a `flights` table exists, owned by the `arrival` module, with `clinic_id`, the episode, flight number, arrival airport, arrival instant in UTC, `updated_by` and `updated_at`, one inbound flight per episode, with row-level security and pgTAP tests (AR3, AR4, AR8, AR18)
**And** Coordinators and Admins write, Doctors read, a Patient reads only their open episode's flight, and a Doctor's write is refused, proven by pgTAP (FR-25, FR-5, AR10)

**Given** a signed-in patient
**When** they open Arrival details from Home and add or change their flight
**Then** the change goes through `set_own_flight(flight_number, arrival_local_time)`, which takes the episode from the caller's open episode, sets `updated_by` from the caller, and is allowed only while that episode is open and not past the Arrival phase; the patient has no direct write on the table, proven by pgTAP (FR-25, AR14)

**Given** an arrival time
**When** it is entered by a patient or Staff
**Then** it is read as the local time at the arrival airport (the clinic's zone by default), stored in UTC, and shown everywhere as "Thu 12 Nov, 19:05 Pune time", with the viewer's own time in brackets when their zone differs (FR-25, AR11, UX-DR20)

**Given** invalid input
**When** the form is submitted
**Then** a flight number not in airline-code-plus-number form shows "Enter the flight number as airline code and number, for example LX 148." and a missing time shows "Enter the arrival date and time." `[ASSUMPTION: flight number format check]` (FR-25)

**Given** a patient and Staff edit the flight at nearly the same time
**When** the second save is from an older version
**Then** it is refused with `conflict` and the user sees the current value (AR7)
**And** Staff can remove a flight entered by mistake, with a confirmation naming it (UX-DR26)

### Story 4.2: Pickup details

As a coordinator,
I want to enter the car and driver who will meet the patient,
So that the patient knows who is meeting them.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** a `pickups` table exists, owned by the `arrival` module, with `clinic_id`, the episode, driver name and phone, car, plate, meeting point and pickup time, with row-level security and pgTAP tests (AR3, AR8, AR18)
**And** Coordinators and Admins write, Doctors read, a Patient reads only their open episode's pickup and cannot write (FR-26, FR-5, AR10)

**Given** the Arrival tab
**When** Staff enter and save pickup details
**Then** they show in a Pickup section visible to the patient, a missing driver phone shows "Not yet confirmed." without blocking the save, and a phone must include a country code (FR-26, UX-DR21)

**Given** a saved change
**When** at least one field actually changed
**Then** a trigger notifies the patient "Your pickup details were updated." through `app.emit_event`, with repeated saves within 10 minutes sharing one notification; a save with no change notifies no one (FR-26, AR12)

### Story 4.3: Stays and room changes

As a coordinator,
I want to record where the patient stays, including a move to another room or place during the visit,
So that the patient always knows where to go.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** an `accommodations` table exists, owned by the `arrival` module, with `clinic_id`, the episode, place, room, check-in and check-out times in the clinic's zone, with row-level security and pgTAP tests, allowing several stays per episode that do not overlap (AR3, AR8, AR18, BRD FR-CAR-06)
**And** Coordinators and Admins write, Doctors read, a Patient reads only their open episode's stays (FR-27, FR-5)

**Given** the Arrival tab
**When** Staff add a stay or record a room change
**Then** the stays list in date order, the current one is marked "Now", and a check-out before check-in or an overlap is refused with a message that says which dates clash (FR-27)

**Given** a saved change that actually changed something
**When** it is saved
**Then** the patient is notified "Your stay details were updated." through a trigger and `app.emit_event`, at most once per 10 minutes (FR-27, AR12)

### Story 4.4: Arrival-day card and arrivals on Today

As a patient,
I want one card that shows my flight, who meets me and where I am staying,
So that I have everything I need on arrival day in one place.

**Acceptance Criteria:**

**Given** a patient whose open episode is in the Arrival phase, or whose arrival day is today or tomorrow
**When** Home loads
**Then** an arrival-day card shows the flight and arrival time in the airport's local time, the driver's name and phone, the car, plate and meeting point, and the current stay (FR-28, UX-DR20)
**And** any field not yet entered shows "Not yet confirmed." and the rest still shows (FR-28, UX-DR21)

**Given** the episode moves to Care, or the day after arrival has passed
**When** Home loads
**Then** the card is no longer shown (FR-28)

**Given** the card on a phone at 200% zoom and 320px width
**When** it is viewed
**Then** no label is truncated, exact values (flight number, phone, plate) are never abbreviated, and the automated accessibility check passes (UX-DR2, UX-DR23)

**Given** Staff
**When** they open Today or the Patients list
**Then** Today lists patients arriving today with their arrival time, and the Patients list shows an "Arriving today" badge for them (FR-9, UX-DR13)

### Story 4.5: "I have landed" and "I need help"

As a patient,
I want to tell the clinic I have landed or that I need help with my pickup,
So that someone knows and can act.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** an `arrival_events` table exists, owned by the `arrival` module, with `clinic_id`, the episode, type (landed or help), time and who recorded it, with row-level security and pgTAP tests; patients create events only through `record_arrival_event(type)`, which uses the caller's open episode (AR8, AR14, AR18, FR-5)

**Given** the arrival-day card
**When** the patient taps "I have landed"
**Then** the event is saved, a trigger raises a Coordinator alert and notification through `app.emit_event`, landed is recorded once per episode, and the screen says "Thank you. Your coordinator has been told." with the clinic phone (FR-29, AR12)

**Given** the patient taps "I need help with my pickup"
**When** the event is saved
**Then** the coordinators are alerted, a new help request is raised again if the previous one was already resolved, and the screen shows the clinic phone and "For a medical emergency, call your local emergency number." and states that this button is about the pickup (FR-29, UX-DR22, BR-06)

**Given** the patient is offline or the request fails
**When** they tap either button
**Then** the screen says "Not sent. Please call the clinic on <clinic phone>." and never shows the thank-you message (FR-29, UX-DR21)

**Given** an alert
**When** it shows on Today
**Then** it reads "Landed" or "Needs help with pickup" with the patient name and time, and a Coordinator resolves it with "Mark handled" on the Arrival tab (FR-9, FR-29)

### Story 4.6: Alert when the patient adds or changes flight details

As a coordinator,
I want to be told when a patient adds or changes their flight,
So that I can arrange or re-plan the pickup in time.

**Acceptance Criteria:**

**Given** a patient adds a flight for the first time, or changes the flight number or arrival time
**When** `set_own_flight` saves it
**Then** a trigger raises a Coordinator alert naming the patient and showing the old value (or "none") and the new value, through `app.emit_event` (FR-30, AR12)

**Given** Staff edit the same flight
**When** the change is saved
**Then** no alert is raised (FR-30)

**Given** the patient changes the flight again while the alert is unresolved
**When** the change is saved
**Then** the same alert is updated (mode `update_unresolved`), keeping the value from before the first unresolved change as "old" and showing the latest as "new" (FR-30, NFR7)

**Given** the alert
**When** the coordinator opens it
**Then** it goes to the Arrival tab's Flight section, and Mark handled resolves it; a Patient cannot read alerts, proven by pgTAP (FR-9, FR-30, FR-5)

### Story 4.7: Walk the arrival journey end to end

As a product owner,
I want to walk Anna's arrival journey from invite to landed in one repeatable run,
So that the walking skeleton is proven working, not assumed.

**Acceptance Criteria:**

**Given** a clean demo database and Mailpit
**When** the end-to-end test for UJ-1 runs, with the sender run on demand
**Then** a coordinator creates a patient and sends the invite, the invite arrives in Mailpit, the patient redeems it on a phone-sized browser, Home shows the journey bar, the patient adds a flight, sees the pickup and stay the coordinator entered, taps "I have landed", and the coordinator's Today shows the alert (UJ-1; FR-1 to FR-3, FR-7, FR-9, FR-12 to FR-16, FR-19, FR-25 to FR-30, FR-45, FR-46)
**And** it also runs the failure case, where the invite page is loaded first by a mail scanner and the patient still redeems it

**Given** the run
**When** it completes
**Then** the isolation suite passes for every table, view, function and bucket added in Epics 1 to 4, the automated accessibility check passes on every patient route, and the end-to-end suite runs in Chromium, Firefox and WebKit at phone and laptop sizes (FR-4, FR-5, FR-6, BRD NFR-12, NFR8)
**And** a demo script for this journey is saved in `docs/demo/arrival.md`

**Given** the demo script
**When** Ravi follows it on a phone and a laptop
**Then** every step works as written, and any step that does not is recorded as a defect before the next epic starts (NFR2)

## Epic 5: Plan and patient day

The Doctor records findings, notes and medicines. The coordinator builds, copies and publishes the Day Plan and records treatments given. The patient sees the schedule, meals and medicines, ticks medicines taken, and reads what the Doctor shares in a "From your doctor" section. Covers FR-31, FR-32, FR-33, FR-34, FR-35. The `care` module owns `notes`, `medicines`, `medicine_intakes`, `day_plans`, `plan_items` and `treatments_given` (AR8). Multi-row changes are single SQL functions: `change_medicine`, `stop_medicine` and `publish_day_plan` (AR14). Admin reads all clinical records and a Coordinator reads Shared notes only, per the PRD role table and the owner's decision (AR10). Medicine dates are dates in the clinic's zone. The app records and alerts; it never advises (BR-06).

### Story 5.1: Doctor's findings and notes

As a doctor,
I want to record post-arrival findings and notes and choose who can see each,
So that the clinical record is complete and the patient sees only what I choose to share.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** a `notes` table exists, owned by the `care` module, with `clinic_id`, the episode, a kind (finding or note), the text, the author, the time, `visibility` of `shared` or `staff_only`, a version and an edit history, with row-level security (AR3, AR8, AR10)
**And** pgTAP tests, generated from the capability matrix, prove that only a Doctor writes, an Admin reads all notes, a Coordinator reads only `shared` notes, a Patient reads only `shared` notes of their own open episode, and nobody reads another clinic's notes (FR-31, FR-3, FR-5, FR-4)

**Given** the Care tab
**When** a Doctor adds a finding or note
**Then** the visibility toggle defaults to Staff-only and states the choice in words ("Staff-only. The patient cannot see this." or "Shared with patient"), and a Staff-only note shows the lock marker on the item itself (FR-31, UX-DR8)

**Given** a saved note
**When** the Doctor edits it or changes its visibility
**Then** the previous text and visibility are kept in its history, a change from Staff-only to Shared or back asks for confirmation naming the note, and a conflicting edit is refused with `conflict` (FR-31, AR7, UX-DR26)

**Given** a Coordinator
**When** they open the Care tab
**Then** they see only Shared notes and no add or edit control, and a direct write is refused by policy (FR-3, FR-31)

### Story 5.2: Prescribe, change and stop medicines

As a doctor,
I want to record the medicines I prescribe, change a dose and stop a medicine without losing the history,
So that the patient sees the current course and the clinic keeps the record.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** a `medicines` table exists, owned by the `care` module, with `clinic_id`, the episode, a lineage id shared by every version of the same medicine, name, dose, a structured schedule of daily slots (morning, midday, evening, night, each with an optional time), start date, duration in days, end date, prescriber, status (current, changed, stopped) and a version, with row-level security and pgTAP tests (AR3, AR8, AR18)
**And** only a Doctor writes, a Coordinator and Admin read, and a Patient reads only their own open episode's medicines (FR-32, FR-5, AR10)

**Given** the Care tab
**When** a Doctor adds a medicine
**Then** name, dose, at least one slot, start date and duration are required with specific messages, and the end date is calculated in the clinic's zone (FR-32)

**Given** a current medicine
**When** the Doctor changes its dose or schedule
**Then** `change_medicine(medicine, expected_version, new values)` ends the current row and creates the next version in one transaction, keeping the lineage id, so the earlier dose stays in history; a change on the start day replaces the row while still keeping it in history; and an older expected version is refused with `conflict` (FR-32, FR-39, AR14, AR7)

**Given** a current medicine
**When** the Doctor stops it
**Then** `stop_medicine(medicine, expected_version)` sets status stopped and the end date to today, and it leaves the current course (FR-32)

**Given** a medicine whose duration has passed
**When** the lists are shown
**Then** it leaves the current course and appears under earlier medicines (FR-32)

### Story 5.3: Build a Day Plan and the Plans screen

As a coordinator,
I want to build a day's plan of treatments and meals for a patient, with their medicines included automatically,
So that the patient will know what happens tomorrow.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** `day_plans` and `plan_items` tables exist, owned by the `care` module, with `clinic_id`, one plan per episode per date, and for each plan a published snapshot and a draft revision with a version, with row-level security and pgTAP tests (AR3, AR8, AR18)
**And** item kinds are therapy, meal, review and other; medicine lines are not typed by Staff but shown read-only from the patient's current `medicines` for that date, so a plan can never show a medicine the Doctor did not prescribe (FR-33, FR-3)
**And** a Patient can never read a draft revision and reads only the published snapshot of their own open episode (FR-5, AR10)

**Given** the Care tab
**When** Staff choose a date and add items
**Then** items group under Morning, Midday and Evening and can be edited, reordered and deleted in the draft, which shows a Draft badge with the time saved, and the current stay for that date is shown read-only (FR-33, UX-DR16, FR-27)

**Given** two staff edit the same draft
**When** the second saves from an older version
**Then** the save is refused with `conflict` and their changes are kept on screen (AR7)

**Given** the Plans screen, which this story adds to the Coordinator's navigation
**When** it opens
**Then** it lists patients in Care, and patients in Arrival who arrive by tomorrow, with tomorrow's plan status (Not started, Draft, Published), where "tomorrow" is in the clinic's zone (FR-33, UX-DR13)
**And** Today shows the number of plans for tomorrow not yet published (FR-9)

### Story 5.4: Copy yesterday, publish and unpublish

As a coordinator,
I want to copy yesterday's plan, publish tomorrow's in one step and take back a plan published by mistake,
So that a routine day takes a minute, not twenty, and mistakes can be corrected.

**Acceptance Criteria:**

**Given** a plan exists for the previous date
**When** Staff choose Copy yesterday on a new date
**Then** the previous day's therapy, meal, review and other items are copied into the draft for the chosen date, and medicine lines come from the current medicines for the new date, never from yesterday's copy (FR-33)
**And** when no plan exists for the previous date the action is disabled with "No plan for Wed 11 Nov", and copying onto a date with a plan asks for confirmation naming what will be replaced (UX-DR26)

**Given** a draft
**When** Staff choose Publish to patient and confirm the patient name and date
**Then** `publish_day_plan(plan, expected_version)` copies the draft into the published snapshot, records the time and raises the patient notification in one transaction, and the badge reads "Published at 17:42" (FR-33, AR14, UX-DR16)
**And** an empty plan cannot be published, and a date in the past asks for confirmation (FR-33)

**Given** a published plan
**When** Staff edit it
**Then** the edits go to the draft revision and the patient keeps seeing the published snapshot until it is published again, when one notification "Your plan for Thursday 12 November was updated." is sent (FR-33, AR10)

**Given** Publish is submitted twice for the same draft version
**When** the second request arrives
**Then** nothing new happens and the screen says "Already published."; a republish after real edits is not blocked (FR-33, AR7, NFR7)

**Given** a plan published by mistake
**When** Staff choose Unpublish and confirm naming the patient and date
**Then** the patient no longer sees it and is notified "Your plan for Thursday was withdrawn. Your coordinator will publish a new one." (FR-33)
**And** a Patient cannot call `publish_day_plan`, proven by pgTAP (FR-3, AR17)

### Story 5.5: Record treatments given

As a coordinator,
I want to record the treatments actually given each day,
So that the record shows what happened as well as what was planned.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** a `treatments_given` table exists, owned by the `care` module, with `clinic_id`, the episode, the date, an optional link to the planned item, treatment, therapist name, duration in minutes and notes, with row-level security making the whole table staff-only, proven by pgTAP that a Patient reads no row (AR3, AR8, AR18, FR-5)

**Given** a published Day Plan
**When** Staff open it on or after the day
**Then** each planned therapy offers "Record as given", prefilled and editable, an unplanned treatment can be added, and planned and given are shown side by side (FR-34)
**And** "Record as given" submitted twice creates one record, through an idempotency key (AR7)

**Given** a record
**When** it is saved or corrected
**Then** duration must be more than zero ("Enter how many minutes the treatment took."), and a correction keeps the earlier values in history (FR-34)

### Story 5.6: The patient's Plan tab and "From your doctor"

As a patient,
I want to see my schedule, meals and current medicines for the day, and what my doctor has shared with me,
So that I know what to expect and what my doctor told me without asking anyone.

**Acceptance Criteria:**

**Given** a published plan for the patient's open episode
**When** the patient opens Plan
**Then** the day view shows the date, the schedule grouped Morning, Midday and Evening, the meals and the current medicines by slot, at 18px, with times in the clinic's local time labelled with the city (FR-35, UX-DR2, UX-DR20)
**And** a date switcher moves between days that have a published plan

**Given** no published plan for a date
**When** the patient opens it
**Then** the screen says "Your plan for this day has not been published yet. Your coordinator will publish it." and shows nothing from a draft (FR-35, UX-DR21)

**Given** the medicines section
**When** it is shown
**Then** it lists the current course by slot, and "Show earlier medicines" reveals changed and stopped ones with their dates (FR-32, FR-35)

**Given** the "From your doctor" section below the day view
**When** the Doctor has shared notes or changed a medicine
**Then** it lists shared notes and medicine changes newest first, with the date and the doctor's name, and never a Staff-only note; Epic 8 adds shared assessment outcomes to the same section (FR-31, FR-5)
**And** a trigger notifies the patient "Your doctor shared a note with you." when a note becomes Shared, with no note text in the notification or email (FR-31, AR12)

**Given** the footer
**When** Plan is shown
**Then** it shows the clinic phone and the emergency line, nothing explains what a medicine or answer means medically, the automated accessibility check passes, and an end-to-end test proves Patient A never sees Patient B's plan or notes (UX-DR22, BR-06, FR-5)

### Story 5.7: Tick medicines as taken

As a patient,
I want to mark each dose as taken,
So that the clinic knows I followed my plan and I do not lose track.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** a `medicine_intakes` table exists, owned by the `care` module, with `clinic_id`, the medicine lineage, the local date, the slot, the time taken and the source (patient or staff), unique on lineage, date and slot, with row-level security and pgTAP tests (AR3, AR8, AR18)
**And** patients record and undo intakes only through `record_intake` and `undo_intake`, which allow only today's date in the clinic's zone, current medicines of their own open episode and, for undo, their own entry within 10 minutes (FR-35, FR-5, AR14)

**Given** the day view
**When** the patient taps "Taken" on a dose
**Then** the row reads "Taken at 08:10" in words, and a change of dose later the same day keeps today's ticks because intakes follow the lineage (FR-35, UX-DR17)

**Given** Staff view the patient's day
**When** they record a dose on the patient's behalf
**Then** it is stored with source staff, and the patient cannot undo a staff entry (FR-35)

**Given** the same dose tapped twice quickly
**When** both requests arrive
**Then** one intake exists (FR-35, NFR7)

**Given** the demo journey for UJ-2
**When** the end-to-end test runs
**Then** the coordinator copies yesterday's plan and publishes it, the patient sees it on a phone-sized browser and taps Taken, the Doctor shares a note and the patient sees it under "From your doctor", and the isolation suite passes for every object added in this epic (UJ-2, FR-6)

## Epic 6: Check-in and doctor review

The patient answers a daily check-in. The Doctor reviews check-ins flagged first, adds notes, changes medicines and marks them reviewed, and can edit the check-in questions and flag rules. Covers FR-36, FR-37, FR-38, FR-39 and the Doctor part of FR-8. `check_ins` is one table owned by `care`, created only by the scheduler and answered only through `submit_check_in`; flags live in a separate staff-only table written only by the evaluation function (AR13, AR14). The app records and alerts. It never interprets answers medically, never tells a patient they were flagged, and applies only rules the Doctor sets (BR-06).

### Story 6.1: The patient's daily check-in

As a patient,
I want to answer a short check-in about my medicines and how I feel,
So that my doctor knows how my treatment is going.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** a `check_ins` table exists, owned by the `care` module, with `clinic_id`, the episode, a template (daily or follow_up), the questions version it uses, the local date, scheduled and closing times, answers, status (open, answered, not answered, withdrawn) and review fields, with a unique key on episode, template and local date, so changing the questions never allows a second check-in for the same day (AR13)
**And** rows are created only by `create_due_check_in`, a scheduled function with no client parameters that `authenticated` cannot call (AR13, AR17)

**Given** an episode in the Care phase
**When** the hourly job runs after 06:00 in the clinic's zone, where the patient is staying
**Then** one daily check-in for that date is created, and none is created for an episode not in Care `[ASSUMPTION: window opens at 06:00 clinic time and closes at the end of that day]` (FR-36, FR-10)

**Given** an open check-in
**When** the patient opens Check-in
**Then** it runs one question per screen with "Question N of M", where M is the number of questions in its version, large answer buttons and Back at every step; answers stay on the device until sent, so reopening resumes where the patient stopped (FR-36, UX-DR18)
**And** the medicines question takes Yes, Partly or No, score questions take 1 to 5 with words at each end, free text is limited to 1,000 characters with a counter, and continuing without an answer says "Choose an answer to continue." `[ASSUMPTION: answer formats and limits]` (FR-36, UX-DR21)

**Given** the review screen
**When** the patient taps Send
**Then** `submit_check_in(check_in, answers, idempotency_key)` takes the episode from the caller, validates the answers against the check-in's own questions version, records them once and refuses a second submission or a check-in that is closed; patients have no direct insert or update on `check_ins`, proven by pgTAP (FR-36, AR7, AR14)
**And** the screen says "Received. Your doctor reviews check-ins each day." with the clinic phone and "For urgent help, call the clinic. In an emergency, call your local emergency number." (UX-DR22)

**Given** Send while offline or a failed request
**When** it happens
**Then** the answers are kept and the screen says "Not sent yet. Try again when you are connected.", and retrying with the same key cannot record it twice (UX-DR21, NFR7)

**Given** the end of the local day
**When** a check-in was never answered
**Then** it becomes "not answered" and the Review Queue shows it to the Doctor as "Not answered" (FR-37)
**And** when no check-in is open the tab says "Your next check-in opens tomorrow at 06:00 Pune time." with the time and city from settings (UX-DR21, UX-DR20)

### Story 6.2: Flag evaluation with sample rules

As a doctor,
I want check-ins marked by rules I set, not rules built into the app,
So that the clinic's judgement, not the software's, decides what needs attention.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** a staff-only table `check_in_flags` exists, owned by the `care` module, holding for each check-in whether it is flagged, the reasons in plain words and the flag-rules version used, with row-level security so a Patient reads no row, proven by pgTAP (AR10, AR13, FR-5)

**Given** a submitted check-in
**When** `submit_check_in` records it
**Then** the evaluation function runs in the same transaction against the current flag rules and writes `check_in_flags`; a rule that refers to a question the check-in does not have is skipped and noted as a reason, and an error in evaluation never blocks the patient's submission (FR-38, AR13)
**And** the function holds no clinical threshold of its own, so with an empty rule set nothing is flagged (FR-38, BR-06)

**Given** the sample rule set from the seed
**When** a check-in has medicines "No" or any score of 2 or less
**Then** it is flagged with reasons such as "Medicines: No" or "Sleep: 2 of 5", labelled "Sample rules. Not clinical advice." wherever shown to Staff `[ASSUMPTION: sample rules only for the demo; the real rules come from the Doctor]` (FR-38, UX-DR22)

**Given** a change to the rules
**When** the next check-in is submitted
**Then** it follows the new rules with no code change, and earlier check-ins keep the flags and rules version they were evaluated with (FR-38)

**Given** unit tests
**When** they run for each answer type, an empty rule set, a rule naming a missing question and a score on the boundary
**Then** every case passes (FR-38)

### Story 6.3: The Doctor's Review Queue

As a doctor,
I want a queue of check-ins with the flagged ones first,
So that I look at the patients who need me before the rest.

**Acceptance Criteria:**

**Given** answered and not-answered check-ins
**When** a Doctor opens Review, which this story adds to the Doctor's navigation
**Then** the list shows flagged check-ins first, then the rest oldest first, then "Not answered" ones, each with the patient name, the check-in type and time, a "Needs review" badge with the reasons in words, and a "Sample rule" badge when the sample rules raised it (FR-37, UX-DR19)
**And** a Doctor sees only check-ins of their own clinic, and an empty queue says "Nothing to review right now." (FR-4, UX-DR21)

**Given** a check-in is flagged on submission
**When** it is saved
**Then** a trigger raises an alert for the Doctors through `app.emit_event`, which shows on Today, the Patients list shows a "Needs review" badge for that patient, and Today shows the number of check-ins waiting for review (FR-9, FR-37, AR12, UX-DR13)

**Given** a Coordinator or Admin
**When** they open the queue
**Then** they can read it but not review it; for a Coordinator the pane shows Shared notes only, proven by an end-to-end test; a Patient cannot see the queue (FR-3, FR-5, FR-31)

**Given** a laptop at 1024px or wider
**When** the queue is shown
**Then** the list sits at 360px beside the review pane, and on a phone each row opens the pane full screen (NFR2, UX-DR10, UX-DR24)

### Story 6.4: Review a check-in

As a doctor,
I want to read a check-in, add a note, change a medicine and mark it reviewed from one screen,
So that I do not have to leave the queue to act.

**Acceptance Criteria:**

**Given** a check-in in the queue
**When** the Doctor opens it
**Then** the pane shows the answers in words, the flag reasons, the patient's recent notes and current medicines, and the actions Add note, Change medicine and Mark reviewed (FR-39, UX-DR19)

**Given** Add note or Change medicine
**When** the Doctor uses it
**Then** each saves at once through its own function (the note as in Story 5.1, defaulting to Staff-only; the medicine through `change_medicine` from Story 5.2, which refuses a change based on an out-of-date version), and the pane refreshes (FR-31, FR-32, FR-39)

**Given** Mark reviewed
**When** the Doctor confirms
**Then** `review_check_in(check_in)` locks the check-in, records who and when, and resolves the related alert in one transaction; the row leaves the queue and the count drops (FR-39, AR14)

**Given** two Doctors review the same check-in
**When** the second confirms
**Then** they see "Already reviewed by <name> at 09:12." and nothing changes; repeating Mark reviewed does nothing new (FR-39, AR7, NFR7)
**And** a Coordinator calling `review_check_in` is refused, proven by pgTAP (FR-3, AR17)

### Story 6.5: The Doctor edits check-in questions and flag rules

As a doctor,
I want to set the daily and follow-up check-in questions and the flag rules for my clinic,
So that the check-in asks what I care about and flags what I decide.

**Acceptance Criteria:**

**Given** a Doctor
**When** they open More, Settings, Clinical rules
**Then** they can edit the daily questions, the follow-up questions and the flag rules through a plain form, within limits of 1 to 10 questions per set, question text up to 200 characters and up to 20 rules, each validated `[ASSUMPTION: limits]` (FR-8, UX-DR28, AR9)
**And** the page shows "Sample rules. Not clinical advice." while the sample set is in use

**Given** the Doctor saves their own set
**When** it is stored
**Then** the badge changes to "Set by the clinic's doctor on 12 November", the new version applies to check-ins created afterwards, and an open or answered check-in keeps its own version (FR-8, FR-38, FR-36)

**Given** an invalid set or a save based on an older version
**When** the Doctor saves
**Then** an invalid set (no questions, a rule naming a missing question) is refused with what to fix, a conflicting save is refused with `conflict`, and the input is kept (FR-8, AR7, UX-DR21)

**Given** a Coordinator
**When** they open Clinical rules
**Then** they see the questions and rules read-only, with no save control, and a direct write is refused by policy (FR-8, FR-3)
**And** an Admin does not see the screen and cannot write, per the PRD role table (FR-8, AR10)

### Story 6.6: Walk the check-in and review journey

As a product owner,
I want to walk Dr. A's morning review from the patient's check-in to the reviewed note in one repeatable run,
So that the whole care loop is proven working.

**Acceptance Criteria:**

**Given** a clean demo database
**When** the end-to-end test for UJ-3 runs
**Then** the hourly job is run on demand and opens a check-in, a patient in Care answers "No" to medicines, the Doctor's Today shows the alert, the Review Queue lists it first with its reason, the Doctor adds a Shared note, changes a medicine and marks it reviewed, and the patient sees the note and the changed medicine under "From your doctor" (UJ-3, FR-36 to FR-39)
**And** the same run confirms the patient never sees a flag and a Coordinator cannot review (BR-06, FR-3)

**Given** the run
**When** it completes
**Then** the isolation suite passes for every object added in Epics 5 and 6 and the automated accessibility check passes on Plan and Check-in (FR-4, FR-5, FR-6, NFR8)
**And** a demo script is saved in `docs/demo/care.md`

**Given** the demo script
**When** Ravi follows it on a phone and a laptop, timing himself
**Then** every step works, a five-question check-in takes under a minute by hand, and any step that does not work is recorded as a defect before the next epic starts (BRD NFR-03, NFR2)

## Epic 7: Documents

Staff and patients add and view documents safely, with passport scans, medical records and the patient's photo stored privately, shared or staff-only, several files at once, and phone photos accepted. Covers FR-17 and FR-18, and the optional photo of FR-13. The `documents` module owns `documents`; documents attach only to a saved patient, never to an onboarding draft (AR8, AR15). Uploads go through the user's own session under storage policies, never the service key. Stories use the findings recorded in `docs/spikes/` by Story 1.12 for the photo conversion approach and the oldest phone tested.

### Story 7.1: Document storage and access rules

As a builder,
I want the document table and private storage set up so that a file can only be stored and read by the people allowed,
So that passport scans and medical records are protected before any screen uses them.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** a `documents` table exists, owned by the `documents` module, with `clinic_id`, the patient, an optional episode, kind (passport, medical record, letter, prescription, summary, photo or other), storage path, file type, size, who uploaded, a status (pending or stored), `visibility` of `shared` or `staff_only`, `deleted_at` and who removed it, with row-level security (AR3, AR8, AR10)
**And** a private bucket exists with a 15 MB size limit, allowed types PDF, JPG and PNG, and overwrite disallowed (AR15, FR-17)

**Given** an upload
**When** it starts
**Then** a pending `documents` row is created first through `start_upload(patient, kind, visibility)`, which fixes the id, the path `<clinic_id>/<patient_id>/<episode_id or general>/<document_id>.<ext>` and the clinic from the caller's token; the storage insert policy allows a file only at the path of a pending row the caller created (AR15)

**Given** the file has arrived
**When** `finish_upload(document)` runs on the server
**Then** the file's real content type is checked, a mismatch deletes the file and the row and returns `upload_rejected`, and a match marks the row stored (AR15)
**And** a daily job deletes pending rows and their files older than 30 minutes, so no orphan file remains

**Given** the isolation suite
**When** it runs for the table and the bucket
**Then** it proves Patient A cannot read or write Patient B's rows or files, Clinic X cannot reach Clinic Y's, a Patient cannot read a `staff_only` document, and a guessed path grants nothing (FR-4, FR-5, AR18)

### Story 7.2: Staff upload documents

As a coordinator or doctor,
I want to upload one or several documents to a patient's record and choose whether the patient can see them,
So that the patient's files are in one place and the private ones stay private.

**Acceptance Criteria:**

**Given** a saved patient's Documents tab
**When** Staff choose Add documents
**Then** a chooser shows the limits first ("PDF, JPG, PNG or HEIC, up to 15 MB each") and accepts several files at once, each with its own kind and a visibility toggle defaulting to Staff-only with the words "Staff-only. The patient cannot see this." (FR-17, BRD FR-ONB-04, UX-DR8, UX-DR15)

**Given** several files
**When** they upload
**Then** each shows its own progress and result in words, a failure of one leaves the others stored, and a file that fails can be retried on its own (FR-17, UX-DR15)

**Given** a file over 15 MB or of another type
**When** it is chosen or rejected after upload
**Then** the message is "Upload a PDF, JPG, PNG or HEIC file under 15 MB." and the other files are unaffected (FR-17, UX-DR21)

**Given** repeated uploads in a short time
**When** the rate limit from Story 3.5 is exceeded
**Then** the upload answers with `rate_limited` and says when to try again (AR21)

**Given** the Documents tab
**When** it lists files
**Then** each shows name, kind, size, who added it and a Shared or Staff-only badge with the lock marker in words on Staff-only ones, and the automated accessibility check passes (FR-18, UX-DR7, UX-DR8)

### Story 7.3: Open a document through a short-lived link

As a coordinator, doctor or patient,
I want to open a document I am allowed to see,
So that I can read it without the file being open to anyone else.

**Acceptance Criteria:**

**Given** a document the signed-in person may see
**When** they tap its name
**Then** a download link is created at that moment, works for about 60 seconds and then stops, and the file is served with `nosniff` and as an attachment (AR15)

**Given** a Patient
**When** they request a `staff_only` document, another patient's, another clinic's or a removed one
**Then** no link is created and nothing about the file is revealed (FR-5, FR-4, AR15)

**Given** a user whose access was removed
**When** they use an old token to request a link
**Then** no link is created, proven by a test (AR5, AR18)

**Given** a link older than 60 seconds
**When** it is opened
**Then** it is refused, and the user can request a new one from the same screen (AR15, UX-DR21)

### Story 7.4: Upload photos from a phone, including HEIC

As a coordinator or patient,
I want to take a photo of a passport or record with my phone and upload it,
So that I do not need a scanner.

**Acceptance Criteria:**

**Given** a phone browser
**When** the user chooses Take a photo or Choose a file
**Then** the camera or the photo library opens and the chosen images upload as in Story 7.2 (FR-17, UX-DR15)

**Given** an iPhone photo in HEIC format
**When** it is chosen
**Then** the browser converts it to JPEG before upload, showing "Preparing photo…", using the approach recorded in `docs/spikes/` by Story 1.12, and only the JPEG is stored (AR15, UX-DR15)

**Given** any photo
**When** it is prepared for upload
**Then** its location and device metadata (EXIF, including GPS) is removed in the browser before upload, proven by a test that inspects a stored file (AR15, NFR6)

**Given** a conversion that fails or takes longer than the limit in the findings note
**When** it happens
**Then** the user sees "We could not prepare this photo. Try taking it again, or choose a PDF." and nothing is uploaded (UX-DR21)

**Given** the content security policy from Story 3.5
**When** this story is applied
**Then** it is extended only as far as photo conversion and storage uploads need, and a test proves uploads and conversion still work under it (AR21)

### Story 7.5: The patient's Documents tab

As a patient,
I want to see the documents my clinic has shared with me and add my own,
So that my records are in one place and the clinic has what it needs.

**Acceptance Criteria:**

**Given** a signed-in patient
**When** they open Documents
**Then** they see Shared documents of their own record and every document they uploaded themselves, each with name, kind and date, and never a Staff-only document Staff added or another patient's (FR-18, FR-5)
**And** with none, the screen says "No documents yet. Your clinic will add documents here. You can add your own." (UX-DR21)

**Given** the patient adds documents
**When** they choose files or take photos
**Then** the upload works as in Stories 7.2 and 7.4 with 56px targets and 18px text, and Staff see the files labelled "Added by patient" (FR-17, UX-DR2)

**Given** a document the patient uploaded
**When** they remove it and confirm, the confirmation naming the file
**Then** `remove_own_document(document)` hides it from the patient only, Staff still see it marked "Removed by patient", and the patient has no direct update on `documents`, proven by pgTAP that a patient cannot change visibility, path or kind (FR-17, FR-5, AR14)
**And** a patient cannot remove a document Staff added (FR-5)

### Story 7.6: Manage documents, add them after onboarding, and the patient photo

As a coordinator,
I want to change who sees a document, remove one added by mistake, add documents right after creating a patient and set the patient's photo,
So that the record is correct and complete without extra steps.

**Acceptance Criteria:**

**Given** a document Staff added
**When** Staff change its visibility
**Then** the change is stated in words and the patient's view updates; changing from Staff-only to Shared asks for confirmation naming the file (FR-18, UX-DR8, UX-DR26)
**And** a document the patient uploaded always stays visible to that patient, whatever its visibility (FR-18)

**Given** a document added by mistake
**When** Staff remove it and confirm naming the file
**Then** it disappears from every list, its download link stops working, and the row is kept with `deleted_at` and who removed it (FR-17, UX-DR15)

**Given** the onboarding success screen
**When** a patient has just been created
**Then** the "Add documents now" card from Story 3.6 is active and opens the new patient's Documents tab ready to add a passport, medical records or a photo (UX-DR14, FR-17)

**Given** a document of kind photo
**When** Staff choose "Use as profile photo"
**Then** it shows on the patient's Overview to Staff, never shared with other patients (FR-13)
**And** a returning patient's documents from earlier episodes remain in the tab (FR-11, FR-18)

### Story 7.7: Walk the documents journey

As a product owner,
I want to walk adding a passport photo and sharing a record in one repeatable run,
So that documents are proven safe, not assumed.

**Acceptance Criteria:**

**Given** a clean demo database
**When** the end-to-end test runs
**Then** a coordinator creates a patient on a phone-sized browser, uses the success card to add a passport photo as Staff-only and two medical records at once as Shared, and the patient signs in, sees only the two Shared files, opens one, and is refused a link to the Staff-only one (UJ-2, FR-17, FR-18)
**And** the patient adds their own document, Staff see it labelled "Added by patient", and the stored photo has no location metadata

**Given** the run
**When** it completes
**Then** the isolation suite passes for the documents table and bucket, including a guessed path and a demoted user's old token, and the automated accessibility check passes on Documents (FR-4, FR-5, FR-6, AR18, NFR8)
**And** a demo script is saved in `docs/demo/documents.md`

**Given** the demo script
**When** Ravi follows it with a real iPhone photo and an Android photo
**Then** every step works, and any step that does not is recorded as a defect before the next epic starts (FR-17, NFR2)

## Epic 8: Before arrival: enquiry, assessment, planning

Staff log the enquiry and quotations, the Doctor logs the assessment, and staff record the programme and payments, so the patient's history is complete from the first contact. Covers FR-20, FR-21, FR-22, FR-23, FR-24. The `enquiry` module owns `enquiries` and `quotations`, `assessment` owns `assessments`, `planning` owns `programmes`, `programme_events` and `payments` (AR8). Per the PRD role table: Coordinators and Admins write enquiries, quotations, programmes and payments and Doctors read them; only Doctors write assessments; Admins read everything (AR10). First contact stays on WhatsApp, email and phone; the app records the outcome and lineage (BR-01). Enquiries, quotations, programmes and payments are staff-only in the prototype; only shared assessment outcomes reach the patient. Known limit: an enquiry is logged against a created patient, so a lead with no email cannot be logged until onboarded (the BRD's lead list, FR-ENQ-04, is out of scope).

### Story 8.1: Log an enquiry

As a coordinator,
I want to log an enquiry that came in on WhatsApp, email or phone,
So that the first contact is recorded against the patient.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** an `enquiries` table exists, owned by the `enquiry` module, with `clinic_id`, the episode, date, channel (WhatsApp, email, phone or other), summary, treatment interest and who handled it, with row-level security and pgTAP tests proving Coordinators and Admins write, Doctors read, a Patient reads nothing and Clinic X cannot read Clinic Y's (AR3, AR8, AR10, AR18, FR-4, FR-5)

**Given** the Before arrival tab
**When** Staff open it
**Then** an Enquiry section shows "Nothing logged yet." when empty, and Staff can add an enquiry with a required summary ("Add a short summary of the enquiry.") (FR-20, UX-DR21)
**And** a returning patient's episode that starts at Assessment or Planning is not asked for an enquiry (FR-20, BR-04)

**Given** an enquiry saved on an episode in the Enquiry phase
**When** the screen confirms
**Then** it offers "Move to Assessment", which calls `move_phase` only if Staff confirm; nothing moves otherwise `[ASSUMPTION: moves are offered, not automatic]` (FR-10, AR14)

### Story 8.2: Log quotations

As a coordinator,
I want to log each quotation I sent, with its versions and status,
So that what was offered and accepted is on the record.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** a `quotations` table exists, owned by the `enquiry` module, with `clinic_id`, the episode, a version, date sent, amount in minor units, currency, validity date and status (sent, accepted, revised or lapsed), with row-level security and pgTAP tests for the same roles as Story 8.1 (AR3, AR8, AR18)
**And** `add_quotation(episode, …)` assigns the next version inside the database under a lock, so two staff adding at once get versions 2 and 3, never an error (FR-21, AR14)

**Given** the Quotation section
**When** Staff add a quotation
**Then** an amount not greater than zero is refused with "Enter an amount greater than zero.", a validity date not after the sent date is refused with a message, and amounts are stored in minor units and displayed with the currency's decimal places through `lib/money`, tested for a two-decimal and a zero-decimal currency (FR-21)

**Given** quotation statuses
**When** they change
**Then** accepting one marks the episode's other quotations revised so only one is accepted; an accepted quotation can be un-accepted only with a confirmation that also unlinks it from any programme; and a quotation past its validity date shows as lapsed (FR-21, UX-DR26)
**And** an existing document can optionally be linked to a quotation (FR-21, FR-18)

### Story 8.3: Log an assessment

As a doctor,
I want to log how and when I assessed a patient and what I found,
So that the outcome is recorded wherever the assessment took place.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** an `assessments` table exists, owned by the `assessment` module, with `clinic_id`, the episode, date, method (in person, WhatsApp call, phone, video or email), the doctor, findings, outcome and `visibility` of `shared` or `staff_only`, with row-level security where only a Doctor writes, Admins read all, Coordinators read `shared` ones, and a Patient has no direct read on the table at all (AR3, AR8, AR10, FR-22)

**Given** the Before arrival tab
**When** a Doctor adds an assessment
**Then** date, method, findings and outcome are required, the content is free text because structured fields wait for the Doctor's input, and the visibility toggle defaults to Staff-only with the choice in words; one setting covers the whole assessment (FR-22, UX-DR8)
**And** the app does not change how the assessment is done, offering no scheduling or interpretation (FR-22, BR-06)

**Given** an assessment marked Shared
**When** the patient opens Plan
**Then** the "From your doctor" section shows its date, method and outcome, read through `my_shared_assessments()`, a definer function with a stated reason that returns only those three fields of the caller's own Shared assessments and never the findings, proven by pgTAP that a patient can never obtain the findings (FR-22, FR-5, AR17)

**Given** an assessment saved on an episode in the Assessment phase
**When** the screen confirms
**Then** it offers "Move to Planning", which calls `move_phase` only if Staff confirm (FR-10, AR14)

### Story 8.4: Record the programme and cost

As a coordinator,
I want to record the programme and approximate cost agreed before travel, and its refinement on arrival,
So that everyone knows what was settled and how it changed.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** `programmes` and `programme_events` tables exist, owned by the `planning` module, with `clinic_id`, the episode, programme name, duration in days, treatments, diet approach, approximate cost in minor units, currency, status (provisional, confirmed, refined on arrival) and an optional accepted quotation; one programme per episode; row-level security and pgTAP tests proving Coordinators and Admins write, Doctors read and a Patient reads nothing (AR3, AR8, AR10, AR18, FR-23)

**Given** the Before arrival tab
**When** Staff record a programme
**Then** a linked quotation must belong to the same episode and be accepted, otherwise the save is refused with a message; the approximate cost is labelled "Approximate" (FR-23, BR-05)

**Given** the Doctor refines the programme after the patient arrives
**When** a Coordinator records the refinement on the Doctor's behalf, naming the Doctor
**Then** `change_programme(programme, expected_version, changes, decided_by)` saves the new values and status "refined on arrival" and writes a `programme_events` row with the previous values, who entered it and which Doctor decided, in one transaction, and the change is allowed only once the episode has reached the Arrival phase (FR-23, BR-05, AR14)

**Given** a programme saved on an episode in the Planning phase
**When** the screen confirms
**Then** it offers "Move to Arrival", which calls `move_phase` only if Staff confirm (FR-10, AR14)

### Story 8.5: Record payments received

As a coordinator,
I want to record deposits, balances and refunds the clinic has received or paid back,
So that the clinic's record of money is in one place, without taking payments in the app.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** a `payments` table exists, owned by the `planning` module, with `clinic_id`, the episode, kind (deposit, balance, refund or other), amount in minor units, currency, date, method, who recorded it and a note, with row-level security and pgTAP tests proving Coordinators and Admins write, Doctors read and a Patient reads nothing (AR3, AR8, AR10, AR18, FR-5)
**And** no card number or bank detail is ever stored (FR-24)

**Given** the Before arrival tab
**When** Staff add a payment
**Then** amount (greater than zero), currency and date are required with plain messages, a refund is shown as money paid back, and an idempotency key makes a double tap create one payment (FR-24, AR7)
**And** the section shows totals per currency, and when a programme exists in the same currency, "Received 500.00 EUR of approximately 2,400.00 EUR", never mixing currencies (FR-24, FR-23)

**Given** a payment recorded in error
**When** Staff remove it and confirm naming the amount and date
**Then** it is hidden with `deleted_at` and stays in history (UX-DR26)
**And** there is no online payment, payment link or card form anywhere (FR-24)

### Story 8.6: Walk the before-arrival journey

As a product owner,
I want to walk Anna's history from first enquiry to deposit in one repeatable run,
So that the record is proven complete and private.

**Acceptance Criteria:**

**Given** a clean demo database
**When** the end-to-end test for the before-arrival part of UJ-6 runs
**Then** a coordinator logs the WhatsApp enquiry and two quotation versions, a doctor logs the assessment as Shared, the coordinator records the programme linked to the accepted quotation and a deposit, and each offered phase move is confirmed so the Overview history reads in order (UJ-6, FR-20 to FR-24, FR-10)
**And** the patient signs in and sees the assessment's date, method and outcome under "From your doctor", but never its findings or anything else from this epic (FR-5)

**Given** the run
**When** it completes
**Then** the isolation suite passes for every object added in this epic, including the `my_shared_assessments` function (FR-4, FR-5, FR-6, AR18)
**And** a demo script is saved in `docs/demo/before-arrival.md`, followed by Ravi on a phone and a laptop with any failing step recorded as a defect (NFR2)

## Epic 9: Continuity

After departure the clinic logs departure assistance and schedules follow-up check-ins, the patient answers them and can request an extra consultation, and consultations are logged. Covers FR-40, FR-41, FR-42, FR-43, FR-44. The `continuity` module owns `departure_assistance`, `follow_up_schedules`, `consultations` and `consultation_requests`; follow-up check-ins are rows in `care`'s `check_ins`, created only by `create_due_check_in` and answered through `submit_check_in` (AR8, AR13). Check-ins are initiated by the clinic's schedule, never by the patient (BR-03). In Continuity, follow-up times are in the patient's own time zone, read at the moment each one is due.

### Story 9.1: Log departure assistance

As a coordinator,
I want to log the travel help I arranged when the patient leaves,
So that the end of the visit is on the record.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** a `departure_assistance` table exists, owned by the `continuity` module, with `clinic_id`, the episode, date, what was arranged and who arranged it, with row-level security and pgTAP tests proving Staff write, a Patient reads nothing and Clinic X cannot read Clinic Y's (AR3, AR8, AR18, FR-4, FR-5)

**Given** the After tab
**When** Staff add an entry
**Then** the date and what was arranged are required, entries list newest first, and the empty section says "Nothing logged yet." (FR-40, UX-DR21)

**Given** an episode in the Care phase
**When** departure assistance is saved
**Then** the screen offers "Move to Continuity", which calls `move_phase` only if Staff confirm, and the After tab works the same on phone and laptop (FR-10, AR14, NFR2)

### Story 9.2: Schedule follow-up check-ins

As a coordinator or doctor,
I want to schedule follow-up check-ins for a patient who has gone home,
So that the clinic, not the patient, decides when to ask.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** a `follow_up_schedules` table exists, owned by the `continuity` module, with `clinic_id`, the episode, a list of dates or a repeat rule, a local time of day, status (active or cancelled) and a version, at most one active schedule per episode, with row-level security and pgTAP tests where only Staff write and a Patient reads nothing (AR3, AR8, AR18, FR-41, BR-03)

**Given** the After tab
**When** Staff create or edit a schedule
**Then** they pick future dates or "every N days for M check-ins" (N at least 1, M from 1 to 26) at a local time of day, with a preview of the dates in the patient's zone and the clinic's; past dates, zero or too many are refused with a message `[ASSUMPTION: at most 26]` (FR-41, FR-47)
**And** follow-up templates from the Doctor are not offered yet, because they wait on the Doctor's input (FR-41)

**Given** an active schedule on an episode in Continuity
**When** the hourly job runs
**Then** for each date now due it calls `create_due_check_in` with the follow-up template, computing the due time in the patient's current time zone (read from the patient record at that moment, including across daylight-saving changes), creating exactly one check-in per episode and date, and raising "Your follow-up check-in is ready." with no health content (FR-41, AR11, AR12, AR13)
**And** running the job twice creates nothing new, and the job creates nothing for an episode that is closed or not in Continuity (NFR7, FR-10)

**Given** an earlier follow-up still unanswered
**When** the next one is created
**Then** the earlier one becomes "not answered" and appears that way in the Review Queue (FR-41, FR-37)

**Given** Staff cancel a schedule
**When** they confirm naming it
**Then** no further check-ins are created and created but unanswered ones are withdrawn, while answered ones are kept (UX-DR26)

### Story 9.3: The patient answers a follow-up check-in

As a patient who has gone home,
I want to answer a short follow-up check-in about how I feel, my medicine and my diet,
So that my doctor still knows how I am doing.

**Acceptance Criteria:**

**Given** a follow-up check-in is open
**When** the patient follows the link in the notification email, signing in first if needed, or opens Check-in
**Then** they land on that check-in, which runs the same one-question-per-screen flow as the daily check-in using the clinic's follow-up questions (how they feel, medicines taken, diet issues, from Story 1.5's seed or the Doctor's edits in Story 6.5), with a review screen and Send (FR-42, UX-DR18)

**Given** the patient sends the answers
**When** `submit_check_in` records them
**Then** the screen says "Received. Your doctor reviews check-ins each day." with the clinic phone and the emergency line, the check-in enters the Review Queue, and the flag function evaluates it with the clinic's rules, never showing a flag to the patient (FR-42, FR-37, FR-38, UX-DR22, BR-06)

**Given** no follow-up is open
**When** the patient opens Check-in
**Then** they see the next scheduled date in their local time and no way to start one themselves (BR-03, UX-DR21)

**Given** a patient whose sign-in link has expired
**When** they request a new one
**Then** they can sign in as in Story 3.8, so a patient who left months ago can still answer, and Patient A cannot read or answer Patient B's follow-up, proven by pgTAP and an end-to-end test (FR-2, FR-5, AR18)

### Story 9.4: Log consultations

As a doctor or coordinator,
I want to log the WhatsApp and phone consultations given after the patient is home,
So that care that happened outside the app is still on the record.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** a `consultations` table exists, owned by the `continuity` module, with `clinic_id`, the episode, date and time, channel (WhatsApp call, WhatsApp video, phone, video or other), the doctor who gave it, a summary and an optional link to a consultation request (left empty here and used by the next story), with row-level security and pgTAP tests proving Staff write, a Patient reads nothing and Clinic X cannot read Clinic Y's (AR3, AR8, AR18, FR-4, FR-5)

**Given** the After tab
**When** a Doctor or Coordinator logs a consultation
**Then** date, channel, the doctor who gave it and a summary are required, and it appears in the episode history in date order (FR-43)

### Story 9.5: The patient requests an extra consultation

As a patient,
I want to ask my clinic for an extra consultation and see their answer,
So that I can get help without searching for the right WhatsApp chat.

**Acceptance Criteria:**

**Given** the migrations
**When** this story is applied
**Then** a `consultation_requests` table exists, owned by the `continuity` module, with `clinic_id`, the episode, requested time, preferred window with the patient's zone, reason, status (requested, approved, declined, cancelled or done), confirmed time, who handled it and the linked consultation, with row-level security and pgTAP tests (AR3, AR8, AR18)
**And** patients create requests only through `request_consultation(window, reason)`, which uses the caller's open episode and always sets status requested with no handler, and cancel only through `cancel_my_request(request)`; they have no direct insert or update, proven by pgTAP (FR-44, FR-5, AR14)

**Given** the patient's Home or Plan
**When** they tap Request a consultation
**Then** they choose a preferred day and time window, give a reason of up to 1,000 characters and send it, the request shows "Waiting for the clinic", and the screen states it is not for emergencies with the clinic phone and the emergency line (FR-44, UX-DR22, BR-06)
**And** the endpoint is rate limited (AR21)

**Given** a new request
**When** it is saved
**Then** a trigger raises a Coordinator alert keyed to that request, so every request raises its own alert, shown on Today with the patient name and time (FR-9, FR-44, AR12)

**Given** Staff open the request
**When** they approve it with a confirmed time, entered in the patient's time zone with the clinic time shown, or decline it with a short reason
**Then** the change goes through `decide_request(request, expected_status, decision)`, so a second decision on a request already decided is refused with `conflict`, the alert resolves, and the patient is notified with no health content and sees "Approved for Thursday 19 Nov, 16:00 your time" or "Declined: <reason>" (FR-44, UX-DR20, AR7)

**Given** the consultation takes place
**When** Staff log it
**Then** the request is marked done and linked to the consultation, the patient sees "Done", and a patient sees only their own requests (FR-43, FR-44, FR-5)

### Story 9.6: Walk the follow-up journey and the whole product

As a product owner,
I want to walk Anna's follow-up from the scheduled check-in to the logged consultation, and then the whole journey from enquiry to follow-up,
So that the prototype's acceptance criteria are proven end to end.

**Acceptance Criteria:**

**Given** a clean demo database
**When** the end-to-end test for UJ-4 runs, with the hourly job and sender run on demand
**Then** a coordinator schedules a follow-up, the job opens the check-in, the patient follows the email link, signs in, answers and sends, requests an extra consultation, the coordinator approves it, and after the call the consultation is logged and the request marked done (UJ-4, FR-40 to FR-44)
**And** the same run covers a patient in a different time zone across a daylight-saving change, and an expired sign-in link replaced by a new one (UJ-4, FR-2, FR-47)

**Given** the run
**When** it completes
**Then** the isolation suite passes across all nine epics with no object lacking a test, the automated accessibility check passes on every patient route, and the end-to-end suite runs in Chromium, Firefox and WebKit (FR-4, FR-5, FR-6, AR18, NFR8, BRD NFR-12)

**Given** the combined demo script in `docs/demo/full-journey.md`
**When** Ravi follows it on a phone and a laptop from enquiry to follow-up
**Then** every step works as written, any step that does not is recorded as a defect, and the prototype's acceptance is checked: the full demo journey works end to end and isolation is proven by tests (brief, SM-1, SM-2)

