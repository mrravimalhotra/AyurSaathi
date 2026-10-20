# Parked Decisions Register
## Ayurvedic Clinic Patient Journey App

Version 0.1, 2026-10-20. Owner: Ravi.

**Rule for BMAD agents:** anything in this register is undecided. Do not implement a parked item and do not guess an answer. Where a "working default" is shown, you may design so that the default works and the item can change later, and you must flag the default in the PRD. Anything the owner has not confirmed is parked.

This register has two parts:
- **Part A:** open questions and deferred decisions (`PK-nn`).
- **Part B:** every `[PROPOSED]` requirement, rule and design decision in the BRD and architecture. These are suggestions the owner has not confirmed, so they are parked until confirmed. Part B is generated from the two documents.

## Part A. Parked questions

| ID | Parked item | Options | Working default (only if a design needs one) | Blocks | Needs from | Recommended way to resolve |
|---|---|---|---|---|---|---|
| PK-01 | **Partly resolved:** first clinic is Ayurvedgram, Pune, and the product stays clinic-agnostic (BR-11, ADR-20). Sponsor: owner chose "not decided yet"; Ravi is the sole decision-maker until named. Still open:  confirmation of Ayurvedgram's real terminology and stages | Name | None | Real terminology, stages, doctor access | Ravi | One-line confirmation |
| PK-02 | **Resolved (owner):** coordinator and doctor each use either phone or laptop, so both device classes are first-class for both roles (BR-12). Still unknown: which device dominates per task, to be seen when shadowing | Phone / laptop per user | Responsive, full-function on both | Form length, bulk entry | Ravi, clinic | Shadow the coordinator for a day |
| PK-03 | **Resolved (owner):** no therapist or kitchen logins in v1; the coordinator enters on their behalf | n/a | Coordinator enters | Roles, scope | Ravi, clinic | Ask the clinic how daily plans reach therapists today |
| PK-04 | **Timing resolved (owner):** consent is captured at onboarding as step 2, versioned and timestamped. Still open: wording and legal approval (lawyer, DPDP and GDPR) before real data | Lawyer-approved text | Capture at onboarding as a second step, versioned and timestamped | Onboarding step 2, privacy, go-live | Ravi, lawyer | Lawyer reviews wording for DPDP and GDPR |
| PK-05 | **Decided (owner):** India (Mumbai preferred) for database and functions. To verify: Supabase and Vercel region availability and latency for European patients (spike S-3), and legal confirmation before real data | India | None | Setup, residency, latency | Ravi, lawyer | Decide after legal advice; check region list (spike S-3) |
| PK-06 | **Resolved (owner):** staff record payments received (deposit, balance); no online payments in v1 | n/a | Record only | Planning scope, compliance | Ravi | Keep record-only for v1 |
| PK-07 | **Resolved (owner):** English only in v1; text stays in resource files so languages can be added later | n/a | English only | Content, translation cost | Ravi | Look at the countries of recent patients |
| PK-08 | **Resolved (owner) for v1:** no WhatsApp sending; manual logging plus email and in-app prompts. Revisit after the pilot | n/a | Manual logging plus email and in-app prompts | Notifications, cost | Ravi | Revisit after the pilot with real usage and costs |
| PK-09 | What counts as a flag in check-ins | Rules set by the doctor | None. The app applies only the doctor's rules | Care review queue | Doctor | Doctor session with sample check-ins |
| PK-10 | Ayurveda-specific structured fields (for example prakriti, pulse findings, Panchakarma protocols) and which doctor defines them | Named doctor | Free text only | Assessment and Care forms | Doctor | One working session |
| PK-11 | Follow-up schedule templates the doctor uses | Weekly then monthly / fortnightly / custom | None | Departure planner | Doctor | Collect real examples from past patients |
| PK-12 | **Resolved (owner):** patient sees the current course; history on request | n/a | Current course, history on request | Patient plan tab | Ravi, doctor | Decide with the doctor |
| PK-13 | Documents as its own tab in the record | Own tab / inside each phase | Own tab | Record layout | Ravi | Confirm in mockup review |
| PK-14 | Daily check-in questions and length | Five questions / fewer / different | Five questions as in mockups | Care check-in design | Ravi, doctor | Review after the pilot |
| PK-15 | **Resolved (owner):** patient can request an extra consultation in the app; clinic approves and schedules. Request flow details PROPOSED | n/a | Request plus clinic approval | Continuity | Ravi | Decide with the doctor's workload in mind |
| PK-16 | **Resolved (owner) for v1:** return-visit nudge is off; revisit after the pilot | n/a | Off | Continuity | Ravi | Decide with the clinic |
| PK-17 | **Resolved (owner) for v1:** no attendant access; attendant details are stored on the patient record only | n/a | None | Roles, privacy | Ravi, lawyer | Decide with consent design |
| PK-18 | Data retention and erasure periods; retention of passport scans; the rule for when real patient data may be stored | Periods per data class | No real patient data until the legal gate is passed | Privacy, go-live | Ravi, lawyer | Legal advice before the pilot |
| PK-19 | Success-measure targets (BRD section 3) | Numbers per measure | None | Reporting | Ravi | Set after a baseline |
| PK-20 | **Partly resolved (owner):** build order is Foundation, then Arrival and Care. Still open: go signal, first sprint scope, team and dates | Dates and team | None. Do not build before the go signal | Everything | Ravi | Review the PRD and epics, then give the go |
| PK-21 | National health-record alignment (ABDM, Ayush Grid) and other health-record or telemedicine rules in India | Align / not in v1 | Not in v1; do not promise alignment | Roadmap, compliance | Ravi, advisor | Research and advice |
| PK-22 | Email provider and sending domain | Several providers | None | Invites, reminders | Ravi | Choose a provider with a verified domain; spike S-4 |
| PK-23 | Web push notifications, including on iPhone installed web apps | Use / not in v1 | Not in v1 | Notifications | Ravi | Spike S-1 |
| PK-24 | Availability, maintenance window, backup RPO and RTO | Numbers | None | Operations | Ravi | Agree with the clinic |
| PK-25 | Error tracking and monitoring tools | Several | None | Operations | Ravi | Pick when the first environment exists |
| PK-26 | **Resolved (owner):** patients sign in with a one-time link or code sent to their email; no password. Still to verify: delivery reliability (spike S-4) | n/a | One-time link or code to email | Authentication | Ravi | Test with older, non-technical users |
| PK-27 | Upload scanning for malware; accepted file types, size limit, HEIC support | Scan / no scan; limits | PDF, JPG, PNG up to 15 MB, no scanning | Documents | Ravi | Spike S-5 and legal view |
| PK-28 | Field-level protection of passport number and similar | Extra column encryption / rely on at-rest encryption and RLS | At-rest encryption and RLS only | Data model | Ravi, advisor | Security review |
| PK-29 | Scheduler mechanism for prompts and reminders | Vercel cron / database scheduler | Either, behind one interface | Notifications | Ravi | Spike S-2 |
| PK-30 | Whether to update the World Ayurveda Congress presentation wording about the app once decisions land | Yes / no | Keep "Proposed" wording until something is in use | Presentation accuracy | Ravi | Confirm before presenting |

