# Independent review of epics.md

Date 2026-11-14. Reviewed: `_bmad-output/planning-artifacts/epics.md` (9 epics, 66 stories). Method: BMAD `bmad-review`, two lenses run as independent subagents with no sight of the author's self-review: **adversarial** (46 findings, A1 to A46) and **edge-case hunter** (about 130 findings, E). Verification-gap was not run: it needs code and tests, and none exist yet. Findings carry no severity, by the skill's rule. Where both lenses found the same problem it is listed once with both references; overlap means the weakness is real.

## Themes

### T1. Patients cannot see what the stories say they see
- No patient screen shows Shared Notes or Shared Assessments; Plan (5.6) shows only schedule, meals and medicines, yet 5.1 notifies "Your doctor added a note", 6.4 and 8.3 assert the patient sees them, and the UJ-3 climax depends on it. (A8; E 8.3)
- "Today card shows what matters now" (3.7) has no rule per phase, so it cannot be tested. (A41; E)
- Today's arrivals, plans to publish and check-ins-to-review count (UX spine) are built by no story. Patient list badges other than "Nothing due" are never added. (A42; E 2.1)

### T2. Row-level security cannot hide columns
- A Shared assessment row exposes `findings` to the patient through the API. (A9; E 8.3)
- "Patient cannot read the flags column" (6.2) and "cannot read treatments-given notes" (5.5) cannot be met with row-level security, because patients and staff share one database role. Use staff-only tables or patient views without the column. (A10; E 6.2)

### T3. Direct table writes bypass the rules
- Patients could update their own `check_ins` row to clear flags or set reviewed; submission must be a function. (A11)
- A patient flight edit through the API skips the server action and its alert; "who changed it" can be forged. Use a trigger or `update_flight` function and a WITH CHECK that pins episode and clinic. (A16; E 4.1)
- A patient soft-deleting a document needs UPDATE, which also lets them change visibility or path. (A22)
- A patient can insert a consultation request already "approved". (A23)

### T4. Notification and alert plumbing contradicts itself
- `emit_event` "invoker or definer with EXECUTE revoked" is unworkable both ways: invoker lets patients forge notifications to any user; definer-revoked blocks the server actions. Name its allowed callers. (A14; E)
- Repeated `dedupe_key` is a no-op (3.1), yet 4.6 needs the alert updated with the latest change. (A15; E)
- One dedupe key across a role fan-out delivers to only the first recipient; key must include the recipient. Patient events before an account exists are undefined. (E)
- Fan-out to disabled users or to a role with no active users. (E)

### T5. Invites and sign-in
- The patient account and role are created at Send invite, so anyone with that mailbox can sign in through the ordinary link flow without redeeming; no way to revoke a mistaken invite or disable a patient. (A19; E)
- The raw invite token and code would sit in `notifications.payload`, defeating hashed tokens. (A18)
- "Clinic and role from the invite row" is circular when the same call creates the row. (A20)
- Invite expiry 24 hours (3.5) against one hour (3.6, PRD FR-2). (E)
- A staff email entered on the patient code screen gives staff passwordless sign-in. Staff and patient sharing an email collides. (E)
- No staff password reset. Redemption while another user is signed in. Session-expired return to page has no criterion. (E)

### T6. Email delivery timing and safety
- The hourly sender delays invites, one-hour codes and "I need help" by up to an hour; end-to-end tests become flaky. Send immediately; keep hourly as the retry sweep. (A17; E)
- Overlapping or crashed sender runs send duplicates (needs row claiming). Sender must re-check recipient and address at send time. (E)
- "No health content" is stated only for patient emails; staff alert emails could carry names and flag reasons. (A37)

### T7. The role table is applied inconsistently
- Doctor given write on flights, pickups and stays (4.1 to 4.3) and on enquiry, quotations, programme and payments (8.x); the PRD role table says read. 8.4's "Doctor refines programme" follows BR-05 but contradicts the PRD table. (A4, A5; E 8.4)
- Coordinator should see Clinical rules read-only (UX), the story hides it. (A6; E)
- Admin reads Shared notes only (5.1) contradicts the PRD and UX; Admin access to assessments unspecified. (A7; E)
- The capability matrix is never created and a JSON file cannot drive policies at runtime. (A3)
- Coordinator review pane must show Shared notes only. (A36) Coordinator can type medicine plan items, sidestepping the prescribing rule. (A25; E)

