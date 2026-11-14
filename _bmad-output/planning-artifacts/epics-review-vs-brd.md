# Self-review of the epics and stories against the BRD

Reviewed: `_bmad-output/planning-artifacts/epics.md` (9 epics, 66 stories) against `docs/brd.md`, with the PRD, architecture spine and UX spines as cross-checks. Reviewer: the author of the stories, so treat this as a first pass, not an independent review. Date 2026-11-14.

## 1. Method
1. Every BRD functional requirement (80 rows), business rule (BR-01 to BR-12), non-functional requirement (NFR-01 to NFR-15) and constraint was mapped to a story or to a stated exclusion.
2. A script checked that every PRD requirement (FR-1 to FR-48), architecture requirement (AR1 to AR26), UX requirement (UX-DR1 to UX-DR28) and NFR1 to NFR8 is referenced by at least one story, that no template placeholder remains, that every story has the user-story lines and Given, When, Then criteria, and that no story depends on a later one.
3. The BMAD step-4 validation checks were walked by hand: starter-template story first, tables created only when needed, story sizing, epic independence and file churn.

## 2. Result in one paragraph
All 32 BRD requirements the owner decided (the 28 marked DECIDED and the 4 decided in part) have at least one story. The mechanical checks pass after fixes. The review found 11 problems in my own first draft, all fixed (section 4). Eight questions remain for the owner (section 5).

## 3. BRD coverage
### 3.1 Decided requirements, all covered
| BRD | Story |
|---|---|
| FR-ACC-01, 02 | 1.5, 1.12, 3.6 |
| FR-ACC-07 | 1.8 |
| FR-ONB-01, 02, 03 | 2.2 |
| FR-ONB-04 | 7.1, 7.3, 7.5 |
| FR-ONB-08 | 2.5 |
| FR-ENQ-01, 02, 06 | 8.1, 8.2, 2.7 |
| FR-ASM-01, 02 | 8.3 |
| FR-PLN-01, 07 | 8.4, 8.5 |
| FR-ARR-01, 02, 03 | 4.1, 4.2, 4.3 |
| FR-CAR-01, 02 | 5.1 |
| FR-CAR-03 | 5.2 |
| FR-CAR-04 | 5.5 |
| FR-CAR-05, 06 | 5.3 |
| FR-CAR-07 | 5.6 |
| FR-CAR-08 | 6.1 |
| FR-CON-01 | 9.1 |
| FR-CON-02, 03 | 9.3, 9.2 |
| FR-CON-04 | 9.4 |
| FR-CON-05 | 2.7 |
| FR-CON-11 | 9.5 |

### 3.2 Proposed requirements the owner chose for the prototype, all covered
Draft, invite and duplicate warning (FR-ONB-06, 07, 09) in 2.3, 3.5, 2.4; arrival card, landed and help buttons, flight-edit alert (FR-ARR-04, 05, 06) in 4.4, 4.5, 4.6; review queue, shared and staff-only notes, copy yesterday (FR-CAR-09, 11, 12) in 6.3, 5.1, 5.4; patient list and home screens (FR-ACC-08, 09) in 2.1, 3.7; document store (FR-ACC-10) in Epic 7; inbox and email (FR-ACC-11) in 3.1, 3.3; phase moves and episodes (FR-ACC-16, 17) in 2.6, 2.7; patient sees only their own record (FR-ACC-05) in every table story; therapy record (FR-CAR-13) in 5.5; patient sees shared assessment outcome (FR-ASM-05) in 8.3; plan status (FR-PLN-02) in 8.4.

### 3.3 Proposed requirements deliberately left out of the prototype
| BRD item | Reason |
|---|---|
| FR-ACC-06 audit log, FR-ACC-15 staff MFA, BR-07 | Owner decision: gate before real data. Not blocked: AR22 and Story 1.2 keep the design ready. |
| FR-ACC-13 patient rights tools (export, correct, erase) | Needs legal advice (PK-18). Added to the real-data gate in the PRD and architecture during this review. |
| FR-ACC-12 message thread, FR-ACC-18 WhatsApp sending | Owner decisions. |
| FR-ACC-03, 04 therapist, kitchen and attendant access | Owner decisions (PK-03, PK-17). |
| FR-ENQ-03, 04, 05 | Source, lead list and patient view of enquiries: not in the PRD. |
| FR-ASM-03, 04 | Clinical fields wait for the Doctor (PK-10); medicines from assessment not in the PRD. |
| FR-PLN-03, 04, 05, 06 | Checklist, visa tracker, information pack, question thread: not in the PRD (visa tracker and rights tools are the likely first pilot additions). |
| FR-ARR-07 | Second transfer leg: not in the PRD. |
| FR-CAR-10 | Flag rules are configurable and sample-labelled (6.2, 6.5); the real rules wait for the Doctor (PK-09). |
| FR-CON-06 | Follow-up templates wait for the Doctor (PK-11); free scheduling in 9.2. |
| FR-CON-07, 08, 09, 10, 12 | Supply tracker, return nudge (owner: off), feedback form, handover, trend view: not in the PRD. |

