# PRD Quality Review — AyurSaathi (prototype PRD, 2026-10-22)

Reviewed: `prd.md`, `addendum.md`; checked against `docs/parked-decisions.md` (Part A and Part B) and `briefs/brief-AyurSaathi-2026-10-21/brief.md`.
Stakes calibration: prototype on invented data, sole decision-maker, acceptance = (1) demo journey works, (2) isolation proven by tests. Rigor is judged against that, not against a pilot or production bar.

## Overall verdict
The PRD has a clear thesis, honest non-goals, a strong isolation story (FR-4 to FR-6, SM-2, SM-C1) and contiguous FR numbering, FR-1 to FR-46. It is usable for architecture and stories now. Three things put it at risk. (1) Several unconfirmed Part B proposals and invented parameters appear as plain requirements, and the Assumptions Index does not match the inline tags. (2) Role ownership is inconsistent: UJ-3 has the Doctor changing Flag Rules while FR-8 gives that to Admin, and many FRs say only "Staff". (3) Testability is uneven. About six FRs have no consequences, and SM-1 claims to validate all 46 FRs although the five UJs do not exercise several of them. Gate: PASS WITH FIXES. None of the issues blocks starting architecture, but the high findings should be fixed before epics and stories are cut.

## Decision-readiness — adequate
Decisions are mostly stated as decisions, with sources named (PK-nn on the open questions). The `[NOTE FOR PM]` callouts are real: the core/custom split and the visa tracker and patient rights tools as likely first additions. Open Questions 1 to 7 are genuinely open and each names its spike or PK. Q8 ("which core features can a Clinic rename or skip") is half-answered in its own parenthesis ("Phases are fixed for now"), and the addendum says "Recommended: no". Either state the decision or leave it open, not both.
Trade-offs given up are named in places (SM-C2, "Screen polish"; deferring MFA and the audit log). The PRD does not say what is given up by making SM-1 cover all five journeys when the brief's acceptance journey is narrower (see Scope honesty).

### Findings
- **[medium]** Q8 is rhetorical (§9 Q8, addendum "Core versus per-clinic split") — an answer is given in the same line. *Fix:* record "Phases are fixed in the prototype" as a decision, and reduce the open item to "which Clinic Settings beyond labels, questions and rules".
- **[medium]** The "Gate before real patient data (all required)" list (§8) reads as decided, but PK-18 lists "the rule for when real patient data may be stored" as open, and the gate items audit log and MFA come from unconfirmed Part B (FR-ACC-06, FR-ACC-15, ADR-06, ADR-08). It is indexed as an assumption only under "§6.2", not tagged where it is stated. *Fix:* tag the gate `[ASSUMPTION: owner has not confirmed this list; PK-18 is open]` and index it.

## Substance over theater — strong
No persona theater: Anna, Meera, Dr. A and Marc each drive decisions (code fallback, copy-yesterday, flag-rule editing, skipping Enquiry). No innovation theater, and the Vision is honest about the clinic-specific context. NFRs are mostly product-specific (UTC storage, no health data in logs, service key only server-side). The "Responsive" NFR ("every task on phone or laptop with the same data") is an adjective without a check. The Counter-metrics (SM-C1, SM-C2) are real and not furniture.

### Findings
- **[low]** NFR "Responsive" (§8) has no testable form. *Fix:* name a pass condition, for example "each UJ-2 and UJ-3 path completes at 375 px width and at 1280 px width on the seeded build".

## Strategic coherence — strong
The thesis (one record, one place, replace channel-hunting for the post-quotation journey; do not replace first contact) carries through to scope and non-goals. The MVP kind is experience/proof, and the two success metrics map to the owner's two acceptance criteria. SM-3 (a written pilot-readiness list) is a sensible non-numeric metric, consistent with the brief's "numeric targets wait for baseline".

### Findings
- **[medium]** SM-1 widens the owner's acceptance (§7 SM-1). The brief's criterion 1 is the sign-in, onboard, invite, flight and pickup, day plan, check-in, doctor review path. The PRD makes UJ-1 to UJ-5 all required (adds the returning patient UJ-5, follow-up and extra Consultation UJ-4) and says it "Validates FR-1 to FR-46". The owner scoped this, so it is not wrong, but it is not stated as a deliberate widening. *Fix:* add one line in SM-1 or §6.1: "UJ-5 and UJ-4 extend the brief's journey (rationale: Continuity and Episodes are in scope)", or mark SM-1 primary on UJ-1 to UJ-3 and the rest secondary.