### T8. Episode lifecycle is undefined
- No rule for closing an episode, at most one open episode, or which episode patient screens use; journey bar for a patient with none open. (A31; E)
- Episodes created in 2.2 before `phase_events` exists (2.6); 2.7 says "starts through move_phase", but creating is not moving. Needs `start_episode`. (A32; E)
- Concurrent phase moves: last writer wins silently; use expected-phase and `conflict`. Moving to the same phase or a closed episode. Effects of moving back (check-ins, schedules). (A33; E)

### T9. Check-in model
- Unique key including the questions version allows two daily check-ins when the Doctor edits questions mid-day. (A12; E)
- Patient-triggered creation contradicts the hourly job and the rule that scheduled functions take no client parameters. Missed check-ins are invisible. (A13; E)
- Window opens 06:00 in the patient's home zone while they are physically in Pune. (E)
- "Question 1 of 5" fixed though questions are editable; 08:00 example conflicts with 06:00. (E; A40)
- Follow-up question set (with diet issue) is never seeded or editable. (A46; E)
- Send while offline, mid-flow resume, evaluation errors aborting submission, rule version not stored. (E)

### T10. Medicines and Day Plans
- The medicine-change function 6.4 relies on is never defined; end-and-create needs one transaction. No stop-medicine action. Concurrent changes fork a course. (A26; E)
- Medicine schedule format and slots undefined, so Taken toggles cannot be derived; intake uniqueness and patient undo of staff entries. (A27; E)
- Editing a published plan shows unpublished drafts to the patient; needs draft revisions. No unpublish. Copy-yesterday with no plan or with ended medicines. (A24; E)

### T11. Documents and uploads
- "Row created only after upload" cannot work with storage policies that join to the row; signed upload URLs would need the service key; orphan files. Create a pending row first. (A21; E)
- Several files at once (BRD FR-ONB-04, DECIDED) not covered. (E)
- Phone photos keep EXIF GPS location. Patient photo at onboarding has no storage rule. (E)
- A patient's own upload switched to Staff-only disappears from them; patient removal of a clinically relevant file. (E)

### T12. Time zones
- Flight arrival time interpreted in the patient's home zone instead of the arrival airport's: pickup hours off. (E)
- DST gaps and repeats; multi-zone nationalities pre-selecting a wrong zone; stay times and medicine end dates with no zone. (E)
- "Pune" hard-coded in the time format. (A28; E)

### T13. Clinic-agnostic rule BR-11 (decided)
- Phase names are not configurable. (A28; E)
- Clinic phone (used in all safety copy) and default time zone are never stored or editable. (A29)

### T14. Missing stories
- Edit patient details (A30; E); delete or merge a mistaken patient (E); revoke patient access (A19; E); staff password reset (E); withdraw consent and re-consent on new wording (E); daily stay changes, BRD FR-CAR-06 decided (A43); programme status history (A45); automated accessibility checks (A44).

### T15. Forward dependencies and false claims
- 1.5 tests notes and medicines tables (Epic 5), sign-out under More (1.6) and cache clearing (1.8). (A1, A2; E)
- 1.6 shows Patients, Review and Plans before those screens exist; Admin's bottom bar undefined. (E)
- 2.2 refers to a review step that appears in 2.5. 3.4 applies limits to endpoints from 3.5 and 7.1. (E; A34)
- 4.7 claims FR-1 to FR-30, including Epics 7 and 8 work. (A35; E)

### T16. Untestable or oversized
- Untestable: 1.2 lint rules, "under a minute" measured by a robot, 3.3 "increasing delay", 4.6 "short window", 6.5 "within limits", seed re-run semantics. (A38, A40; E)
- Too large for one session: 1.2, 3.3, 3.5, 3.6, 7.1. (A38, A39; E)
- Release routine partial failure leaves clinic A migrated and clinic B not. (E)

## Full findings
The complete lens outputs (A1 to A46 and every edge-case item, with location, trigger, fix and consequence) are preserved in the session record and reproduced in the themes above by reference. Each will be addressed or explicitly rejected in the fix pass, with the outcome logged.
