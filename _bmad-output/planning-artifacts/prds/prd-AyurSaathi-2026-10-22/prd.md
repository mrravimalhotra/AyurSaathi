---
title: "PRD: AyurSaathi"
status: draft
created: 2026-10-22
updated: 2026-10-22
---

# PRD: AyurSaathi
*Working title. Confirm.*

## 0. Document Purpose

This PRD defines an end-to-end working prototype of AyurSaathi for Ravi (product owner and sole decision-maker) and for the downstream BMAD steps: UX, architecture, epics and stories, and build. It builds on the finalized product brief (`_bmad-output/planning-artifacts/briefs/brief-AyurSaathi-2026-10-21/`) and on the earlier planning set in `docs/` (`brd.md`, `architecture.md`, `architecture-review.md`, `parked-decisions.md`, `ux/mockups.html`). It does not duplicate them. Technical choices are in `addendum.md`. Vocabulary is anchored in the Glossary; features group the functional requirements (FR-n, numbered globally); every assumption is tagged inline and indexed in section 10.

**Scoping rule:** some requirements below come from candidate items the owner has not formally confirmed (the register's Part B). They are in this PRD only because the owner chose them for the prototype or because the journey cannot be walked without them. They are prototype defaults, not confirmed product requirements, and every invented parameter (limits, timings, formats) carries an inline `[ASSUMPTION]` tag.

**Scope of this PRD:** an end-to-end working prototype on invented data. It is not rolled out to users. Finer details, WhatsApp setup and email provider configuration come later.

## 1. Vision

AyurSaathi is a web app, installable on a phone's home screen, that runs the international patient journey for an Ayurvedic clinic: enquiry, assessment, planning, arrival, care and follow-up, on one shared patient record that lasts across visits. Staff and doctors work in a clinic area. Patients see their own plan, travel details and check-ins.

Today that journey runs over WhatsApp, email and phone, so records are scattered, patients lose information and the clinic depends on individual inboxes. AyurSaathi gives each patient one place and gives the clinic one record. First contact, quotations and assessment calls stay on the existing channels. The app records the outcome and runs the structured parts.

The first clinic is Ayurvedgram, Pune. The product is a common core that every clinic shares, with each clinic's terminology, templates and clinical rules held as its own settings. Over time it becomes a platform on which several Ayurveda clinics run. The prototype exists so Ravi can see how the journey works end to end and decide whether to take it to Ayurvedgram.

## 2. Target User

### 2.1 Jobs To Be Done
- **Coordinator:** put a patient's flight, pickup, stay and daily plan in one place once, instead of repeating them on three channels.
- **Doctor:** see which patients need attention today, record notes and medicines, and review check-ins without leaving the screen.
- **Patient:** know what happens next without searching WhatsApp, email and calls, and report how I feel in under a minute.
- **Ravi (builder and decision-maker):** walk the whole journey on a real build and judge whether it is worth taking to the clinic.

### 2.2 Non-Users (v1)
Therapists and kitchen staff (the coordinator enters for them), attendants and companions, and other clinics. Real patients are not users of the prototype.

### 2.3 Key User Journeys

- **UJ-1. Anna opens her invite and sees her arrival.**
  - **Persona + context:** Anna, in her sixties, from Austria, not very technical, travelling to Pune for treatment. She has accepted a quotation by WhatsApp.
  - **Entry state:** Not signed in. On her phone, from an email.
  - **Path:** opens the invite link; if the link fails she types the code shown on the same screen; lands on the patient home with the six-step journey bar and a card for today; adds her flight number and arrival time; sees the car, driver and stay details the clinic has entered.
  - **Climax:** the arrival-day card shows her flight, who meets her and where she stays, in one place.
  - **Resolution:** on landing she taps "I have landed". The coordinator sees the alert.
  - **Edge case:** the link was opened by a mail scanner first and no longer works. Anna types the code instead and is signed in.

- **UJ-2. Meera onboards a patient and publishes tomorrow's plan.**
  - **Persona + context:** Meera, coordinator, on her phone between other tasks.
  - **Entry state:** Signed in as coordinator, in the clinic area.
  - **Path:** starts onboarding, enters name, email, phone and nationality; the consent step shows the sample text; she saves a draft when interrupted and resumes; uploads a passport photo from her phone; submits and the invite is sent. During care she opens a patient's day plan, copies yesterday's plan, changes two items and publishes it.
  - **Climax:** the patient's day view updates and the patient is notified.
  - **Resolution:** the plan shows as published with a time. Tomorrow starts from this plan.
  - **Edge case:** a patient with the same email already exists. The app warns and offers to open that record.

- **UJ-3. Dr. A reviews the morning's check-ins.**
  - **Persona + context:** Dr. A, on a laptop or phone, at the start of the day.
  - **Entry state:** Signed in as doctor.
  - **Path:** opens the review queue; flagged check-ins appear first with the reason; opens one, reads the answers, adds a note marked Shared or Staff-only, adjusts a medicine, marks the check-in reviewed.
  - **Climax:** the patient sees the shared note and the changed medicine on her next visit to the day view.
  - **Resolution:** the check-in leaves the queue. The Staff-only Note is visible only to Staff.
  - **Edge case:** the sample flag rule marks too many check-ins. Dr. A changes the rule in settings.

- **UJ-4. Anna, back home, answers a follow-up and asks for a call.**
  - **Persona + context:** Anna, two weeks after departure.
  - **Entry state:** Signed in by emailed link or code.
  - **Path:** sees a clinic-scheduled follow-up check-in; confirms the medicine, rates how she feels and flags a diet issue; submits; then requests an extra consultation with a preferred time.
  - **Climax:** the app confirms the check-in was received.
  - **Resolution:** the coordinator approves the request and logs the consultation after it takes place.
  - **Edge case:** she is in a different time zone. Times show in her local time.

- **UJ-6. Meera and Dr. A record the journey before and after treatment.**
  - **Persona + context:** Meera, coordinator, and Dr. A, in the days around Anna's visit.
  - **Entry state:** Signed in; Anna's Episode is in Enquiry.
  - **Path:** Meera logs the WhatsApp enquiry and the first Quotation; Dr. A logs the assessment call and its outcome; Meera records the Programme and the deposit received; after Anna's care, Meera records treatments given and logs her departure assistance.
  - **Climax:** Anna's whole history sits in one record.
  - **Resolution:** each step moves the Episode to the next Phase.

- **UJ-5. Marc returns for a second visit.**
  - **Persona + context:** Marc, treated last year, returning.
  - **Entry state:** Existing patient record, closed first episode.
  - **Path:** the coordinator opens Marc's record and starts a new episode at Assessment, skipping Enquiry; earlier documents and history are already there.
  - **Climax:** nothing is re-entered.
  - **Resolution:** the new episode moves through the phases independently of the first.

## 3. Glossary

- **Clinic** — an organisation that uses AyurSaathi. Owns its patients, staff, settings and data. Ayurvedgram, Pune is the first Clinic.
- **Clinic Settings** — per-Clinic configuration: name and branding, terminology labels, Check-in questions, Flag Rules, templates. Distinct from the shared core. Branding and terminology are edited by Admin; Check-in questions and Flag Rules by the Doctor.
- **Patient** — a person treated by a Clinic. One permanent record per Patient per Clinic.
- **Episode** — one visit or treatment cycle of a Patient. A Patient has many Episodes.
- **Phase** — one of six stages an Episode moves through: Enquiry, Assessment, Planning, Arrival, Care, Continuity.
- **Staff** — Coordinator, Doctor or Admin of a Clinic.
- **Coordinator** — Staff who enters logistics and daily plans.
- **Doctor** — Staff who records assessments, Notes and medicines, reviews Check-ins, and edits Flag Rules and Check-in questions. `[ASSUMPTION: the Doctor, not Admin, owns clinical rules, because the app applies only the doctor's rules.]`
- **Admin** — Staff who manages users and the branding and terminology parts of Clinic Settings.
- **Invite** — an email sent to a Patient with a single-use link and a code, used to sign in for the first time.
- **Quotation** — a priced offer for a programme, versioned within an Episode.
- **Programme** — the treatment plan and approximate cost settled before travel. Linked to an accepted Quotation.
- **Day Plan** — the schedule of treatments, meals, medicines and stay for one Patient on one date. Draft or Published.
- **Check-in** — a short set of questions a Patient answers: during Care (daily) or during Continuity (clinic-scheduled).
- **Flag** — a mark on a Check-in set by a Flag Rule.
- **Flag Rule** — a Clinic Setting that decides which Check-in answers raise a Flag. The prototype ships a Sample Flag Rule set.
- **Review Queue** — the Doctor's list of Check-ins awaiting review, Flagged first.
- **Note** — a Doctor's record, marked Shared (visible to the Patient) or Private (visible to Staff-only).
- **Visibility** — whether a Note, assessment or Document is Shared (visible to the Patient) or Staff-only (visible to Staff-only). Always written "Staff-only".
- **Assessment** (the logged record) — a Doctor's record of an assessment with date, method, findings and outcome. Not to be confused with the Assessment Phase.
- **Medicine** — a prescribed item with name, dose, schedule, start date and duration. "Current course" means the Medicines active today.
- **Pickup** — the car, driver, meeting point and time entered by Staff for a Patient's arrival.
- **Accommodation** — where a Patient stays, with check-in details, entered by Staff.
- **Payment** — a recorded amount received from a Patient (deposit, balance or other). Record only.
- **Alert** — an item in Staff's needs-attention block: an unreviewed Flagged Check-in, "I have landed", "I need help", a flight-detail edit, or a pending Consultation Request.
- **Notification** — a stored message to one user (in-app inbox), optionally also sent by email.
- **Consent** — a Patient's recorded agreement, versioned and timestamped, captured as step 2 of onboarding.
- **Consultation** — a Doctor's contact with a Patient by phone, WhatsApp or video, logged after it takes place.
- **Consultation Request** — a Patient's request for an extra Consultation. Approved or declined by the Clinic.
- **Document** — an uploaded or generated file attached to a Patient, with visibility Shared or Staff-only.

## 4. Features

### 4.1 Access, roles and clinic isolation
**Description:** One application for Staff and Patients. Staff sign in with email and password. Patients sign in with an emailed single-use link, or a code typed on the same screen. Every clinic-owned record belongs to a Clinic, and access is limited by Clinic first and role second. The prototype's proof of safety is an automated test suite, not manual checking. Realizes UJ-1, UJ-2, UJ-3.

**Who can do what (prototype).** Where an FR says "Staff", it means the roles in this table.

| Capability | Coordinator | Doctor | Admin |
|---|---|---|---|
| Onboard Patients, Invites, Documents | yes | yes | yes |
| Patient list, Episodes and Phase moves | yes | yes | yes |
| Log enquiry, Quotation, Programme, Payments | yes | read | yes |
| Log Assessment | no | yes | no |
| Flight, Pickup, Accommodation | yes | read | yes |
| Build and publish Day Plans; record treatments given | yes | yes | yes |
| Notes, findings, Medicines | no | yes | read |
| Review Queue and reviewing Check-ins | read | yes | read |
| Schedule follow-up Check-ins; departure assistance | yes | yes | yes |
| Log Consultations; decide Consultation Requests | yes | yes | yes |
| Check-in questions and Flag Rules | no | yes | no |
| Branding, terminology, users | no | no | yes |

`[ASSUMPTION: this role split is the prototype default, derived from the earlier authorisation matrix; confirm with the clinic.]`

**Functional Requirements:**

#### FR-1: Staff sign-in
Staff can sign in with email and password. Realizes UJ-2, UJ-3.

**Consequences (testable):**
- A Staff account with a wrong password is refused with a plain message.
- A signed-in Staff user lands in the clinic area for their role.

**Out of Scope:** multi-factor authentication (a gate before real data, see section 8).

#### FR-2: Patient sign-in by link or code
A Patient can sign in using an emailed single-use link, or a code typed on the same screen if the link fails. No password. Realizes UJ-1, UJ-4.

**Consequences (testable):**
- A used or expired link is refused; the code remains available.
- The link and code expire after a set period. `[ASSUMPTION: one hour, as the platform default; configurable.]`
- Re-requesting a link within a short window of the last request is refused with a message saying when to retry. `[ASSUMPTION: 60 seconds.]`

#### FR-3: Roles
The system can restrict each screen and action to Patient, Coordinator, Doctor or Admin. Realizes UJ-2, UJ-3.

**Consequences (testable):**
- A Patient cannot open any clinic-area route.
- A Coordinator cannot write Notes or prescribed medicines.

#### FR-4: Clinic isolation
Every clinic-owned record belongs to exactly one Clinic, and a user can read or write only records of their own Clinic.

**Consequences (testable):**
- With two seeded Clinics, Staff of Clinic X receive no rows of Clinic Y from any table.
- Document storage paths begin with the Clinic, and a file of Clinic Y cannot be fetched by Clinic X.

#### FR-5: Patient isolation
A Patient can read only their own record, Shared Notes and Shared Documents, and can write only their own flight details, Check-in answers, Consultation Requests and uploads.

**Consequences (testable):**
- Patient A cannot read any row of Patient B in any table.
- Patient A cannot read a Staff-only Note or Staff-only Document of their own record.

#### FR-6: Isolation test suite
The system can run an automated suite that exercises FR-4 and FR-5 against every clinic-owned table and the document store, as Patient A, Patient B, Staff of Clinic X and Staff of Clinic Y. This is the prototype's second acceptance criterion.

**Consequences (testable):**
- The suite lists every table and fails if a table has no isolation test.
- The suite fails the build when any cross-patient or cross-clinic read or write succeeds.

#### FR-7: Installable app
Staff and Patients can install the app on a phone home screen, and use it on a laptop browser. Realizes UJ-1.

**Consequences (testable):**
- The app provides a web manifest and a minimal service worker; no health data is cached offline.

#### FR-8: Clinic Settings
Admin can set the Clinic's name, branding and terminology labels. The Doctor can set Check-in questions and Flag Rules. Ayurvedgram is the seeded Clinic. `[ASSUMPTION: split by role as in the Glossary.]`

**Consequences (testable):**
- Changing a label in Clinic Settings changes it on the screens without a code change.
- No screen text names Ayurvedgram except through Clinic Settings.
- Admin cannot edit Flag Rules; a Coordinator cannot edit any Clinic Setting.

**Feature-specific NFRs:** all queries run as the signed-in user; the service key is used only in server-side jobs.
**Notes:** `[NOTE FOR PM]` the core-versus-customizable split is a draft (addendum). Confirm at architecture.

### 4.2 Patient record, episodes and phases
**Description:** Staff see a list of Patients with a Phase tag, can filter and search, and see a needs-attention block. Each Patient has many Episodes. Staff move an Episode between Phases and each move is recorded. A Patient sees a six-step journey bar and a card for what matters today. Realizes UJ-1, UJ-2, UJ-5.

**Functional Requirements:**

#### FR-9: Patient list
Staff can list Patients with their current Phase, filter by Phase and search by name, email or phone. Realizes UJ-2.

**Consequences (testable):**
- Search returns only Patients of the Staff user's Clinic.
- A needs-attention block shows Alerts.

#### FR-10: Episodes and phase moves
Staff can move an Episode forward or back between Phases, and the system records who, when, and an optional note. Realizes UJ-2.

**Consequences (testable):**
- Every Phase change creates a history entry.
- A Patient can have more than one Episode, each with its own Phase.

#### FR-11: Returning Patient
Staff can start a new Episode for an existing Patient at Assessment or Planning, without re-entering personal details or Documents. Realizes UJ-5.

**Consequences (testable):**
- The new Episode inherits the Patient record; Enquiry is skipped.

#### FR-12: Patient home
A Patient can see a journey bar of the six Phases with the current Phase marked, and a card for what matters today. Realizes UJ-1.

**Consequences (testable):**
- Phase status is shown in text as well as colour.

### 4.3 Onboarding and documents
**Description:** A dedicated flow, separate from the Patient list, to add a Patient. Required fields are minimal. Optional details and uploads can follow. A consent step is the second step. The Invite is sent at the end. The Documents tab holds all files of the Patient. Realizes UJ-2.

**Functional Requirements:**

#### FR-13: Onboard a Patient
Staff can create a Patient with name, email, phone and nationality (required) and photo, date of birth, passport number and emergency contact (optional). Realizes UJ-2.

**Consequences (testable):**
- Submission fails with a specific message per missing required field.
- Phone must include a country code; email must be valid.
- If emergency contact has a name but no phone, submission asks for the phone.

#### FR-14: Save draft
Staff can save an unfinished onboarding as a draft and resume it later. Realizes UJ-2.

**Consequences (testable):**
- A draft does not create a sign-in account or send an Invite.

#### FR-15: Duplicate warning
Staff are warned when the email, phone or passport number matches an existing Patient in the Clinic. Realizes UJ-2.

**Consequences (testable):**
- The warning links to the existing record; Staff can still continue after confirming.

#### FR-16: Consent step
The onboarding flow includes a Consent step as step 2, recording the Consent text version, the time and who gave it. `[ASSUMPTION: the prototype uses sample wording labelled "not legal text".]`

**Consequences (testable):**
- A Consent record stores the text version and timestamp.
- The sample text is visibly labelled as sample.

#### FR-17: Upload documents
Staff and Patients can upload PDF, JPG, PNG or HEIC files up to 15 MB each, with Shared or Staff-only visibility. Realizes UJ-2.

**Consequences (testable):**
- A file over 15 MB or of another type is rejected with "Upload a PDF, JPG, PNG or HEIC file under 15 MB."
- Uploads from a phone camera succeed.
- `[ASSUMPTION: HEIC is accepted and converted to JPEG; the method is decided at architecture.]`

#### FR-18: Documents tab
A Patient record has a Documents tab listing all Documents with kind and visibility.

**Consequences (testable):**
- A Patient sees only Shared Documents.

#### FR-19: Invite
After onboarding, the system can send the Patient an Invite email with a single-use link and a code. Realizes UJ-1.

**Consequences (testable):**
- Staff can resend an Invite.
- In the prototype the Invite goes through a development mail setup or is shown to Staff in the app. Provider setup comes later.

### 4.4 Enquiry, assessment and planning
**Description:** Staff log what happened outside the app, after the fact, and record the Programme and cost settled before travel. The app does not change how Enquiry or Assessment happen. Realizes UJ-2, UJ-5.

**Functional Requirements:**

#### FR-20: Log an enquiry
Staff can log an enquiry with date, channel (WhatsApp, email, phone, other), summary, treatment interest and who handled it. Realizes UJ-6.

**Consequences (testable):**
- Returning Patients are not required to have an enquiry.

#### FR-21: Log a Quotation
Staff can log each Quotation with version, date sent, amount and currency, validity and status. Realizes UJ-6.

**Consequences (testable):**
- Amount must be greater than zero; versions within an Episode are unique and increasing.

#### FR-22: Log an Assessment
The Doctor can log an Assessment with date, method (in person, WhatsApp call, phone, video, email), Doctor, findings and outcome, marked Shared or Staff-only. Realizes UJ-6.

**Consequences (testable):**
- A Patient sees only Shared Assessments.

#### FR-23: Record the Programme
Staff can record the Programme and approximate cost linked to the accepted Quotation, with a status (provisional, confirmed, refined on arrival). Realizes UJ-6.

**Consequences (testable):**
- A Programme can link only to a Quotation of the same Episode.

#### FR-24: Record payments received
Staff can record payments received (deposit, balance, other) with amount, currency, date and method. No online payments. Realizes UJ-6.

**Consequences (testable):**
- The app stores no card data.

### 4.5 Arrival
**Description:** Flight, pickup and stay are visible to the Patient in one place. The clinic enters pickup and stay. The Patient or clinic enters flight details. Realizes UJ-1.

**Functional Requirements:**

#### FR-25: Flight details
Staff or the Patient can enter flight number and arrival date and time. Realizes UJ-1.

**Consequences (testable):**
- Flight number must be airline code plus number (for example "LX 148"). `[ASSUMPTION: this format check.]`
- Arrival time is stored in UTC and shown in the viewer's local time.

#### FR-26: Pickup
Staff can enter pickup details (driver name and phone, car, plate, meeting point, time), visible to the Patient. Realizes UJ-1.

**Consequences (testable):**
- A Patient sees pickup details only for their own Episode.

#### FR-27: Accommodation
Staff can enter Accommodation and check-in details, visible to the Patient. Realizes UJ-1.

**Consequences (testable):**
- A Patient sees Accommodation only for their own Episode.
- A change by Staff updates the Patient's arrival-day card.

#### FR-28: Arrival-day card
A Patient can see an arrival-day card on the home screen with flight, who meets them and where they stay. Realizes UJ-1.

**Consequences (testable):**
- The card shows flight number and arrival time in the Patient's local time, the driver's name and phone, and the Accommodation.
- A field Staff have not yet entered shows as "Not yet confirmed".

#### FR-29: "I have landed" and "I need help"
A Patient can tap "I have landed" or "I need help", and the Coordinator sees an alert. Realizes UJ-1.

**Consequences (testable):**
- The alert appears in the needs-attention block (FR-9) with Patient name and time.

#### FR-30: Flight-edit alert
When a Patient edits flight details, the Coordinator receives an alert.

**Consequences (testable):**
- The alert names the Patient and the change.

### 4.6 Care
**Description:** The Doctor records findings, notes and medicines. The Coordinator builds a Day Plan for each Patient and publishes it. The Patient sees the schedule, diet and current medicines, answers a daily Check-in, and the Doctor reviews. The app records and alerts. It never gives medical advice. Realizes UJ-2, UJ-3.

**Functional Requirements:**

#### FR-31: Post-arrival findings and Notes
Doctor can record post-arrival findings and Notes, each marked Shared or Staff-only. Realizes UJ-3.

**Consequences (testable):**
- A Patient sees Shared Notes only. A Coordinator reads Shared Notes and never Staff-only ones.

#### FR-32: Prescribed medication
Doctor can record medicines with name, dose, schedule, start date and duration. Realizes UJ-3.

**Consequences (testable):**
- A Patient sees the current course and can ask to see the history, which is then shown.

#### FR-33: Build and publish a Day Plan
Staff can build a Day Plan from treatments, diet, medicines and accommodation, copy yesterday's plan, and publish it to the Patient. Realizes UJ-2.

**Consequences (testable):**
- Copy duplicates yesterday's items into a Draft for the chosen date.
- Only Published Day Plans are visible to the Patient.
- Publishing a plan twice does not duplicate the plan or its notification.

#### FR-34: Record daily treatments given
Staff can record treatments actually given on a day. Realizes UJ-6.

**Consequences (testable):**
- A record stores the treatment, therapist name, duration and notes for one date.
- A treatment given can differ from the one planned, and both are kept.

#### FR-35: Patient day view
A Patient can see the Published Day Plan's schedule and diet, and the current medicines, with a way to tick medicines taken. Realizes UJ-2.

**Consequences (testable):**
- A medicine tick is stored with a time and source.

#### FR-36: Daily Check-in
A Patient can answer a daily Check-in about whether medicines were taken and how the treatment is going. `[ASSUMPTION: five questions as a default; the questions are a Clinic Setting.]` Realizes UJ-3.

**Consequences (testable):**
- Medicines answer is yes, partly or no; scores are 1 to 5; free text is limited to 1,000 characters. `[ASSUMPTION: these answer formats and limits.]`
- Submitting twice for the same day does not create two Check-ins.
- The Patient sees confirmation that the Check-in was received.

#### FR-37: Review Queue
Doctor can open a Review Queue of Check-ins, Flagged first, with the reason for each Flag. Realizes UJ-3.

**Consequences (testable):**
- Flagged Check-ins sort above unflagged ones.
- The Doctor sees only Check-ins of their Clinic.

#### FR-38: Sample Flag Rules
The system can raise a Flag on a Check-in using Flag Rules from Clinic Settings. The prototype ships a Sample Flag Rule set, labelled "sample, not clinical". `[ASSUMPTION: sample rules exist only so the demo can show a queue; the real rules come from the Doctor, PK-09.]` Realizes UJ-3.

**Consequences (testable):**
- Changing a Flag Rule in Clinic Settings changes which Check-ins are Flagged, without a code change.
- The app raises a Flag only from configured rules and never interprets answers medically.

#### FR-39: Review a Check-in
Doctor can add a Note, change a medicine and mark a Check-in reviewed from the same screen. Realizes UJ-3.

**Consequences (testable):**
- A reviewed Check-in leaves the Queue and records who and when.

### 4.7 Continuity
**Description:** After departure the Clinic schedules follow-up Check-ins. The Patient answers them. The Clinic logs Consultations. A Patient can request an extra Consultation. Realizes UJ-4.

**Functional Requirements:**

#### FR-40: Log departure assistance
Staff can log departure travel assistance. Realizes UJ-6.

**Consequences (testable):**
- An entry stores date, what was arranged and who arranged it, against the Episode.

#### FR-41: Schedule follow-up Check-ins
Staff can schedule follow-up Check-ins for a Patient, which appear to the Patient at the scheduled time in the Patient's time zone. Realizes UJ-4.

**Consequences (testable):**
- Check-ins are initiated by the Clinic's schedule, never by the Patient.
- Running the schedule job twice creates no duplicate Check-ins.

#### FR-42: Answer a follow-up Check-in
A Patient can report how they feel, confirm medicines taken and flag diet issues. Realizes UJ-4.

**Consequences (testable):**
- The answer enters the Review Queue like a care Check-in.

#### FR-43: Log Consultations
Doctor or Coordinator can log WhatsApp and phone Consultations given after the Patient is home, with date, channel and summary.

**Consequences (testable):**
- A logged Consultation appears in the Patient's Episode history in date order.
- Channel is one of WhatsApp call, WhatsApp video, phone, video or other.

#### FR-44: Request an extra Consultation
A Patient can request an extra Consultation with a preferred time and reason, and Staff can approve or decline it. Realizes UJ-4.

**Consequences (testable):**
- A new request appears in the needs-attention block.
- A Patient sees the status of their own requests only.

### 4.8 Notifications
**Description:** Events become notifications stored in an in-app inbox and sent by email. Provider setup and WhatsApp come later. Realizes UJ-1, UJ-2.

**Functional Requirements:**

#### FR-45: In-app inbox
A user can see their notifications in an in-app inbox, such as a Published Day Plan, an Invite, a follow-up Check-in or an alert.

**Consequences (testable):**
- A user sees only their own notifications.

#### FR-46: Email notifications
The system can send email notifications for the same events. In the prototype delivery uses a development mail setup. Provider and sending domain are configured later.

**Consequences (testable):**
- A failed send is recorded and retried. `[ASSUMPTION: up to three attempts with increasing delay.]`
- The in-app Notification still exists after a failed send.

### 4.9 Prototype foundations
**Description:** Two supports the journeys depend on: the Patient's time zone and a repeatable demo seed.

**Functional Requirements:**

#### FR-47: Patient time zone
Staff can record a Patient's time zone, and the system displays that Patient's flight, Check-in and reminder times in it. Realizes UJ-4.

**Consequences (testable):**
- A time entered for a Patient in a different time zone from the viewer shows correctly in each viewer's local time.
- A new Patient defaults to the Clinic's time zone until set. `[ASSUMPTION: default to the Clinic's time zone.]`

#### FR-48: Demo seed
The system can load a clean demo data set of invented Patients, Staff and two Clinics, covering all six Phases, so UJ-1 to UJ-6 and the isolation suite can be run from a clean start. Realizes UJ-1 to UJ-6.

**Consequences (testable):**
- Loading the seed twice leaves the same data, not duplicates.
- Every seeded name, email, phone and passport number is invented, and the seed is the only place such data lives.

## 5. Non-Goals (Explicit)
- Not a replacement for first contact on WhatsApp, email and phone.
- Not a clinical decision tool: no diagnosis, no medical advice, no interpretation of answers.
- Not a marketplace or a commissions platform.
- Not a payment processor: payments are only recorded.
- Not a multi-clinic operating platform in this prototype: the design is clinic-ready, but only one Clinic is live.
- Not a national health-record system: no ABDM or Ayush Grid integration.

## 6. MVP Scope

### 6.1 In Scope
An end-to-end working prototype of the six Phases on invented data: access, roles and clinic isolation with a test suite; patient record and episodes; onboarding with documents and the consent step; enquiry, quotation, assessment, programme and payment logs; arrival; care; continuity; notifications in-app and by development email. English only. Phone and laptop for Staff, phone first for Patients.

### 6.2 Out of Scope for MVP
- Real patient data and any rollout to users.
- Audit log and staff MFA. A hard gate before real data.
- WhatsApp sending and setup, email provider and domain configuration, web push (later).
- Online payments, native apps, other clinics live.
- Therapist, kitchen and attendant logins; return-visit nudges.
- Visa tracker, pre-arrival checklist and information pack, in-app message thread, patient rights tools (export, correct, erase), medicine supply tracker, feedback form, departure documents handover, trend view of check-in scores, second transfer leg, therapy record per session. `[NOTE FOR PM]` visa tracker and patient rights tools are the likely first additions for the pilot.
- Finer details within each Phase.

## 7. Success Metrics

**Primary**
- **SM-1**: Demo journey completion. A person can walk UJ-1 to UJ-6 on a deployed build from a clean seed, without editing the database by hand. Target: 6 of 6 journeys completed. This is wider than the brief's single demo journey, because the PRD covers all six Phases. Validates FR-1 to FR-48.
- **SM-2**: Isolation coverage. The isolation suite covers every clinic-owned table and the document store, and passes. Target: 100% of tables listed, 0 cross-patient or cross-clinic reads or writes succeed. Validates FR-4, FR-5, FR-6.

**Secondary**
- **SM-3**: Pilot-readiness findings. After the demo, Ravi records a list of what blocks a pilot (usability with older users, staff entry time, clinical content). Target: a written list exists. This list feeds the pilot PRD.

**Counter-metrics (do not optimize)**
- **SM-C1**: Number of tests. Isolation coverage is measured by tables covered, not test count. Counterbalances SM-2.
- **SM-C2**: Screen polish. Do not spend prototype time perfecting visuals at the expense of a complete journey. Counterbalances SM-1.

## 8. Cross-Cutting Requirements and Constraints

**NFRs**
- **Data:** invented data only in code, seeds, tests and screenshots. No real patient data until the legal gate is passed.
- **Responsive:** Coordinator and Doctor can do every task on phone or laptop with the same data. No device-only features.
- **Language:** English only. UI text lives in resource files so languages can be added later.
- **Time:** all times stored in UTC. Patient time zone is stored and times display in local time.
- **Privacy:** no personal health data in application logs, error reports or analytics.
- **Security:** access rules are enforced in the database. The browser never holds the service key.
- **Reliability:** scheduled jobs are idempotent. Retried actions do not duplicate.
- **Accessibility:** status is never shown by colour alone.

**Gate before real patient data (all required):** legal review of consent, GDPR and DPDP, with approved Consent wording and retention periods; audit log; staff MFA; isolation suite passing; hosting region confirmed; sponsor and doctor engaged at Ayurvedgram.

**Platform:** web app installable on a phone. Stack (Next.js, Vercel, Supabase) and India hosting are decided, recorded in the addendum.

## 9. Open Questions
1. Who is the sponsor at Ayurvedgram? (PK-01)
2. What are the doctor's real Flag Rules, structured clinical fields, follow-up templates and Check-in questions? (PK-09, PK-10, PK-11, PK-14). Needs a doctor session.
3. Consent wording and legal approval, retention and erasure periods. (PK-04, PK-18). Needs a lawyer.
4. Can the Supabase Mumbai region host the database project? What is the latency for European patients? (PK-05, spike S-3)
5. How is HEIC converted: in the browser before upload or on the server? (PK-27, spike S-5)
6. Should the Check-in scheduler be a database scheduler or Vercel cron? (PK-29, spike S-2)
7. Is malware scanning of uploads needed? (PK-27)
8. Which core features can a Clinic rename or skip, if any? (Phases are fixed for now.)
9. What is the sending domain and email provider setup for pilot? Deferred. (PK-22)

## 10. Assumptions Index
Every `[ASSUMPTION]` in the document, for explicit confirmation:
- Glossary, Doctor and FR-8: the Doctor owns Check-in questions and Flag Rules; Admin owns branding, terminology and users.
- Role table (section 4.1): the capability split by role.
- FR-2: link and code expire after one hour; 60-second re-request window.
- FR-16: the Consent step uses sample wording labelled "not legal text".
- FR-17: HEIC is accepted and converted to JPEG; method decided at architecture.
- FR-25: flight number format check.
- FR-36: five Check-in questions by default; answer formats and limits.
- FR-38: Sample Flag Rules exist only so the demo can show a queue.
- FR-46: up to three send attempts with increasing delay.
- FR-47: a new Patient defaults to the Clinic's time zone.
- Section 6.1: clinic home, patient home, Documents tab, Episodes and phase moves are in because the journey cannot be walked without them.
- Section 6.2: the audit log and MFA are deferred to the gate before real data.
- Section 8: the core-versus-customizable split in the addendum is a draft.
