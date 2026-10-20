# Business Requirements Document (BRD)
## Ayurvedic Clinic Patient Journey App

| Field | Value |
|---|---|
| Version | 0.1 (draft for BMAD pickup) |
| Date | 2026-10-20 |
| Owner | Ravi (product owner) |
| Status | Draft. Not yet reviewed screen by screen by the owner |
| Companion documents | `architecture.md`, `parked-decisions.md`, `BMAD_PICKUP.md`; source material in `Ayurveda_Journey_App_MASTER.md` |
| Build method | Claude Code with the BMAD method (owner's decision) |

### How to read this document
- **Status tags** on every requirement and decision:
  - `[DECIDED]` the owner said it.
  - `[PROPOSED]` Claude's suggestion, **not decided by the owner, therefore parked until confirmed.** BMAD may carry it into the PRD as a "candidate, unconfirmed" item and use the stated default if a design needs one, but must not commit it to a sprint without the owner's confirmation. Every `[PROPOSED]` item is listed in `parked-decisions.md` (Part B).
  - `[PARKED]` an open question or deferred decision. Do not build it and do not guess. Each has an ID (`PK-nn`) in `parked-decisions.md` (Part A), with a default only where one is stated.
- **IDs**: `BO-n` business objective, `FR-xxx-nn` functional requirement, `NFR-nn` non-functional, `BR-nn` business rule, `AS-n` assumption, `CN-n` constraint, `RK-n` risk, `E-n` candidate epic.
- **Priority** (MoSCoW) is Claude's proposal for every item and is itself `[PROPOSED]`.
- Dummy data only until the owner confirms otherwise (see PK-18 and compliance section).

---

## 1. Executive summary

A single Ayurvedic clinic in India treats international patients whose whole journey (enquiry, medical assessment, planning, arrival, treatment, follow-up, repeat visits) runs over WhatsApp, email and phone calls. Records, travel plans and medical history are scattered, staff juggle three channels, and patients can lose vital information.

The product is one web application, installable to the phone home screen, with role-based views: a clinic dashboard for staff and doctors, and a patient view. Both sit on one shared patient record that lasts across visits. The app does not replace the first contact channels or the way assessments are done; it captures the outcome and the lineage, and runs the structured parts of the journey (travel logistics, daily care plan, check-ins, follow-up). `[DECIDED]`

## 2. Business context and problem

### 2.1 Context
- The customer is the clinic, not the patient. First deployment is one specific clinic. `[DECIDED]`
- Related work: a World Ayurveda Congress presentation, "Technology-enabled Ayurveda Medical Tourism", describes the journey stages and lists a patient app/portal and a longitudinal digital record as proposed next steps. It reports more than 510 patients from 13 countries and about nine years of operations at Ayurvedgram, Pune. The first deployment is for Ayurvedgram, Pune `[DECIDED]`. The product must stay clinic-agnostic so other clinics can be added later `[DECIDED]` (see BR-11, CN-6). Sponsor identity is still open (PK-01).
- Visa context: foreign patients typically travel on an Ayush (AY) visa which needs a supporting letter from an accredited Ayush institution; attendants use AY-2, up to two at a time (source: Indian consulate page, see research notes).

### 2.2 Problem statement `[DECIDED]`
1. There is no central place for the clinic to access a patient's records (travel plan, medical history, quotation, assessment outcome).
2. Patients must check several channels (WhatsApp, email, phone) and may lose vital information.
3. Information depends on individual staff members' inboxes and phones.

### 2.3 Opportunity
Public medical-tourism platforms are marketplace-style and Ayurveda clinic software is OPD-centred. Neither was found to cover the international journey (visa, pickup, stay, daily care, remote follow-up) for a single clinic with WhatsApp as the front door. See `01_research.md`.

## 3. Business objectives and success measures `[PROPOSED]`

| ID | Objective | Measure (target to be agreed, PK-19) |
|---|---|---|
| BO-1 | One source of truth per patient | Share of active patients with a complete record |
| BO-2 | Cut staff time spent finding information | Time to find a patient's travel and medicine details (minutes) |
| BO-3 | Fewer lost or repeated messages | Count of "where is my pickup/plan" style messages on WhatsApp |
| BO-4 | Keep patients engaged during care and after departure | Check-in response rate during Care and Continuity |
| BO-5 | Preserve lineage from first enquiry | Share of quotations and assessments logged against the patient record |
| BO-6 | Encourage repeat visits | Repeat-visit rate tracked from the record |
| BO-7 | Stay compliant with privacy rules | Zero unlogged access to patient data; consent recorded for every patient |

## 4. Scope

### 4.1 In scope for the first release `[PROPOSED]`
- Foundation: login, roles, patient list, audit log.
- Onboarding with documents.
- Arrival and Care (daily-use core).
- Enquiry, Assessment and Planning logs.
- Continuity: follow-up check-ins and consultation log.
- Installable web app (PWA), English language.
- Email notifications and in-app inbox.

### 4.2 Out of scope for the first release `[PROPOSED]`
- Native iOS and Android apps. (`[DECIDED]` web first; native later only if needed.)
- Operating more than one clinic in production, onboarding other clinics, marketplace features, commissions. (The design must be ready for it; see BR-11.)
- Online payments (see PK-06).
- Sending WhatsApp from inside the app (see PK-08).
- Integration with national health-record systems such as ABDM / Ayush Grid (not researched; PK-21).
- Automated clinical advice, diagnosis or interpretation of check-in answers.

### 4.3 Parked scope
Items awaiting a decision are in section 17 and `parked-decisions.md`.

## 5. Stakeholders and users

| Stakeholder | Role | Interest |
|---|---|---|
| Ravi | Product owner | Outcome, scope, decisions |
| Clinic owner / management | Sponsor at Ayurvedgram, Pune (person not confirmed, PK-01) | Efficiency, patient experience, repeat business |
| Doctor(s) | Clinical lead (named doctor not confirmed, PK-10) | Assessment records, daily review, follow-up |
| Front desk / coordinator | Daily operator | Fast data entry, travel and logistics |
| Therapists and kitchen | Delivery of care | Daily schedule (login or not: PK-03) |
| Patient | Traveller | One clear view of the plan, easy check-ins |
| Attendant | Travelling companion (up to two) | Logistics view (access: PK-17) |
| Lawyer / data protection advisor | Compliance | Consent, GDPR, DPDP (not yet engaged, PK-04) |

### 5.1 Personas (illustrative, invented)
- **Coordinator (Meera):** enters flight, pickup and stay details from a phone; wants to copy yesterday's plan and publish in one tap.
- **Doctor (Dr. A):** wants flagged check-ins first, writes a note and adjusts a medicine without leaving the screen.
- **Patient (Anna, Austria, age 60s, not very technical):** opens a link from WhatsApp, sees today's plan, answers a one-minute check-in.
- **Returning patient (Marc):** was treated last year; skips Enquiry and starts at Assessment or Planning.

## 6. Journey overview `[DECIDED]`

Enquiry → Assessment → Planning → Arrival → Care → Continuity → (return visit: Assessment or Planning)

A patient has one permanent record and many **episodes** (one per visit). Each episode moves through the phases. Phase changes are made by staff and logged. `[PROPOSED]` (episode model)

## 7. As-is and to-be by phase

| Phase | As-is | To-be (decided unless tagged) |
|---|---|---|
| Enquiry | Patient reaches out by WhatsApp, email or phone. Clinic replies with information and a quotation on the same channels. Nothing logged centrally. | First contact stays on those channels. Clinic logs the enquiry and quotation in the app and onboards the patient so later phases run in the app. |
| Assessment | In person (Nadi Pariksha) when the doctor is on a foreign trip; otherwise over a WhatsApp call. Findings not centrally recorded. | Both paths stay as they are. The app logs the method used (phone, WhatsApp, email, physical examination) and the outcome for future reference. |
| Planning | A wider programme is settled before travel, with an approximate cost (quotation). Programme details may be refined by the doctor on arrival. Communication on WhatsApp and email. | Preliminary programme and approximate cost recorded in the app before travel. Consent timing `[PARKED]` PK-04. Checklist, visa tracker and info pack `[PROPOSED]`. |
| Arrival | Flight, pickup and accommodation communicated by WhatsApp and email. | Flight details (number, arrival time) entered by clinic or patient. Pickup (car, driver) and accommodation/check-in entered by clinic. All visible to the patient. |
| Care | Daily schedule, diet and doctor contact on WhatsApp. | Clinic records post-arrival assessment, doctor's notes, prescribed medication, daily treatments, daily diet and daily accommodation. Patient sees schedule, diet and medicines. Daily check-ins on medicines taken and on how the treatment is going. |
| Continuity | Follow-up by email, WhatsApp and video call. Prescriptions by email. | Departure travel assistance logged. Post-departure diet and medication follow-ups as an interactive loop with clinic-scheduled check-ins. WhatsApp and phone consultations after the patient is home are logged. The record persists for repeat visits. |

Returning patients skip Enquiry and go to Assessment or Planning. `[DECIDED]`

## 8. Functional requirements

Format: ID, requirement, actor, status, priority (MoSCoW, itself proposed). Requirements marked `[DECIDED]` come from the owner's statements. Where only the field detail is proposed, the row says so.

### 8.1 Cross-cutting and access (ACC)

| ID | Requirement | Actor | Status | Pri |
|---|---|---|---|---|
| FR-ACC-01 | One application with role-based logins for clinic staff and patients, sharing one backend and patient record | All | DECIDED | Must |
| FR-ACC-02 | Roles: patient, clinic staff (front desk/coordinator), doctor, admin | All | DECIDED for clinic vs patient; staff split PROPOSED | Must |
| FR-ACC-03 | Therapist and kitchen roles | Therapist, kitchen | Not in v1 (PK-03 resolved): coordinator enters on their behalf | Won't (v1) |
| FR-ACC-04 | Attendant (companion) view-only access to logistics if the patient grants it | Attendant | PARKED (PK-17) | Could |
| FR-ACC-05 | A patient can see only their own record; staff see by role | All | PROPOSED | Must |
| FR-ACC-06 | Audit log of every view and change of patient data (who, what, when, record) | System | PROPOSED | Must |
| FR-ACC-07 | Installable web app: appears on the home screen of patient and clinic phones | All | DECIDED | Must |
| FR-ACC-08 | Clinic home screen: patient list with phase tag, filter by phase, search, and a "needs attention" block | Staff | PROPOSED (mockup direction accepted by owner) | Must |
| FR-ACC-09 | Patient home screen: six-step journey bar plus a card for what matters today | Patient | PROPOSED (mockup direction accepted) | Must |
| FR-ACC-10 | Document store for passport scans, medical records, letters, summaries, with per-document visibility. Whether Documents is its own tab in the record is PARKED (PK-13, default: own tab) | Staff, patient | PROPOSED | Must |
| FR-ACC-11 | In-app inbox and email notifications | System | PROPOSED | Should |
| FR-ACC-12 | In-app message thread between patient and clinic | Patient, staff | PROPOSED | Could |
| FR-ACC-13 | Patient rights tools: export, correct, erase on request | Admin | PROPOSED (compliance driven; periods PARKED PK-18) | Must |
| FR-ACC-14 | English-language interface for v1; further languages | All | English PROPOSED; others PARKED (PK-07) | Must / Could |
| FR-ACC-15 | Multi-factor authentication for staff | Staff | PROPOSED | Must |
| FR-ACC-16 | Staff can move a patient episode forward or back between phases; each change logged | Staff | PROPOSED | Must |
| FR-ACC-17 | Episode model: one permanent patient, many episodes (one per visit) | System | PROPOSED | Must |
| FR-ACC-18 | Sending WhatsApp messages from inside the app | Staff | PARKED (PK-08). Default: staff log WhatsApp conversations manually | Could |

### 8.2 Onboarding (ONB)

| ID | Requirement | Actor | Status | Pri |
|---|---|---|---|---|
| FR-ONB-01 | Dedicated screen/flow to onboard a new patient, separate from the patient list | Staff | DECIDED | Must |
| FR-ONB-02 | Required fields: name, email, phone, nationality | Staff | DECIDED | Must |
| FR-ONB-03 | Optional but captured: photo, date of birth, passport number, emergency contact | Staff | DECIDED | Must |
| FR-ONB-04 | Optional uploads: passport scan, previous medical records (several files) | Staff, patient | DECIDED | Must |
| FR-ONB-05 | Additional optional fields: preferred language, time zone, dietary preferences, attendant details | Staff | PROPOSED | Should |
| FR-ONB-06 | Save a draft and resume later | Staff | PROPOSED | Should |
| FR-ONB-07 | Send the patient an invite link (email); patient sets access without installing anything first | System | PROPOSED | Must |
| FR-ONB-08 | Capture consent during onboarding (step 2 of the flow) | Patient/staff | PARKED (PK-04: timing and wording) | Must |
| FR-ONB-09 | Warn on possible duplicates (same email, phone or passport number) | System | PROPOSED | Should |
| FR-ONB-10 | Link earlier enquiry notes or quotation already sent over WhatsApp or email | Staff | PROPOSED | Should |

### 8.3 Enquiry (ENQ)

| ID | Requirement | Actor | Status | Pri |
|---|---|---|---|---|
| FR-ENQ-01 | Log an enquiry after the fact: date, channel (WhatsApp, email, phone, other), summary, treatment interest, handled by, attachments | Staff | Logging DECIDED; field list PROPOSED | Must |
| FR-ENQ-02 | Log each quotation: version, date sent, amount and currency, inclusions and exclusions, validity, status, file | Staff | Logging DECIDED; field list PROPOSED | Must |
| FR-ENQ-03 | Record enquiry source (referral, website, event, repeat) | Staff | PROPOSED | Could |
| FR-ENQ-04 | List of enquiries not yet onboarded, for follow-up | Staff | PROPOSED | Could |
| FR-ENQ-05 | After onboarding the patient can see their enquiry history and quotations, read only | Patient | PROPOSED | Should |
| FR-ENQ-06 | Returning patients skip Enquiry | System | DECIDED | Must |

### 8.4 Assessment (ASM)

| ID | Requirement | Actor | Status | Pri |
|---|---|---|---|---|
| FR-ASM-01 | Log an assessment: date, method (in person, WhatsApp call, phone, video, email), doctor, findings, outcome, attachments | Doctor/staff | Method, findings, outcome DECIDED; extra fields PROPOSED | Must |
| FR-ASM-02 | The app does not change how assessment is done; in-person when the doctor is abroad, otherwise remote | n/a | DECIDED | Must |
| FR-ASM-03 | Doctor-defined structured Ayurveda fields (for example prakriti, pulse findings, chief complaint) | Doctor | PARKED (PK-10) | Should |
| FR-ASM-04 | Log medicines prescribed at assessment with start date and duration, to feed check-ins | Doctor | PROPOSED | Should |
| FR-ASM-05 | Patient sees a summary of the outcome and advice; notes can be marked private to the clinic | Patient, doctor | PROPOSED | Should |

### 8.5 Planning (PLN)

| ID | Requirement | Actor | Status | Pri |
|---|---|---|---|---|
| FR-PLN-01 | Record the preliminary programme and approximate cost settled before travel, linked to the accepted quotation | Staff/doctor | DECIDED | Must |
| FR-PLN-02 | Plan status: provisional, confirmed, refined on arrival | Staff | PROPOSED | Should |
| FR-PLN-03 | Pre-arrival checklist with owner (patient or clinic), status and due date | Staff, patient | PROPOSED | Should |
| FR-PLN-04 | Visa tracker per traveller: type (AY-1 patient, AY-2 attendants, up to two), supporting letter, application status, expiry | Staff | PROPOSED | Should |
| FR-PLN-05 | Pre-arrival information pack in the app (what to bring, weather, diet, transfers) | Staff | PROPOSED; content and languages PARKED (PK-07) | Could |
| FR-PLN-06 | Pre-arrival questions kept in one thread | Patient, staff | PROPOSED | Could |
| FR-PLN-07 | Payments (deposit, balance) | Staff | DECIDED (PK-06): record payments received, no online payments. Data fields PROPOSED | Should |
| FR-PLN-08 | Capture consent at plan confirmation as an alternative to onboarding | Patient | PARKED (PK-04) | Must |

### 8.6 Arrival (ARR)

| ID | Requirement | Actor | Status | Pri |
|---|---|---|---|---|
| FR-ARR-01 | Flight details (flight number, arrival time) entered by the clinic or the patient | Staff, patient | DECIDED | Must |
| FR-ARR-02 | Pickup: car and driver details entered by the clinic, visible to the patient | Staff | DECIDED; extra fields (phone, plate, meeting point, time) PROPOSED | Must |
| FR-ARR-03 | Accommodation and check-in details entered by the clinic, visible to the patient | Staff | DECIDED | Must |
| FR-ARR-04 | Arrival-day card on the patient home screen: flight, who meets you, where to stay | Patient | PROPOSED | Should |
| FR-ARR-05 | "I have landed" and "I need help" buttons that alert the coordinator | Patient | PROPOSED | Could |
| FR-ARR-06 | Notify the coordinator when the patient edits flight details | System | PROPOSED | Should |
| FR-ARR-07 | Second transfer leg (airport to city) as a further pickup item | Staff | PROPOSED | Could |

### 8.7 Care (CAR)

| ID | Requirement | Actor | Status | Pri |
|---|---|---|---|---|
| FR-CAR-01 | Record post-arrival assessment findings | Doctor | DECIDED | Must |
| FR-CAR-02 | Record doctor's notes | Doctor | DECIDED | Must |
| FR-CAR-03 | Record prescribed medication | Doctor | DECIDED | Must |
| FR-CAR-04 | Record daily treatments given | Staff | DECIDED | Must |
| FR-CAR-05 | Record daily diet | Staff | DECIDED | Must |
| FR-CAR-06 | Record daily accommodation or stay details | Staff | DECIDED | Must |
| FR-CAR-07 | Patient sees the daily schedule, diet and medicines | Patient | DECIDED | Must |
| FR-CAR-08 | Daily check-in: whether medicines are taken, and how the treatment is going | Patient | DECIDED; question set (sleep, appetite, free text) PROPOSED, length PARKED (PK-14) | Must |
| FR-CAR-09 | Doctor review queue: today's check-ins, flagged first; notes and medicine change from the same screen | Doctor | PROPOSED | Should |
| FR-CAR-10 | Rules that decide what counts as a flag | Doctor | PARKED (PK-09). The app applies only rules the doctor sets | Must |
| FR-CAR-11 | Doctor notes marked shared with patient or private to clinic | Doctor | PROPOSED | Should |
| FR-CAR-12 | Build tomorrow's plan once, with "copy from yesterday" and doctor-set templates for diet and medicines, then publish to the patient | Staff | PROPOSED | Should |
| FR-CAR-13 | Therapy record per session (therapy, therapist, duration, notes) | Staff | PROPOSED | Could |
| FR-CAR-14 | Patient sees whole medicine history or only the current course | Patient | PARKED (PK-12). Default: current course | Should |

### 8.8 Continuity (CON)

| ID | Requirement | Actor | Status | Pri |
|---|---|---|---|---|
| FR-CON-01 | Log departure travel assistance | Staff | DECIDED | Must |
| FR-CON-02 | Post-departure diet and medication follow-ups as an interactive loop; patient reports how they feel, confirms medicine taken, flags diet issues | Patient | DECIDED | Must |
| FR-CON-03 | Check-in prompts are scheduled by the clinic, not initiated by the patient | Staff | DECIDED | Must |
| FR-CON-04 | Log WhatsApp and phone consultations given after the patient is home | Doctor/staff | DECIDED | Must |
| FR-CON-05 | The record persists; repeat visits create a new episode starting at Assessment or Planning | System | DECIDED | Must |
| FR-CON-06 | Follow-up schedule builder using doctor-set templates | Doctor | PROPOSED; template content PARKED (PK-11) | Should |
| FR-CON-07 | Medicine supply tracker: when a supply runs out so the clinic can reorder | Staff | PROPOSED | Could |
| FR-CON-08 | Return-visit nudge to the coordinator after a set period | Staff | PROPOSED; timing PARKED (PK-16) | Could |
| FR-CON-09 | End-of-programme feedback form | Patient | PROPOSED | Could |
| FR-CON-10 | Departure documents handover (prescription, diet guidance, treatment summary) | Staff | PROPOSED | Should |
| FR-CON-11 | Patient can request an extra consultation in the app | Patient | PARKED (PK-15). Default: reply to clinic prompts only | Could |
| FR-CON-12 | Trend view of check-in scores for the doctor | Doctor | PROPOSED | Could |

## 9. Business rules

| ID | Rule | Status |
|---|---|---|
| BR-01 | First contact, quotations and assessment calls stay on WhatsApp, email and phone; the app records the outcome and lineage | DECIDED |
| BR-02 | Clinic enters, patient reads. Patient-editable items: flight details, check-ins, document uploads | Flight details DECIDED; rest PROPOSED |
| BR-03 | Follow-up check-ins are initiated by the clinic's schedule | DECIDED |
| BR-04 | Returning patients skip Enquiry | DECIDED |
| BR-05 | The programme and approximate cost are settled before travel; the doctor may refine on arrival | DECIDED |
| BR-06 | The app records and alerts. It never gives medical advice or interprets answers medically; the doctor defines flags | PROPOSED |
| BR-07 | Every view and change of patient data is logged | PROPOSED |
| BR-08 | Mockups, prototypes and test environments use invented patient data only | PROPOSED (applied so far in all mockups) |
| BR-09 | Real patient data may enter the system only after legal review of consent, GDPR and DPDP | PROPOSED go-live gate (PK-18) |
| BR-11 | The product is clinic-agnostic. Nothing specific to Ayurvedgram (name, branding, terminology, phase names, templates, staff, locale defaults) is hard-coded; it is clinic configuration. Ayurvedgram is the first clinic (tenant) | DECIDED |
| BR-12 | Coordinator and doctor can do every task on either phone or laptop. Responsive design, no device-specific features, same data on both | DECIDED |
| BR-10 | A patient's name or story is shown publicly (for example in a presentation) only with that patient's consent | PROPOSED |

## 10. Data requirements

Detailed entities and relationships are in `architecture.md` section 6. Business-level data classes:

| Class | Examples | Sensitivity | Retention |
|---|---|---|---|
| Identity and contact | name, email, phone, nationality, DOB, photo | Personal | PARKED (PK-18) |
| Identity documents | passport number, passport scan | High | PARKED (PK-18); keep only as long as visa and travel require (proposed) |
| Health data | medical records, assessments, medicines, check-ins, notes | Special (health) | PARKED (PK-18) |
| Travel and logistics | flights, pickups, stay | Personal | PARKED (PK-18) |
| Commercial | quotations, programme cost, payments (if any) | Business | PARKED (PK-18) |
| Consent and audit | consent records, access logs | Compliance | Keep for the life of the patient record (proposed) |

## 11. Non-functional requirements (all targets `[PROPOSED]`)

| ID | Area | Requirement |
|---|---|---|
| NFR-01 | Usability | Clinic staff and doctors use phone or laptop interchangeably (BR-12); patient screens phone first; large readable text; patient screens usable by a non-technical older user with no training |
| NFR-02 | Accessibility | Target WCAG 2.2 AA for patient screens |
| NFR-03 | Performance | Main screens usable within about 3 seconds on a typical mobile connection; daily check-in submittable in under a minute |
| NFR-04 | Availability | Business-hours availability matters most; targets and maintenance windows PARKED (PK-24) |
| NFR-05 | Security | Encryption in transit and at rest; role-based access; row-level security at the database; signed, expiring file links; staff MFA; session timeouts on shared devices |
| NFR-06 | Privacy | Data minimisation; explicit, versioned, revocable consent; patient rights tooling; audit trail |
| NFR-07 | Auditability | Immutable log of access and changes to patient data |
| NFR-08 | Data location | Single primary region; choice PARKED (PK-05) |
| NFR-09 | Backup and recovery | Regular backups and a tested restore; RPO and RTO numbers PARKED (PK-24) |
| NFR-10 | Observability | Error tracking and structured logs without personal health data in logs |
| NFR-11 | Maintainability | One codebase; automated tests; migrations in version control; environments for development, staging, production |
| NFR-12 | Browser support | Current Chrome, Safari, Edge, Firefox on phone and desktop |
| NFR-13 | Installability | Installable to the home screen; behaviour of web push on iPhone to be verified at build time |
| NFR-14 | Localisation readiness | Text kept in resource files so languages can be added later (PK-07) |
| NFR-15 | Time handling | Store times in UTC with the patient's time zone; show local time to the patient (flights, check-in prompts) |

## 12. Compliance and regulatory notes

These are first-pass findings from public pages (see `01_research.md`) and are **not legal advice**. A lawyer must review before any real data is stored (PK-04, PK-18).

- **India DPDP Act and Rules:** guidance read says explicit informed consent is required, blanket or implied consent is invalid, consent should be revocable, patients can access, correct and erase data, breaches must be reported within 72 hours, and a data protection officer and impact assessments apply to high-risk processing. Notice wording, retention and cross-border rules were not covered by the sources read.
- **GDPR for European patients:** Article 49 allows a transfer to a third country on the data subject's explicit consent after the risks are explained, or where necessary for a contract or pre-contractual steps the patient requested. Whether an India-based clinic has other duties (for example an EU representative) was not established.
- **Ayush visa:** a supporting letter from an accredited Ayush institution is required for treatment visits (not wellness-only visits); attendants use AY-2, up to two at a time. The app should store the letter and track visa status.
- **Not researched:** health-record rules in India (for example telemedicine and record-keeping rules), ABDM / Ayush Grid alignment, payment regulation for foreign cards. Parked (PK-21, PK-18).

## 13. Assumptions, constraints, dependencies

### Assumptions
| ID | Assumption |
|---|---|
| AS-1 | The first clinic is a single site with one to a few doctors and a small operations team |
| AS-2 | Patients have a smartphone and email; many already use WhatsApp |
| AS-3 | Coordinator and doctor use either phone or laptop during the working day (owner, PK-02) |
| AS-4 | The prototype uses dummy data; production data comes after legal review |
| AS-5 | English is enough for the first release (PK-07) |

### Constraints
| ID | Constraint |
|---|---|
| CN-1 | Web application first (owner decision); no native apps in the first release |
| CN-2 | Stack: Next.js, Vercel, Supabase, as used on the owner's Invento app (owner decision) |
| CN-3 | Development is cloud driven (owner decision) |
| CN-4 | Built with Claude Code and the BMAD method (owner decision) |
| CN-6 | Multi-tenant ready from day one: every clinic-owned record carries a clinic key and access is isolated per clinic. Only one clinic is live in v1 (owner decision) |
| CN-5 | No building until the owner gives the go signal. The owner has said the build will be done in Claude Code with BMAD; the go date and first sprint scope are PARKED (PK-20) |

### Dependencies
- Owner answers to the parked decisions marked as blocking in `parked-decisions.md`.
- A doctor to define clinical fields, flag rules and follow-up templates (PK-09, PK-10, PK-11).
- Legal advice on consent, GDPR and DPDP (PK-04, PK-18).
- Accounts and keys for hosting, database, email sending.

## 14. Risks

| ID | Risk | Mitigation |
|---|---|---|
| RK-1 | Staff see entry as double work and stop using the app | Very short forms, templates, copy from yesterday, entry on phone |
| RK-2 | Older or non-technical patients struggle | Link-based access, large text, optional attendant view |
| RK-3 | Compliance gaps before real data is stored | Legal review gate; dummy data until then |
| RK-4 | Over-claiming status in public material (for example calling features "piloting") | Use In use / Piloting / Proposed discipline in presentations; whether to update the congress presentation wording is PARKED (PK-30) |
| RK-5 | Clinical fields and flags designed without a doctor | Doctor session before building forms (PK-09, PK-10) |
| RK-6 | WhatsApp costs and rules surprise the budget | Start with email and in-app prompts; evaluate the API later (PK-08) |
| RK-7 | Health data leaks through logs, files or exports | No health data in logs; signed URLs; row-level security; access audit |
| RK-8 | Scope grows before the core works | Build order: foundation, then Arrival and Care |

## 15. Candidate epics for BMAD `[PROPOSED]`

BMAD's analyst, PM and architect agents should turn these into a PRD, epics and stories. Order is a suggestion (PK-20).

| ID | Epic | Covers | Notes |
|---|---|---|---|
| E-1 | Foundation | Auth, roles, patient list, episode model, audit log, installable shell | FR-ACC-01 to 09, 15 to 17 |
| E-2 | Onboarding and documents | Onboarding flow, uploads, invite link, duplicate warning | FR-ONB-*, FR-ACC-10 |
| E-3 | Arrival | Flight, pickup, stay, arrival-day card, change alerts | FR-ARR-* |
| E-4 | Care | Daily plan builder, patient day view, check-ins, doctor review queue | FR-CAR-* (flag rules parked) |
| E-5 | Enquiry and quotation | Enquiry log, quotation versions, lead list | FR-ENQ-* |
| E-6 | Assessment | Assessment log, private/shared notes, medicines from assessment | FR-ASM-* (clinical fields parked) |
| E-7 | Planning | Programme, checklist, visa tracker, info pack | FR-PLN-* (payments, consent parked) |
| E-8 | Continuity | Departure handover, follow-up schedule, check-in loop, consultation log, supply tracker, return nudge | FR-CON-* |
| E-9 | Notifications | In-app inbox, email, scheduled prompts | FR-ACC-11; WhatsApp parked |
| E-10 | Compliance and data rights | Consent records, export/correct/erase, retention jobs | FR-ONB-08, FR-ACC-13 (largely parked) |
| E-11 | Admin and templates | User management, diet, medicine and follow-up templates, settings | Supports E-4 and E-8 |
| E-12 | Hardening and launch | Accessibility, performance, security review, backup test, pilot with the clinic | NFR-* |

### Example story seeds (to be written by BMAD)
- As a coordinator, I can onboard a patient with only four required fields so I can start the record in under two minutes.
- As a patient, I can open my invite link on my phone and see my arrival details without installing anything.
- As a coordinator, I can copy yesterday's plan for a patient and publish it so the patient sees tomorrow's schedule.
- As a doctor, I can see flagged check-ins first and mark them reviewed with a note.
- As a patient, I can answer a one-minute check-in and see that it was received.

## 16. Release plan `[PROPOSED]`

| Release | Content | Data |
|---|---|---|
| R0 Prototype | E-1, E-2, E-3, E-4 thin slice, clickable and working end to end | Dummy only |
| R1 Pilot with the clinic | Add E-5, E-6, E-7, E-8, E-9 basics | Real data only after legal gate (PK-18) |
| R2 Improve | E-10, E-11, reporting, extra language, WhatsApp decision | Real |

Release dates and team size are not decided (PK-20).

## 17. Parked items summary

The full register with defaults, blockers and recommended resolution is in `parked-decisions.md`. Parked IDs: PK-01 to PK-30.

## 18. Glossary

| Term | Meaning |
|---|---|
| Ayush | Indian government grouping of Ayurveda, Yoga and Naturopathy, Unani, Siddha, Homeopathy |
| AY-1 / AY-2 | Ayush visa for the patient / for attendants |
| Nadi Pariksha | Pulse diagnosis used in Ayurveda |
| Panchakarma | Ayurvedic detoxification therapy programme |
| Prakriti | Ayurvedic constitution type |
| Episode | One visit or treatment cycle of a patient |
| PWA | Progressive web app: a web app installable to the home screen |
| RLS | Row-level security in the database |
| DPDP | India's Digital Personal Data Protection Act |
| BMAD | Breakthrough Method for Agile AI-Driven Development |
| WAC | World Ayurveda Congress |

## 19. Traceability to the owner's decisions

| Owner decision (master file A3) | Requirements |
|---|---|
| 1 Clinic is the customer; one clinic first (Ayurvedgram), agnostic design for others | Sections 2, 4; BR-11, CN-6 |
| 3 One app, role-based | FR-ACC-01, 02 |
| 4 Web, home screen | FR-ACC-07, CN-1 |
| 5 Next.js, Vercel, Supabase | CN-2 |
| 7 Enquiry logged, channels unchanged | FR-ENQ-01, 02, BR-01 |
| 8 Assessment logged | FR-ASM-01, 02 |
| 9 Planning programme and cost before travel | FR-PLN-01, BR-05 |
| 10 Arrival entries | FR-ARR-01 to 03 |
| 11 Care entries and check-ins | FR-CAR-01 to 08 |
| 12 Continuity | FR-CON-01 to 05 |
| 13 Returning patients | FR-ENQ-06, FR-CON-05, BR-04 |
| 14 Onboarding fields | FR-ONB-01 to 04 |
| 15 No building yet | CN-5 |
