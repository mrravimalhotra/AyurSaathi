# Rubric Review: ARCHITECTURE-SPINE.md (AyurSaathi)

Reviewer: independent. Spine not edited. Checked against the good-spine checklist and PRD FR-1..FR-48.

## Verdict

Strong, mostly enforceable spine with a coherent tenancy decision, but it is not yet safe to hand down: the data model omits several PRD entities, the service-key rule contradicts the invite/user-creation path, the notification sender and idempotency mechanisms are unowned, and the operational/environmental envelope is almost wholly silent.

## Findings

### F1 (High) Data model: PRD entities with no home
Location: Structural Seed ER diagram; Capability to Architecture Map.
Missing or unplaced:
- Medicine tick, with time and source (FR-35). No table.
- Treatments given, which differ from planned and keep both (FR-34). No table. `plan_items` is the plan only.
- Departure assistance (FR-40). No table.
- Invite, with single-use link and code (FR-19, FR-2). No entity and no mechanism (Supabase OTP versus own token). UJ-1's mail-scanner edge case depends on this choice.
- Alerts (FR-9, 29, 30, 44). "I have landed", "I need help" and flight-edit are events with no table, and it is not stated whether Alerts are derived or stored.
- Follow-up Check-in schedule (FR-41), as distinct from the Check-in instance. Flags and review state (FR-37, 39: flag reason, reviewed_by/at) are also unplaced. Check-in answers are not modelled, and the question definitions live in settings.
- Onboarding draft (FR-14), and how a draft that has no auth account sits in `patients`.
- Clinic time zone default (FR-47). No home.
- Notification recipient: the ER has `PROFILE ||--o{ NOTIFICATION`, and `PROFILE` is staff (`CLINIC employs PROFILE`). Patients also receive notifications (FR-45, 33), so the model is internally inconsistent.
- `check_ins` is mapped to both `care` and `continuity`. AD-6 says a module writes only its own tables, so ownership is ambiguous.

Fix: add the missing tables to the ER and the map. Name one owner module per table. Decide the Invite/OTP mechanism and whether Alerts are a view over events or a table.

### F2 (High) AD-4 contradicts creating accounts; sender and cron runtime unowned
Location: AD-4, AD-10, AD-3, Deferred.
- AD-4 confines the service-role key to "server-only scheduled jobs and admin scripts". Sending an Invite or creating the Patient's sign-in account on submit (FR-14, FR-19), and Admin managing users (FR-8 area), need the Auth admin API at request time. The rule is either violated or the path is undecided. The PRD NFR says the service key is "used only in server-side jobs".
- AD-10 says `pg_cron` calls database functions, then "a sender delivers". Postgres cannot send SMTP. Which runtime runs the sender (Vercel cron, Edge Function, pg_net), and with what key, is not fixed, and it is exactly where units will diverge. It also resolves PRD OQ6 without saying so.
- Retry with "increasing delay" (FR-46) has no owner.

Fix: add an AD naming one privileged-operations module/route, with its key scope, for user creation and invites. Name the sender runtime and how it is triggered, and the retry schedule.

### F3 (Medium) Several Rules are not enforceable as written
- AD-6: nothing enforces "reads and writes only its own tables". It needs an import-boundary lint (for example eslint boundaries) and a CI check. The Rule also contradicts itself: "only `patients` is imported by all", yet `notifications` is written from every module, `planning` day plans embed medicines and accommodation (FR-33), and the Review screen (FR-39) spans notes, medicines and check-ins.
- AD-5: idempotency keys are required but there is no storage or scope (table, TTL, unique key). The PRD gives natural keys (a Check-in per day, a Day Plan per date), and the Rule should say to use those.
- AD-1: "at least one policy" does not prevent a permissive `using (true)`. Only AD-12 catches it. Add a lint for `true` policies or `to public` grants.
- AD-8: the two-value column covers Patient reads only. The PRD role matrix needs Coordinator to read Shared notes but never Staff-only, and Admin to read notes. Per-role capability policies (the table in PRD 4.1) are not a decision anywhere, and AD-3 only puts `role` in the token.
- AD-14: the reference-ID error reporting needs a sink, but error tracking is deferred. No mechanism is named.
- FR-7 (no health data cached offline): no AD forbids the Serwist worker from caching authenticated responses. "Offline beyond the app shell" under Deferred is not enough. Add a rule.
- AD-11: the 15 MB / MIME limit is client-side only as written. Add bucket-level size and MIME limits to the Rule.

### F4 (Medium) Operational and environmental envelope is silent
- Environments are not defined: dev, preview, hosted demo, per-clinic prod. The AD-2 "selected by environment variables" mechanism has no secrets management, no domain per clinic, and no CI/CD (the "release routine" in AD-13 is not defined or located).
- The hosted demo holds seeded Clinic Y (FR-48, AD-12) in a project that AD-2 says is one clinic. State that the demo project is a test exception, or that the seed is never loaded in a clinic's production project.
- Provider strategy is thin. Vercel and Supabase are adopted with no portability stance. The SMTP provider is deferred without a fixed sender interface, so the notification units may couple to a transport.
- Operations: backup and restore, monitoring, and availability are deferred as a block with no owner or trigger. The gate before real data in the PRD (hosting region confirmed) is not mapped to any AD.
- Performance and scale targets are not stated even as "none for the prototype".

Fix: add an Environments and Operations section with decisions, explicit deferrals tied to the pre-real-data gate, and open questions.

### F5 (Low) Tenancy applied mostly consistently, with gaps
Consistent: AD-2, AD-3 (`clinic_id` in token), AD-11 (path prefix), AD-12 (two clinics in one database), AD-13 (manifest).
Gaps:
- The `clinics` table itself has no `clinic_id`. State its policy key (`id`).
- Tables that inherit through a parent (`plan_items`, `notifications`) need `clinic_id` stated explicitly. AD-2 covers it only by "every clinic-owned table".
- The ER shows no `clinic_id` columns at all, so a reader cannot confirm tenancy per entity.

### Stack check
Every named version matches the current npm registry as of 2026-10-31 (checked: next 16.4.3, react 19.3.1, typescript 7.0.2, supabase-js 2.118.0, ssr 0.12.7, supabase CLI 2.122.0, zod 4.6.7, tailwindcss 4.3.3, vitest 5.0.5, playwright 1.64.1, @serwist/next 9.5.13). TypeScript and Tailwind are correctly flagged as assumptions. Node 22 is in maintenance by now, so 24 LTS may be the better pin. The Mumbai region is correctly marked unverified.

### Spec coverage
- Covered by capability map: all of FR-1..FR-48 at module level.
- Weak: FR-34, 35, 40 (no table); FR-19 and FR-14 (mechanism); FR-7 (no rule); FR-29, 30, 9 (alerts).
- Sound: the Deferred list does not undermine tenancy or the access model. The email provider and error-tracking deferrals can cause divergence unless an interface is fixed first (see F2, F4).
- Open Questions are reasonable, but PRD OQ6 (scheduler) and OQ5 (HEIC) are silently decided in AD-10 and AD-11 and should be noted as resolved.
