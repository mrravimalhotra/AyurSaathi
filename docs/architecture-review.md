# Architecture Review
## AyurSaathi: architect pass on `architecture.md` v0.1

Date 2026-10-20. Reviewer: architect step of BMAD. Nothing is built. Items I could not verify are marked **Unverified**. Recommendations are proposals for the owner, not decisions.

## 1. Summary
The proposed design holds up and fits the decided stack. Changes needed: two missing tables for decided features, a safer way to deliver patient sign-in links, and a recommendation on the scheduler. Everything else stands as proposed. The owner has decided India hosting and clinic-agnostic design since v0.1; both are reflected below.

## 2. Gaps fixed in `architecture.md`
| Gap | Fix applied |
|---|---|
| FR-PLN-07 (payments received, decided) had no table | Added `payments` (episode, kind deposit/balance/other, amount_minor, currency, received_on, method, recorded_by, note). Record only, no card data |
| FR-CON-11 (patient requests an extra consultation, decided) had no table | Added `consultation_requests` (episode, requested_at, preferred_window, reason, status requested/approved/declined/done, handled_by, consultation_id) |
| Patient access to payments and requests missing from the authorisation matrix | Patient reads own payments; creates and reads own requests; staff and doctor read and write |

## 3. ADR review
| ADR | Verdict | Notes |
|---|---|---|
| 01 Single app | Keep | Route groups plus middleware. Clinic isolation added by ADR-20 |
| 02 Next.js App Router, TypeScript | Keep | |
| 03 Supabase Postgres | Keep (decided) | |
| 04 RLS | Keep, mandatory | Every policy checks clinic first, then role (ADR-20). Cross-clinic and cross-patient tests per table |
| 05 User token, service key server-only | Keep | Cron and admin tools are the only service-key users |
| 06 Staff password + MFA; patient link or code | Keep, with change | Patient method is decided. Add a typed-code fallback beside the link, because email security scanners can open and use a single-use link before the patient does. Show "enter your code" on the same screen |
| 07 Private storage, signed URLs | Keep | Direct signed uploads from the phone |
| 08 Audit | Keep | Triggers for changes; server-side logging for views. Index on `(patient_id, at)` |
| 09 PWA, shell-only offline | Keep | No health data cached |
| 10 One scheduler, idempotent | Keep | See section 4, S-2 |
| 11 Notification outbox | Keep | Channels in v1: in-app, email |
| 12 UTC plus patient time zone | Keep | |
| 13 Text in resource files | Keep | English only (decided) |
| 14 Environments, migrations | Keep | Local, preview, staging, production |
| 15 No health data in logs | Keep | |
| 16 Region | Decided: India. Check S-3 | |
| 17 Upload scanning | Open (PK-27) | Types and size decided; scanning not |
| 18 Field-level protection | Open (PK-28) | Default stays at-rest encryption and RLS |
| 19 Retention jobs | Open (PK-18) | Soft delete columns exist |
| 20 Clinic-agnostic multi-tenant | Keep (decided) | See section 5 for the one open design edge |

## 4. Spikes: status
| Spike | Status | Finding |
|---|---|---|
| S-1 Web push on iPhone | Not needed | Web push is not in v1 (PK-23) |
| S-2 Scheduler | Recommendation | Prefer the database scheduler (pg_cron calling a secured function) over Vercel cron, because check-in prompts must fire at patient-local times and need at-least-hourly runs. **Unverified:** Vercel cron frequency limits on the owner's plan. Keep both behind one interface (ADR-10) |
| S-3 India region | Partly verified | Supabase documents Mumbai (`ap-south-1`) as a supported Edge Functions region and project regions are selectable per project. **Unverified:** that Mumbai is offered for new database projects on the owner's plan, Vercel function region, and latency to Europe. Check with the Management API `available-regions` call when the account exists. A region cannot be changed later without migrating to a new project, so settle it before the first real project |
| S-4 One-time link or code, Resend | Partly verified | Supabase Auth supports email magic link and email OTP, both rate limited (default 60-second resend window) and expiring; docs recommend custom SMTP for production, and the custom-SMTP default is limited to 30 new users per hour. Resend would be configured as that SMTP. **Unverified:** actual delivery and the exact expiry on the owner's project |
| S-5 Phone uploads, HEIC | Open | iPhones can produce HEIC. Options: convert to JPEG in the browser before upload, or convert server-side after upload. Decide after a real-phone test |
| S-6 RLS performance and tests | Open | Plan: a test harness that runs every policy as patient A, patient B, staff of clinic X, staff of clinic Y. Needed before the first sprint ends |
| S-7 DPAs per vendor | Open | Vercel, Supabase, Resend. Lawyer's list. Also confirm the legal basis for processing EU patients' data in India (GDPR Art. 49 is noted in the BRD; not legal advice) |

## 5. Risks and open design edges
1. **One login, one clinic in v1.** `profiles.clinic_id` ties a login to one clinic. A person who is a patient at two clinics would need two logins. Acceptable for v1; revisit before the second clinic.
2. **Email uniqueness** is proposed as unique lower(email) on profiles. With several clinics this should be unique per clinic and email. Change when the first migration is written.
3. **Email deliverability** is the main dependency of patient sign-in. Verified domain, SPF/DKIM, staff can resend, typed-code fallback.
4. **Staff on phones.** Both roles use phones (BR-12), so staff sessions need shorter timeouts and MFA that works on the same phone. Authenticator app on the same device is acceptable; note it as a risk for the security review.
5. **Doctor-defined content** (flag rules, structured fields, follow-up templates) is stored as configuration per clinic, empty until the doctor provides it. No default medical rules will be shipped.
6. **Region lock-in.** See S-3.

## 6. Recommended next actions
1. Owner confirms the candidate requirements the walking skeleton needs: FR-ACC-05, 06, 15, 16, 17, FR-ONB-07.
2. Create the cloud accounts when the go signal is given (Supabase India region, Vercel, Resend with a verified domain) and complete S-3 and S-4 first.
3. Run S-6 as part of the first sprint, not later.
