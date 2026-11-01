---
status: draft
stepsCompleted: ['step-01-validate-prerequisites']
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


<!-- Repeat for each epic in epics_list (N = 1, 2, 3...) -->

## Epic {{N}}: {{epic_title_N}}

{{epic_goal_N}}

<!-- Repeat for each story (M = 1, 2, 3...) within epic N -->

### Story {{N}}.{{M}}: {{story_title_N_M}}

As a {{user_type}},
I want {{capability}},
So that {{value_benefit}}.

**Acceptance Criteria:**

<!-- for each AC on this story -->

**Given** {{precondition}}
**When** {{action}}
**Then** {{expected_outcome}}
**And** {{additional_criteria}}

<!-- End story repeat -->
