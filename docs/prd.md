# Product Requirements Document (PRD)
## AyurSaathi: Ayurvedic Clinic Patient Journey App

| Field | Value |
|---|---|
| Version | 0.1 (draft for owner review) |
| Date | 2026-10-20 |
| Owner | Ravi (product owner and sole decision-maker; sponsor not yet named, PK-01) |
| Inputs | `project-brief.md`, `brd.md`, `architecture.md`, `parked-decisions.md` |
| Status | Planning only. No code until the go signal (PK-20) |

### How to read this PRD
- **Sections 4 to 6 are the requirements.** Everything in the main body is `[DECIDED]` by the owner.
- **Section 7 is "Candidate requirements, unconfirmed".** These are `[PROPOSED]` by Claude. They are not committed to any sprint until the owner confirms.
- **Section 9 lists open questions** (`PK-nn`) with the working default. Do not build a parked item and do not guess.
- IDs refer to the BRD (`FR-xxx-nn`, `BR-nn`, `NFR-nn`) and the register (`PK-nn`).
- The app records and alerts. It never gives medical advice or interprets answers medically (BR-06).

---

## 1. Goals and background

A single Ayurvedic clinic in India treats international patients whose whole journey runs over WhatsApp, email and phone. Records, travel plans and medical history are scattered, staff juggle three channels, and patients can lose vital information.

**Product:** one installable web app (PWA) with a clinic area for staff and doctors and a patient area, both on one permanent patient record that lasts across visits. The app does not replace first contact channels or the way assessments are done. It logs the outcome and lineage, and runs the structured parts of the journey: travel logistics, daily care plan, check-ins and follow-up.

**First clinic:** Ayurvedgram, Pune. **The product is clinic-agnostic** (BR-11): nothing specific to Ayurvedgram is hard-coded, and every clinic-owned record carries a clinic key (CN-6, ADR-20). Only one clinic is live in v1.

**Goals (`[PROPOSED]`, targets parked, PK-19):** one source of truth per patient; less staff time finding information; fewer lost or repeated WhatsApp messages; engagement during care and after departure; lineage from first enquiry; repeat visits; privacy compliance.

## 2. Users

| User | Needs | Device |
|---|---|---|
| Coordinator (front desk) | Fast, short data entry; flight, pickup, stay; daily plan | Phone or laptop |
| Doctor | Assessment records, prescribed medicines, daily check-in review, notes | Phone or laptop |
| Admin | Users, settings, patient-rights requests | Phone or laptop |
| Patient (often older, non-technical) | One clear view of the plan; easy check-ins; no password | Phone first |

Not in v1: therapist and kitchen logins (the coordinator enters for them, PK-03) and attendant access (PK-17).

## 3. Journey and scope

Enquiry → Assessment → Planning → Arrival → Care → Continuity → return visit (Assessment or Planning). Returning patients skip Enquiry (BR-04).

A patient has one permanent record and many episodes, one per visit. Staff move an episode between phases and each move is logged (episode model and phase moves are `[PROPOSED]`, see section 7).

**Build order (decided):** Foundation, then Arrival and Care, then the remaining phases. The first working slice is a walking skeleton: sign-in, onboard a patient, patient opens the invite, clinic enters flight and pickup, patient sees the arrival card. Pull-through of onboarding into this slice is required because Arrival needs a patient to exist.

**Out of scope for v1:** native apps; running or onboarding other clinics (design stays tenant-ready); online payments; WhatsApp sending; web push; attendant, therapist and kitchen logins; return-visit nudges; ABDM or Ayush Grid integration; automated clinical advice.

## 4. Platform and cross-cutting requirements (decided)