## Done-ness clarity — thin
Most FRs have concrete consequences (FR-13 field rules, FR-17 size and message, FR-36 ranges, FR-41 idempotence). Gaps:
- **No consequences at all:** FR-27 Accommodation, FR-28 Arrival-day card, FR-34 Record daily treatments given, FR-40 Log departure assistance, FR-43 Log Consultations (FR-12, FR-20, FR-22, FR-24 have only one weak or negative consequence).
- **Unbounded or missing parameters:** FR-2 "used or expired link" gives no expiry duration; FR-46 "retried" gives no retry count or interval; FR-7 "use it on a laptop browser" has no check; FR-35 "a way to tick medicines taken" does not say where it is shown; FR-32 "can request history, shown on request" does not say what the request is.
- **Role ambiguity weakens tests:** FR-9, 10, 11, 13 to 15, 20 to 27, 30, 33, 34, 40 and 43 say "Staff", but the Glossary splits Staff into Coordinator, Doctor and Admin and FR-3 only gives two example restrictions. A tester cannot tell whether a Doctor may log a Quotation or an Admin may publish a Day Plan. The addendum points to `docs/architecture.md`, whose authorisation matrix is itself unconfirmed (Part B ADR-04).
- **Acceptance seed missing:** SM-1 requires a "clean seed", and FR-4 to FR-6 require two Clinics and Patients A and B, but no FR or constraint specifies the demo seed (invented data set, two Clinics, one test-only). Both acceptance criteria depend on it.

### Findings
- **[high]** FRs without a testable consequence (§4.5 FR-27, FR-28; §4.6 FR-34; §4.7 FR-40, FR-43) — you said every FR must be testable and these are not. *Fix:* add at least one consequence each, for example FR-27 "a Patient sees accommodation of own Episode only; fields: property, room, check-in date"; FR-28 "card shows flight number, driver name, stay name; is absent before an Episode has pickup or stay entered, with an empty-state message"; FR-34 "a treatment-given record stores treatment, date, who recorded it; visible to Staff only unless in a Published Day Plan"; FR-40/43 field lists.
- **[high]** Role responsibility is not defined for "Staff" FRs (§4.2 to §4.7). *Fix:* add a compact role-by-capability table (or per-FR role) in the PRD or addendum, and say Doctor/Coordinator/Admin per FR. Align "Doctor and Staff" in FR-22 and FR-43 (Doctor is Staff by the Glossary, so the phrase is redundant or means "Doctor and Coordinator").
- **[medium]** Missing demo seed requirement (§4.1, §7). *Fix:* add an FR or §8 constraint: "A seed script creates invented data: two Clinics (Ayurvedgram plus one test-only Clinic), N Patients with Episodes in each Phase, one user per role." Reconcile with §5 and FR-8, which call only one Clinic live and only Ayurvedgram seeded.
- **[medium]** Unbounded parameters (FR-2 link expiry, FR-46 retry policy, FR-7). *Fix:* state values or mark `[ASSUMPTION]` with a default (for example link valid 15 minutes, 3 retries).

## Scope honesty — adequate
Non-Goals and §6.2 are explicit and mostly match Part A and the brief (PK-03, 06, 07, 08, 16, 17, 23; no web push; no WhatsApp). The `[ASSUMPTION]` machinery exists, but it is incomplete (see Mechanical notes). More important, several items that Part B lists as unconfirmed are written as firm requirements with no flag:
- FR-9 needs-attention block and alerts (FR-ACC-08; the alert types are new), FR-10/11 episodes and moves (FR-ACC-16/17), FR-14 draft (FR-ONB-06), FR-15 duplicate warning (FR-ONB-09), FR-29/30 landed, help and flight-edit alerts (FR-ARR-05/06), FR-33 copy-yesterday and publish (FR-CAR-12), FR-37/39 queue and combined review (FR-CAR-09), FR-26 Pickup fields, FR-23 Programme status values (FR-PLN-02).
- The invented validation values: the 60-second link re-request limit (FR-2), the "airline code plus number" format (FR-25), the 1,000-character free text and scores 1 to 5 (FR-36), the exact error message (FR-17). The validation rules in architecture section 8.4 are listed as unconfirmed.
Section 6.1's assumption ("clinic home, patient home, Documents tab, episodes and phase moves are in because the journey cannot be walked without them") covers FR-9 to FR-12, FR-18 only; the others are not covered. The owner scoped the prototype as end-to-end, and the brief lists the same capability areas, so including them is defensible, but the Rule for BMAD agents says "flag the default in the PRD".

