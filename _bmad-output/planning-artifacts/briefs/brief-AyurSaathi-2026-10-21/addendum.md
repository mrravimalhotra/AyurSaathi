# Addendum: AyurSaathi product brief

Detail that belongs downstream (PRD, architecture), not in the brief.

## Decisions already made (owner, 2026-10-20 to 2026-10-22)
Ayurvedgram first and clinic-agnostic; coordinator and doctor on phone or laptop; no therapist, kitchen or attendant logins; English only; consent captured at onboarding step 2 (wording needs a lawyer); India hosting (Mumbai preferred, region to verify); record payments, no online payments; no WhatsApp sending, no web push, no return-visit nudge; patients see the current medicine course with history on request; patients may request an extra consultation, clinic approves; Documents is its own tab; upload types PDF, JPG, PNG, HEIC up to 15 MB; patient sign-in by emailed link or code; email through Resend. Full register: `docs/parked-decisions.md`.

## Draft core versus customizable split (to confirm)
Core: sign-in and roles, clinic isolation, patient record and episodes, documents, notifications, audit log, the six journey phases.
Customizable per clinic: branding, terminology, check-in questions, flag rules, structured clinical fields, diet and medicine templates, follow-up schedules, information pack content. Open question: whether a clinic may rename or skip phases (recommended: no for now).

## Build order
Foundation, then Arrival and Care, then Enquiry, Assessment, Planning, then Continuity. Walking skeleton first.

## Source material
`docs/brd.md`, `docs/prd.md`, `docs/architecture.md`, `docs/architecture-review.md`, `docs/parked-decisions.md`, `docs/source/Ayurveda_Journey_App_MASTER.md`, `docs/ux/mockups.html`.