| ID | Requirement |
|---|---|
| FR-ACC-01 | One application with role-based logins for clinic staff and patients, sharing one backend and patient record. |
| FR-ACC-02 | Clinic roles and a patient role. The exact staff split (coordinator, doctor, admin) is carried as a candidate (section 7). |
| FR-ACC-07 | Installable web app: appears on the home screen of patient and clinic phones. |
| BR-01 | First contact, quotations and assessment calls stay on WhatsApp, email and phone; the app records the outcome and lineage. |
| BR-03 | Follow-up check-ins are initiated by the clinic's schedule, not by the patient. |
| BR-04 | Returning patients skip Enquiry. |
| BR-05 | Programme and approximate cost are settled before travel; the doctor may refine on arrival. |
| BR-11 | Clinic-agnostic. Clinic name, branding, terminology, phase labels, templates and locale defaults are configuration. |
| BR-12 | Coordinator and doctor can do every task on either phone or laptop, with the same data on both. No device-specific features. |
| CN-1 to CN-6 | Web first; Next.js, Vercel, Supabase; cloud-driven development; Claude Code with BMAD; no build before the go signal; multi-tenant ready. |

**Decided technical choices:** patients sign in with a one-time link or code sent to their email, no password (PK-26); database and functions hosted in India, Mumbai preferred, subject to the region check and legal confirmation (PK-05, ADR-16); English-only interface with text kept in resource files (PK-07); email through Resend (PK-22; sending domain still open); no web push, email and in-app notifications only (PK-23).

## 5. Functional requirements by phase (decided)

Field lists marked "proposed" are in section 7. The core requirement is decided; the exact fields are not.

### 5.1 Onboarding
| ID | Requirement |
|---|---|
| FR-ONB-01 | A dedicated screen or flow to onboard a new patient, separate from the patient list. |
| FR-ONB-02 | Required fields: name, email, phone, nationality. |
| FR-ONB-03 | Optional but captured: photo, date of birth, passport number, emergency contact. |
| FR-ONB-04 | Optional uploads: passport scan, previous medical records (several files). Accepted types PDF, JPG, PNG and HEIC, up to 15 MB each (PK-27; malware scanning still open). |
| FR-ONB-08 | Consent is captured during onboarding as step 2, versioned and timestamped. The wording needs lawyer approval before any real patient data (PK-04). |
| FR-ACC-10 (part) | Documents is its own tab in the patient record (PK-13). |

### 5.2 Enquiry
| ID | Requirement |
|---|---|
| FR-ENQ-01 | Staff log an enquiry after the fact (date, channel, summary, and similar). |
| FR-ENQ-02 | Staff log each quotation (version, date, amount, and similar). |
| FR-ENQ-06 | Returning patients skip Enquiry. |

### 5.3 Assessment
| ID | Requirement |
|---|---|
| FR-ASM-01 | Log an assessment: method (in person, WhatsApp call, phone, video, email), findings and outcome. |
| FR-ASM-02 | The app does not change how assessment is done; in person when the doctor is abroad, otherwise remote. |

### 5.4 Planning
| ID | Requirement |
|---|---|
| FR-PLN-01 | Record the preliminary programme and approximate cost settled before travel, linked to the accepted quotation. |
| FR-PLN-07 | Staff record payments received (deposit, balance). No online payments (PK-06). |

### 5.5 Arrival
| ID | Requirement |
|---|---|
| FR-ARR-01 | Flight details (flight number, arrival time) entered by the clinic or the patient. |
| FR-ARR-02 | Pickup: car and driver details entered by the clinic, visible to the patient. |
| FR-ARR-03 | Accommodation and check-in details entered by the clinic, visible to the patient. |

### 5.6 Care
| ID | Requirement |
|---|---|
| FR-CAR-01 | Record post-arrival assessment findings. |
| FR-CAR-02 | Record doctor's notes. |
| FR-CAR-03 | Record prescribed medication. |
| FR-CAR-04 | Record daily treatments given. |
| FR-CAR-05 | Record daily diet. |
| FR-CAR-06 | Record daily accommodation or stay details. |
| FR-CAR-07 | Patient sees the daily schedule, diet and medicines. |
| FR-CAR-08 | Daily check-in on whether medicines are taken and how the treatment is going. Question set and length are open (PK-14; default five questions). |
| FR-CAR-14 | Patient sees the current medicine course, with history on request (PK-12). |

