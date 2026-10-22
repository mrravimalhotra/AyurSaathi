# Addendum: AyurSaathi product brief

Detail that belongs downstream (PRD, architecture), not in the brief.

## Decisions already made
See `docs/parked-decisions.md` Part A (items marked Resolved) for every owner decision to date. That register is the source of truth.

## Draft core versus customizable split (to confirm)
Core: sign-in and roles, clinic isolation, patient record and episodes, documents, notifications, audit log, the six journey phases.
Customizable per clinic: branding, terminology, check-in questions, flag rules, structured clinical fields, diet and medicine templates, follow-up schedules, information pack content. Open question: whether a clinic may rename or skip phases (recommended: no for now).

## Build order
Foundation, then Arrival and Care, then Enquiry, Assessment, Planning, then Continuity. Walking skeleton first.

## Source material
`docs/brd.md`, `docs/prd.md`, `docs/architecture.md`, `docs/architecture-review.md`, `docs/parked-decisions.md`, `docs/source/Ayurveda_Journey_App_MASTER.md`, `docs/ux/mockups.html`.