### Mapping to the earlier pending-decision numbers (file `05_design_decisions_and_pending.md`)
PD1→PK-01, PD2→PK-02, PD3→PK-03, PD4→PK-04, PD5→PK-05, PD6→PK-06, PD7→PK-07, PD8→PK-08, PD9→PK-09, PD10→PK-10, PD11→PK-11, PD12→PK-12, PD13→PK-13, PD14→PK-14, PD15→PK-15, PD16→PK-16, PD17→PK-17, PD18→PK-18, PD19→PK-20, PD20→PK-30. PK-19 and PK-21 to PK-29 are new.

## Part B. Unconfirmed proposals (parked until the owner confirms)
Generated from `brd.md` and `architecture.md`. Rows marked *partly* are decided in part and proposed in part (for example the requirement is decided but its field list is proposed).
| ID | Item | Partly decided | Source |
|---|---|---|---|
| FR-ACC-02 | Roles: patient, clinic staff (front desk/coordinator), doctor, admin | partly | BRD |
| FR-ACC-05 | A patient can see only their own record; staff see by role | yes | BRD |
| FR-ACC-06 | Audit log of every view and change of patient data (who, what, when, record) | yes | BRD |
| FR-ACC-08 | Clinic home screen: patient list with phase tag, filter by phase, search, and a "needs attention" block | yes | BRD |
| FR-ACC-09 | Patient home screen: six-step journey bar plus a card for what matters today | yes | BRD |
| FR-ACC-10 | Document store for passport scans, medical records, letters, summaries, with per-document visibility | yes | BRD |
| FR-ACC-11 | In-app inbox and email notifications | yes | BRD |
| FR-ACC-12 | In-app message thread between patient and clinic | yes | BRD |
| FR-ACC-13 | Patient rights tools: export, correct, erase on request | yes | BRD |
| FR-ACC-14 | English-language interface for v1; further languages | yes | BRD |
| FR-ACC-15 | Multi-factor authentication for staff | yes | BRD |
| FR-ACC-16 | Staff can move a patient episode forward or back between phases; each change logged | yes | BRD |
| FR-ACC-17 | Episode model: one permanent patient, many episodes (one per visit) | yes | BRD |
| FR-ONB-05 | Additional optional fields: preferred language, time zone, dietary preferences, attendant details | yes | BRD |
| FR-ONB-06 | Save a draft and resume later | yes | BRD |
| FR-ONB-07 | Send the patient an invite link (email); patient sets access without installing anything first | yes | BRD |
| FR-ONB-09 | Warn on possible duplicates (same email, phone or passport number) | yes | BRD |
| FR-ONB-10 | Link earlier enquiry notes or quotation already sent over WhatsApp or email | yes | BRD |
| FR-ENQ-01 | Log an enquiry after the fact: date, channel (WhatsApp, email, phone, other), summary, treatment interest, handled by, attachments | partly | BRD |
| FR-ENQ-02 | Log each quotation: version, date sent, amount and currency, inclusions and exclusions, validity, status, file | partly | BRD |
| FR-ENQ-03 | Record enquiry source (referral, website, event, repeat) | yes | BRD |
| FR-ENQ-04 | List of enquiries not yet onboarded, for follow-up | yes | BRD |
| FR-ENQ-05 | After onboarding the patient can see their enquiry history and quotations, read only | yes | BRD |
| FR-ASM-01 | Log an assessment: date, method (in person, WhatsApp call, phone, video, email), doctor, findings, outcome, attachments | partly | BRD |
| FR-ASM-04 | Log medicines prescribed at assessment with start date and duration, to feed check-ins | yes | BRD |
| FR-ASM-05 | Patient sees a summary of the outcome and advice; notes can be marked private to the clinic | yes | BRD |
| FR-PLN-02 | Plan status: provisional, confirmed, refined on arrival | yes | BRD |
| FR-PLN-03 | Pre-arrival checklist with owner (patient or clinic), status and due date | yes | BRD |
| FR-PLN-04 | Visa tracker per traveller: type (AY-1 patient, AY-2 attendants, up to two), supporting letter, application status, expiry | yes | BRD |
| FR-PLN-05 | Pre-arrival information pack in the app (what to bring, weather, diet, transfers) | yes | BRD |
| FR-PLN-06 | Pre-arrival questions kept in one thread | yes | BRD |
| FR-ARR-02 | Pickup: car and driver details entered by the clinic, visible to the patient | partly | BRD |
| FR-ARR-04 | Arrival-day card on the patient home screen: flight, who meets you, where to stay | yes | BRD |
| FR-ARR-05 | "I have landed" and "I need help" buttons that alert the coordinator | yes | BRD |
| FR-ARR-06 | Notify the coordinator when the patient edits flight details | yes | BRD |
| FR-ARR-07 | Second transfer leg (airport to city) as a further pickup item | yes | BRD |
| FR-CAR-08 | Daily check-in: whether medicines are taken, and how the treatment is going | partly | BRD |
| FR-CAR-09 | Doctor review queue: today's check-ins, flagged first; notes and medicine change from the same screen | yes | BRD |
| FR-CAR-11 | Doctor notes marked shared with patient or private to clinic | yes | BRD |
| FR-CAR-12 | Build tomorrow's plan once, with "copy from yesterday" and doctor-set templates for diet and medicines, then publish to the patient | yes | BRD |
| FR-CAR-13 | Therapy record per session (therapy, therapist, duration, notes) | yes | BRD |
| FR-CON-06 | Follow-up schedule builder using doctor-set templates | yes | BRD |
| FR-CON-07 | Medicine supply tracker: when a supply runs out so the clinic can reorder | yes | BRD |
| FR-CON-08 | Return-visit nudge to the coordinator after a set period | yes | BRD |
| FR-CON-09 | End-of-programme feedback form | yes | BRD |
| FR-CON-10 | Departure documents handover (prescription, diet guidance, treatment summary) | yes | BRD |
| FR-CON-12 | Trend view of check-in scores for the doctor | yes | BRD |
| BR-02 | Clinic enters, patient reads. Patient-editable items: flight details, check-ins, document uploads | partly | BRD |
| BR-06 | The app records and alerts. It never gives medical advice or interprets answers medically; the doctor defines flags | yes | BRD |
| BR-07 | Every view and change of patient data is logged | yes | BRD |
| BR-08 | Mockups, prototypes and test environments use invented patient data only | yes | BRD |
| BR-09 | Real patient data may enter the system only after legal review of consent, GDPR and DPDP | yes | BRD |
| BR-10 | A patient's name or story is shown publicly (for example in a presentation) only with that patient's consent | yes | BRD |
| ADR-01 | Single deployable application (modular monolith). Clinic and patient areas live in one Next.js project, separated by route groups and role checks | partly | Architecture |
| ADR-02 | Next.js App Router with TypeScript | partly | Architecture |
| ADR-04 | Authorisation is enforced in the database with row-level security (RLS); the UI hides things but never is the only guard | yes | Architecture |
| ADR-05 | The app talks to the database with the signed-in user's token so RLS applies. The service-role key exists only in server-side jobs and admin tools,... | yes | Architecture |
| ADR-06 | Staff sign in with email and password plus MFA (authenticator app). Patients sign in with a one-time link or code sent to their email, so they need... | yes | Architecture |
| ADR-07 | Files live in private Supabase Storage buckets and are served through short-lived signed URLs; access rules mirror table rules | yes | Architecture |
| ADR-08 | Audit: database triggers log changes; the server logs views of patient records. The audit log cannot be edited or deleted by any application role | yes | Architecture |
| ADR-09 | Installable PWA: web manifest and a minimal service worker. Offline support limited to the app shell; no patient health data is cached offline | partly | Architecture |
| ADR-10 | Scheduled work (check-in prompts, reminders, nudges) is driven by one scheduler that calls idempotent, secured endpoints or functions | yes | Architecture |
| ADR-11 | Notifications are stored in a table first (in-app inbox), then delivered by channel (in-app, email). Other channels plug in later | yes | Architecture |
| ADR-12 | All timestamps stored in UTC; each patient has a time zone; prompts and flight times display in the patient's local time | yes | Architecture |
| ADR-13 | UI text lives in resource files from day one (English only first) | yes | Architecture |
| ADR-14 | Environments: local, preview (per pull request), staging, production. Database changes only through versioned migration files | yes | Architecture |
| ADR-15 | No personal health data in application logs, error reports or analytics | yes | Architecture |

Also unconfirmed: all non-functional targets (NFR-01 to NFR-15), the candidate epics (E-1 to E-12), the release plan, the success measures (BO-1 to BO-7), the validation rules in architecture section 8.4, the data model in architecture section 6, and the build approach in architecture section 10.