Therapists and kitchen do not log in; the coordinator enters on their behalf (PK-03).

### 5.7 Continuity
| ID | Requirement |
|---|---|
| FR-CON-01 | Log departure travel assistance. |
| FR-CON-02 | Post-departure diet and medication follow-ups as an interactive loop: patient reports how they feel, confirms medicine taken, flags diet issues. |
| FR-CON-03 | Check-in prompts are scheduled by the clinic. |
| FR-CON-04 | Log WhatsApp and phone consultations given after the patient is home. |
| FR-CON-05 | The record persists; repeat visits create a new episode starting at Assessment or Planning. |
| FR-CON-11 | Patient can request an extra consultation in the app; the clinic approves and schedules (PK-15). |

## 6. Non-functional requirements and constraints

All NFR targets are `[PROPOSED]` (BRD section 11) except where the decisions above set them. They are listed here as design inputs, not commitments.

- **Usability:** coordinator and doctor flows work on phone and laptop (BR-12). Patient screens are phone first, large text, usable by an older non-technical person with no training.
- **Accessibility:** target WCAG 2.2 AA on patient screens.
- **Privacy and security:** health data. Row-level security in the database, clinic isolation (ADR-20), private storage with short-lived signed links, audit trail, no health data in logs, staff MFA. Proposed in detail in the architecture.
- **Time handling:** store UTC, show the patient's local time.
- **Dummy data only** in code, seeds, tests and screenshots until the legal gate is passed (BR-08, BR-09).

## 7. Candidate requirements, unconfirmed

`[PROPOSED]` by Claude. Carried so the owner can accept, change or drop each one. Full list with sources in `parked-decisions.md` Part B. Grouped by what they unblock:

**Platform and trust**
- FR-ACC-05 patient sees only their own record; staff by role. FR-ACC-06 audit log of every view and change. FR-ACC-15 staff MFA. FR-ACC-16 and FR-ACC-17 staff move episodes between phases (logged); one permanent patient, many episodes.
- FR-ACC-08 clinic home screen (patient list with phase tag, filter, search, needs-attention block). FR-ACC-09 patient home screen (six-step journey bar plus a today card).
- FR-ACC-10 (rest) document store with per-document visibility. FR-ACC-11 in-app inbox and email. FR-ACC-12 in-app message thread. FR-ACC-13 patient rights tools (export, correct, erase).

**Onboarding:** FR-ONB-05 extra optional fields, FR-ONB-06 save draft, FR-ONB-07 email invite link, FR-ONB-09 duplicate warning, FR-ONB-10 link earlier enquiry notes.

**Enquiry to Planning:** FR-ENQ-03 to 05 (source, lead list, patient read-only history); FR-ASM-04 and 05 (medicines from assessment, shared versus private notes); FR-PLN-02 to 06 (plan status, checklist, visa tracker, info pack, one question thread). Field lists for FR-ENQ-01/02, FR-ASM-01 and the payments record.

**Arrival:** FR-ARR-04 arrival-day card; FR-ARR-05 "I have landed" and "I need help" buttons; FR-ARR-06 alert on flight edits; FR-ARR-07 second transfer leg; extra pickup fields (phone, plate, meeting point, time).

**Care:** FR-CAR-09 doctor review queue with flagged first; FR-CAR-11 shared or private notes; FR-CAR-12 build tomorrow's plan with "copy from yesterday" and templates, then publish; FR-CAR-13 therapy record per session.

**Continuity:** FR-CON-06 follow-up schedule builder; FR-CON-07 medicine supply tracker; FR-CON-09 end feedback form; FR-CON-10 departure documents handover; FR-CON-12 check-in trend view.

**Rules and data:** BR-02 patient-editable items (flight details, check-ins, uploads); BR-06 the app records and alerts only; BR-07 every view and change is logged; BR-08, BR-09, BR-10 data and publicity rules. The data model, authorisation matrix and ADRs in `architecture.md`, plus success targets and the release plan.

Recommendation for the owner review: confirm FR-ACC-05, 06, 15, 16, 17 and FR-ONB-07 first. They are needed by the walking skeleton and by the privacy design, and the build cannot be safe without them.