### Findings
- **[high]** Unconfirmed Part B items and invented parameters are stated as plain requirements without a flag (§4.2 FR-9 to FR-11; §4.3 FR-14, FR-15; §4.5 FR-29, FR-30; §4.6 FR-33, FR-37, FR-39; FR-2, FR-25, FR-36). *Fix:* add one scoping rule to §0 or §6.1 ("Capability areas listed in the brief are in scope; their field lists, limits and message texts are prototype defaults, not owner-confirmed, Part B of `parked-decisions.md`"), and tag the invented numeric parameters inline `[ASSUMPTION]` and index them. Do not tag every FR.
- **[medium]** PK-09's working default is "None" and "the app applies only the doctor's rules", but FR-38 ships a Sample Flag Rule set (§4.6 FR-38). It is labelled "sample, not clinical", which is acceptable, but the assumption is in the Index only and not tagged at the FR. *Fix:* add the inline `[ASSUMPTION: sample rules exist only so the demo can show a queue; the PK-09 default is none]`. The same applies to the "five questions" default of PK-14 (already tagged in FR-36, good).
- **[medium]** FR-24 Payments, FR-44 Consultation Request, FR-15 are not in the brief's In list, though payments logging is covered by PK-06 and requests by PK-15 (both resolved). *Fix:* none needed beyond noting the source in the PRD (add "PK-06" and "PK-15" in the feature notes) so a reader does not read them as new scope.

## Downstream usability — adequate
FR IDs are unique and contiguous (FR-1 to FR-46); SM IDs are SM-1 to SM-3, SM-C1, SM-C2 with resolving references (FR-29 to FR-9 resolves). UJs each have a named protagonist, context, entry state, climax and edge case. Weaknesses are traceability and glossary use.

UJ to FR coverage: FR-20, FR-21, FR-23, FR-24 (Enquiry, Quotation, Programme, payments) and FR-34, FR-40 are realized by no UJ. UJ-1 states the quotation was accepted by WhatsApp but no journey logs it. FR-4 to FR-6 and FR-8 have no "Realizes" line (acceptable, since SM-2 covers them). UJ-2 combines onboarding and day-plan publishing in one journey and so reads as two. Several UJ details are not backed by an FR: the Patient timezone is "stored" (§8) but no FR captures it; UJ-4's "different time zone" depends on that.

Glossary use (see Mechanical notes for drift) is a real problem for source extraction: several domain nouns are used as if defined but are not in the Glossary.

### Findings
- **[high]** Glossary does not cover nouns that FRs and UJs rely on: alert, needs-attention block, Notification and inbox, Flight details, Pickup, Accommodation, Medicine/Prescribed medication, Treatment, Findings, Assessment (a Phase and a logged record), Payment, Draft (only defined inside Day Plan), clinic area, Patient home. *Fix:* add entries for at least Alert, Needs-attention block, Notification, Assessment (log vs Phase), Medicine, Pickup, Accommodation, Payment, and define Shared/Private visibility once, applying to Note, Document and assessment (the Glossary defines visibility only for Note and Document, but FR-22 applies it to assessments).
- **[medium]** Patient time zone has no capture FR (§8 NFR Time, UJ-4 edge case, FR-25, FR-41). *Fix:* add to FR-13 optional "time zone (defaults from nationality/browser)", or an FR "Patient time zone", with a consequence ("Times in the Patient views use the stored zone").
- **[medium]** Four FR groups are not exercised by any UJ, while SM-1 says it validates FR-1 to FR-46 (§7). *Fix:* either add steps to UJ-2 (log enquiry, Quotation, Programme, payment) and UJ-3/UJ-4 (treatments given, departure assistance), or restate SM-1's "Validates" to the FRs the UJs actually cover and say the remainder are validated by acceptance tests.

## Shape fit — adequate
Consumer-grade patient app with several roles and an older, non-technical primary patient: UJ with named protagonists is the right shape, and five UJs is proportionate. As a chain-top PRD (feeds UX, architecture, stories) the traceability bar is higher than the PRD currently meets, which is why the findings above matter. Nothing is over-formalized; the amount of process is right for the stakes. Section 4's per-feature "Description" blocks do carry UX-ish detail (for example the Phase tag, the six-step bar), which is acceptable here because the mockups exist.

