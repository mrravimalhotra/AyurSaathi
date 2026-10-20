# Project Brief
## AyurSaathi: Ayurvedic Clinic Patient Journey App

Version 0.1, 2026-10-20. Written by the BMAD analyst step from `brd.md` sections 1 to 3. Status tags follow the BRD: only `[DECIDED]` items are requirements. Everything else is unconfirmed. No code until the go signal (PK-20).

## 1. Problem `[DECIDED]`
An Ayurvedic clinic in India treats international patients. Their whole journey (enquiry, assessment, planning, arrival, care, continuity, repeat visits) runs over WhatsApp, email and phone. As a result:
1. The clinic has no central place for a patient's travel plan, medical history, quotation and assessment outcome.
2. Patients check several channels and can lose vital information.
3. Information lives in individual staff inboxes and phones.

## 2. Proposed solution `[DECIDED]`
One installable web app (PWA) with role-based views: a clinic dashboard for staff and doctors, and a patient view. Both sit on one permanent patient record. The app does not replace first contact channels or the way assessments are done. It logs the outcome and lineage, and runs the structured parts of the journey: travel logistics, daily care plan, check-ins, follow-up.

- Customer: the clinic, not the patient. First clinic is Ayurvedgram, Pune. The product is clinic-agnostic and multi-tenant ready (BR-11, CN-6, ADR-20): clinic-specific names, branding, terminology and templates are configuration, not code. Only one clinic is live in v1.
- Stack: Next.js, Vercel, Supabase. Built with Claude Code and BMAD.
- Journey: Enquiry → Assessment → Planning → Arrival → Care → Continuity → return visit (Assessment or Planning).

## 3. Users
Coordinator (daily data entry) and Doctor (reviews check-ins, notes, medicines), both on either phone or laptop (BR-12), Patient (older, non-technical, opens a link on a phone), Admin. Therapist, kitchen and attendant access are parked (PK-03, PK-17).

## 4. Goals `[PROPOSED]`, targets parked (PK-19)
BO-1 one source of truth per patient; BO-2 less time finding information; BO-3 fewer lost or repeated WhatsApp messages; BO-4 engagement during care and after departure; BO-5 lineage from first enquiry; BO-6 repeat visits; BO-7 privacy compliance.

## 5. Scope
- **Decided, build to these:** FR-ACC-01, 07; FR-ONB-01 to 04; FR-ENQ-01, 02, 06; FR-ASM-01, 02; FR-PLN-01; FR-ARR-01 to 03; FR-CAR-01 to 08; FR-CON-01 to 05; BR-01, 03, 04, 05.
- **Candidate, unconfirmed:** the rest of the BRD marked `[PROPOSED]` (see `parked-decisions.md` Part B).
- **Out of scope for release 1 (proposed):** native apps, running or onboarding other clinics (design is tenant-ready), online payments, WhatsApp sending, ABDM integration, automated clinical advice.

## 6. Constraints
Web first. Dummy data only until legal review of consent, GDPR and DPDP (BR-08, BR-09). The app records and alerts; it never gives medical advice (BR-06). Clinical fields and flag rules must come from a doctor (PK-09, PK-10).

## 7. Risks to watch
Double-entry fatigue for staff (RK-1), older patients struggling (RK-2), compliance before real data (RK-3), clinical design without a doctor (RK-5), scope growth (RK-8).

## 8. Questions blocking planning
Tracked in `parked-decisions.md`: PK-01 (sponsor name; clinic is Ayurvedgram), PK-04 (consent, can stay parked for planning), PK-05 (hosting region, can stay parked), PK-20 (go signal and first sprint scope).

## 9. Next BMAD steps
PM: write the PRD (decided items in the body, proposed items under "Candidate requirements, unconfirmed"). UX: review `ux/mockups.html` screen by screen with the owner. Architect: review each proposed ADR and run spikes S-1 to S-7. PO: shard and check epics. Build only after the go signal.