## 8. Epics and delivery order

Order follows the decided build order. Items marked * contain candidate requirements that need confirmation before they enter a sprint.

| Order | Epic | Contents |
|---|---|---|
| 1 | E-1 Foundation* | Sign-in (patient link, staff login), roles, clinic isolation, patient list, episode model*, audit log*, installable shell |
| 2 | E-2 Onboarding and documents | FR-ONB-01 to 04, 08; Documents tab; invite link* |
| 3 | E-3 Arrival | FR-ARR-01 to 03; arrival card* |
| 4 | E-4 Care | FR-CAR-01 to 08, 14; day plan builder*; doctor review queue* (flag rules parked) |
| 5 | E-5 Enquiry and quotation | FR-ENQ-01, 02, 06 |
| 6 | E-6 Assessment | FR-ASM-01, 02 (clinical fields parked) |
| 7 | E-7 Planning | FR-PLN-01, 07 (consent timing already decided) |
| 8 | E-8 Continuity | FR-CON-01 to 05, 11 |
| 9 | E-9 Notifications | Email and in-app inbox, scheduled prompts |
| 10 | E-10 Compliance and data rights | Consent records, export, correct, erase (periods parked) |
| 11 | E-11 Admin and templates | Users, diet, medicine and follow-up templates, clinic configuration |
| 12 | E-12 Hardening and launch | Accessibility, performance, security review, backup test, pilot |

**Release plan (`[PROPOSED]`):** R0 prototype with dummy data (E-1 to E-4 thin slice); R1 pilot with Ayurvedgram (E-5 to E-9); R2 improve (E-10, E-11, reporting). Real patient data only after the legal gate. Dates and team are not decided.

## 9. Open questions

Defaults are for design only and must be flagged. Do not implement an item without its decision.

| ID | Question | Working default |
|---|---|---|
| PK-01 | Sponsor's name; Ayurvedgram's real terminology and stages | Ravi decides |
| PK-04 | Consent wording and legal approval (DPDP, GDPR) | Versioned text; no real data until approved |
| PK-09 | What counts as a flag in check-ins (doctor) | None; the app applies only the doctor's rules |
| PK-10 | Ayurveda-specific structured fields (doctor) | Free text only |
| PK-11 | Follow-up schedule templates (doctor) | None |
| PK-14 | Check-in questions and length | Five questions |
| PK-18 | Retention, erasure periods and the real-data gate (lawyer) | No real patient data until passed |
| PK-19 | Success-measure targets | None |
| PK-20 | Go signal, first sprint scope, team and dates | Do not build |
| PK-21 | ABDM, Ayush Grid and other health-record rules | Not in v1 |
| PK-22 | Sending domain for email | None |
| PK-24 | Availability, maintenance window, backup RPO and RTO | None |
| PK-25 | Error tracking and monitoring tools | None |
| PK-27 | Malware scanning; HEIC conversion approach | No scanning |
| PK-28 | Extra protection for passport number | At-rest encryption and RLS only |
| PK-29 | Scheduler mechanism (Vercel cron or database) | Either, behind one interface |
| PK-30 | Update World Ayurveda Congress wording | Keep "Proposed" |

**Spikes before commitment:** S-1 web push on iPhone (not needed for v1); S-2 scheduler; S-3 India region and latency; S-4 one-time-link delivery through Resend; S-5 phone camera uploads and HEIC; S-6 RLS performance and test harness; S-7 data processing agreements per vendor.

## 10. Dependencies

A doctor session for flags, clinical fields and follow-up templates; a lawyer for consent, retention and cross-border rules; accounts for Vercel, Supabase (India), Resend with a verified domain, and a domain name for the app.

## 11. Traceability

Owner decisions are recorded in `parked-decisions.md` Part A (marked "Resolved") and in the BRD requirement tables. Each requirement in sections 4 and 5 maps to a BRD ID of the same name. Candidate items in section 7 are the `[PROPOSED]` rows of Part B.