## Specific checks requested
- **FR numbering stable:** yes. FR-1 to FR-46 contiguous, no duplicates, IDs not reused. To keep stable when adding the missing FRs above (seed, time zone), append as FR-47 and up rather than inserting.
- **Decided Part A items contradicted:** no direct contradiction found. Checked PK-02, 03, 05, 06, 07, 08, 12, 13, 15, 16, 17, 22, 23, 26, 27 against §4, §6.2, §8 and the addendum; all consistent. Two near-misses: (a) PK-09 default "None" vs FR-38 Sample Flag Rules, which is a flagged working default but not tagged inline (above); (b) PK-27 says HEIC "converted on upload" is decided and only the approach is open, whereas FR-17 tags the whole conversion as an `[ASSUMPTION]` and picks the target format "JPEG", which is invented. *Fix:* make the conversion a plain requirement; tag only "JPEG" and the method.
- **Role contradiction:** UJ-3 edge case has Dr. A changing the Flag Rule in settings, but FR-8 and the Glossary (Admin manages Clinic Settings) give that to Admin. *Fix:* decide who may edit Flag Rules (Doctor defines flags per BR-06 and PK-09, so likely Doctor, with Admin able to as well), then change FR-8, the Admin glossary entry and UJ-3 to agree. **[high]**, because it is a permission conflict that tests would encode.
- **Unconfirmed item silently became a requirement:** yes, see Scope honesty (high). No Part B item that the owner explicitly parked as out (visa tracker, message thread, patient rights, supply tracker, feedback form, nudge, trend view, therapy record per session, second transfer leg) was added; §6.2 lists them correctly.
- **FR uses Glossary terms exactly:** mostly. Drift listed below.

## Mechanical notes
- **Broken cross-reference:** §0 says assumptions are "indexed in section 9", but section 9 is Open Questions; the Assumptions Index is section 10. Fix the reference.
- **Assumptions Index roundtrip fails:** index has 7 entries; inline tags exist only for FR-16, FR-17, FR-36. Index entries for FR-38, §6.1, §6.2 and §8 have no inline tag (FR-8's note is a `[NOTE FOR PM]`, not an `[ASSUMPTION]`). §0 claims "every assumption is tagged inline", which is false. Also the invented parameters named under Scope honesty are not indexed at all.
- **Glossary drift:**
  - "Staff-only" (FR-5, FR-17) vs "Staff only" (Glossary: Note, Document).
  - "Doctor Notes" (FR-3) vs Note.
  - "Clinic Setting" (Flag Rule entry) vs "Clinic Settings".
  - "Queue" and "Review Queue" mixed.
  - "Day view" (FR-35) vs "Day Plan" vs "Patient home".
  - "Staff user" (FR-9, FR-1 "Staff account").
  - "service key" in FR-8 NFR and §8 "service key"; the Glossary has no entry.
  - "Doctor and Staff" (FR-22, FR-43), as Doctor is Staff.
  - "Patient's local time" vs "viewer's local time" (FR-25).
  - "Shared assessments" (FR-22): assessments have visibility but are not in the Glossary visibility definition.
- **Phase naming:** Glossary Phase list is Enquiry, Assessment, Planning, Arrival, Care, Continuity; the vision uses "follow-up" for Continuity. Acceptable, but use "Continuity" once with "follow-up" in brackets.
- **Section 4.1 title mentions "Access, roles and clinic isolation"** but FR-7 (installable app) and FR-8 (Clinic Settings) are not about those; move them or rename the feature.
- **UJ protagonists:** all five named with context inline. UJ-5 (Marc) has no edge case, unlike the others; low.
- **Open-items density:** 9 Open Questions, 3 inline `[ASSUMPTION]`, 2 `[NOTE FOR PM]` for a prototype PRD. Appropriate for the stakes; the issue is not too many open items but unflagged defaults.
- **Required sections:** present (vision, users, glossary, features, non-goals, scope, metrics, NFRs, open questions, assumptions). No Dependencies/Risks section; the brief has one (sponsor not engaged, legal review, no older-user testing). Acceptable for a prototype, but add two lines or point to the brief.