### 3.4 Business rules
BR-01 (8 intro, 4.5); BR-02 (patient writes: flight, check-ins, uploads, plus medicine ticks and consultation requests, noted below); BR-03 (9.2, 9.3); BR-04 (2.7, 8.1); BR-05 (8.4); BR-06 (5.x, 6.2, 6.4, 9.5 safety copy); BR-07 deferred; BR-08 (1.9, demo ribbon 1.3); BR-09 (real-data gate, seed guard 1.9); BR-10 not applicable to the prototype; BR-11 (1.4, 1.7); BR-12 (every staff story, NFR2).

### 3.5 BRD non-functional requirements
| NFR | Status |
|---|---|
| 01 usability, 02 accessibility | UX-DR2, UX-DR23 in 1.3 and the patient stories |
| 03 performance | Added in this review: 1.6 (about 3 seconds) and 6.1 (check-in under a minute) |
| 04 availability, 09 backup | Parked (PK-24); in the real-data gate |
| 05 security | AR3 to AR17, Epics 1 and 3 |
| 06 privacy | Isolation suite, 1.4, Epic 7; consent 2.5 |
| 07 auditability | Deferred (gate) |
| 08 data location | Spike 1.10 |
| 10 observability | Added in this review: health check in 1.1, no-PHI logging in 1.2, error reference in 1.3 |
| 11 maintainability | 1.2, 1.13 |
| 12 browser support | Added in this review: 4.7 runs three browsers |
| 13 installability | 1.8 |
| 14 localisation readiness | 1.3 |
| 15 time handling | 2.8 |

## 4. Problems found in my first draft and fixed
| # | Problem | Fix |
|---|---|---|
| 1 | No story created staff accounts, though the UX spec has a People screen and AR6 names user administration | New Story 1.12 |
| 2 | No story built the per-clinic release routine or `clinics.json` workflow (AR19) | New Story 1.13 |
| 3 | AR2 (toolchain pins) and AR22 (audit-ready conventions) had no story | Added to Stories 1.1 and 1.2 |
| 4 | No criterion for "no health data in logs" (NFR5) or for a safe error message | Added to Stories 1.2 and 1.3 |
| 5 | BRD performance, health check and browser support had no criteria | Added to 1.1, 1.6, 4.7, 6.1 |
| 6 | Sign-out and theme choice were not specified for staff or patients | Added to 1.5, 1.6, 3.7 |
| 7 | Story 1.4 needed claim helper functions created in the later Story 1.5 | Helpers moved to 1.4; test helpers set claims directly in 1.2 |
| 8 | Story 1.6 promised More items whose screens arrive in later stories | Reworded so each later story adds its item |
| 9 | Story 9.4 linked to a table from the later Story 9.5 | Optional field left empty and filled in 9.5 |
| 10 | The UX flow gave findings and outcome separate visibility; the PRD gives one setting | UX flow corrected |
| 11 | Patient rights tools (BRD "Must") were missing from the real-data gate | Added to the PRD and architecture gate lists |
| + | Added AR26, a definition of done every story follows | New requirement |

## 5. Open questions for the owner
1. **Edit a patient's details.** Nothing lets staff correct a typo after creation. Not in the PRD. Add a story to Epic 2?
2. **Admin access to Staff-only notes.** Epic 5 assumes Admin reads Shared notes only.
3. **Patient view of the programme, quotations and payments.** Epic 8 keeps them staff-only because the PRD gives the patient no view. The BRD's proposed FR-ENQ-05 would show enquiries and quotations read-only.
4. **Quotation inclusions and exclusions.** The BRD lists them as proposed fields. The PRD and Story 8.2 omit them.
5. **Invite validity of 24 hours** and **sign-in link validity of one hour** are assumptions.
6. **Phase moves are offered after each log, not automatic** (8.1, 8.3, 8.4, 9.1). The PRD's UJ-6 says each step "moves the Episode". Confirm offered is acceptable.
7. **Large stories to split at sprint planning if needed:** 1.2 (CI, harness and three checks), 3.5 and 3.6 (invites and redemption), 6.1 (check-in table and flow).
8. **BRD items in 3.3 above** the owner may want back in the prototype, in particular the visa tracker and the checklist.

## 6. What this review cannot tell you
It was written by the same author as the stories, so it will share my blind spots. The clinical content (flag rules, check-in questions) and the legal gate depend on a doctor and a lawyer. Sizing is judged from the criteria, not from a build.
