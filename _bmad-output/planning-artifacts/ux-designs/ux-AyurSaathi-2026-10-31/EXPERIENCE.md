---
name: AyurSaathi
status: final
sources:
  - _bmad-output/planning-artifacts/prds/prd-AyurSaathi-2026-10-22/prd.md
  - _bmad-output/planning-artifacts/architecture/architecture-AyurSaathi-2026-10-24/ARCHITECTURE-SPINE.md
  - _bmad-output/planning-artifacts/briefs/brief-AyurSaathi-2026-10-21/brief.md
updated: 2026-10-31
---

# AyurSaathi — Experience Spine

> Prototype on invented data. Companion to `DESIGN.md` (visual identity; tokens are referenced as `{path.to.token}`). Both spines win on conflict with any mock. Requirement IDs (FR-n) and journey IDs (UJ-n) are the PRD's.

## Foundation

A responsive web app, installable to the phone home screen, with three areas in one codebase: a **public** area (sign-in, invite redemption), a **patient** area (phone first), and a **clinic** area (Coordinator, Doctor, Admin on phone or laptop with identical capability, BR-12). No UI component library is named; components are built to `DESIGN.md`. English only, with all text in resource files and clinic terminology overridable (AD-7). Dark theme follows the system setting. Every screen shows the Demo data ribbon.

## Information Architecture

### Public

| Surface | Reached from | Purpose |
|---|---|---|
| Sign in | App open, signed out | Enter email; receive a link and a code (FR-2, FR-1 for staff) |
| Enter code | After "Send link" | Type the six-digit code if the link fails |
| Redeem invite | Link in the Invite email | One button to open the account (AD-14) |
| Install help | Sign-in footer, after first sign-in | How to add to the home screen |

### Patient area (bottom bar: Home, Plan, Documents, Check-in)

| Surface | Reached from | Purpose | PRD |
|---|---|---|---|
| Home | Bar, app open | Journey bar; "today" card; arrival-day card; Updates; request a consultation | FR-12, 28, 25, 29, 44, 45 |
| Arrival details | Home arrival-day card | Flight (editable), pickup, stay; "I have landed", "I need help" | FR-25–29 |
| Plan | Bar | Day view: schedule, meals, medicines with Taken toggles; date switcher; current medicines, "Show earlier medicines" | FR-35, 32 |
| Documents | Bar | Documents shared with the patient; upload | FR-17, 18 |
| Check-in | Bar | Today's check-in, or the next follow-up | FR-36, 42 |
| Request a consultation | Home, Plan | Preferred time and reason; status of past requests | FR-44 |
| Updates | Home section | Notifications (published plan, check-in due, request decided) | FR-45 |
| Settings | Home header | Theme, sign out | |

### Clinic area (phone bottom bar: Today, Patients, Review or Plans, More; laptop sidebar)

| Surface | Reached from | Purpose | PRD |
|---|---|---|---|
| Today | Bar, app open | Alerts (needs-attention); today's arrivals; plans to publish; check-ins to review count | FR-9, 29, 30, 44 |
| Patients | Bar | List with phase chip, filter by phase, search | FR-9 |
| Onboard a patient | Patients, "Add patient" | Three steps: Details, Consent, Review and invite; save draft; on success an "Add documents now" card | FR-13–16, 19 |
| Patient record | Patients list, Alert | Header (name, phase, time zone, alerts); tabs below | FR-10, 11, 47 |
| Record: Overview | Tab | Summary, phase history, move phase, start a new Episode | FR-10, 11 |
| Record: Before arrival | Tab | Enquiry log, Quotations, Assessment log, Programme, Payments | FR-20–24 |
| Record: Arrival | Tab | Flight, pickup, accommodation, arrival events | FR-25–30 |
| Record: Care | Tab | Notes, medicines, Day Plans, treatments given, Check-ins | FR-31–39 |
| Record: After | Tab | Departure assistance, follow-up schedule, consultations, requests | FR-40–44 |
| Record: Documents | Tab | All documents with Shared or Staff-only | FR-17, 18 |
| Day Plan builder | Care tab, Today | Pick a date, copy yesterday, edit items, publish | FR-33, 34 |
| Review Queue | Bar (Doctor) | Check-ins, flagged first; review a check-in | FR-37–39 |
| Settings: Clinic | More, Settings | Branding and terminology (Admin) | FR-8 |
| Settings: Clinical rules | More, Settings | Check-in questions and Flag Rules, labelled "Sample" (Doctor) | FR-8, 36, 38 |
| Settings: People | More, Settings | Staff users and roles (Admin) | FR-3 |

→ Composition references (spines win on conflict): `mockups/key-patient-home-arrival.html`, `mockups/key-patient-checkin.html`, `mockups/key-clinic-today-laptop.html`, `mockups/key-doctor-review-phone.html`.

**Closure.** Every PRD requirement above maps to a surface; every surface is reached from a journey (UJ-1 to UJ-6, Key Flows below). Consultations logged after contact (FR-43) live on Record: After; Payments (FR-24) on Record: Before arrival.

**Role visibility.** Coordinator: all clinic surfaces except Clinical rules (read-only) and People; sees Shared Notes only; cannot write Notes, Medicines or Assessments. Doctor: all clinical surfaces and Clinical rules. Admin: Clinic and People settings; reads clinical records. This mirrors the PRD role table; the database enforces it, and the UI hides what the role cannot use rather than showing disabled controls.

## Voice and Tone

Microcopy. Brand voice lives in `DESIGN.md.Brand & Style`. Calm, plain, specific. Short sentences. Second person to patients ("your plan"), neutral to staff. No exclamation marks, no urgency words, no jokes, no medical claims.

| Do | Don't |
|---|---|
| "Your plan for Thursday 12 November." | "Get ready for tomorrow!" |
| "Not yet confirmed." | "Pending…" or an empty field |
| "Received. Your doctor reviews check-ins each day." | "Your doctor is monitoring you." |
| "For urgent help, call the clinic on +91 20 5555 0100. In an emergency, call your local emergency number." | "Press for help!" on a health question |
| "That file is larger than 15 MB. Choose a smaller file or compress it." | "Upload failed." |
| "We could not save the plan. Your changes are still on this screen. Try again." | "Error 500." |
| "Staff-only. The patient cannot see this." | A lock icon with no words |
| "Sample rules. Not clinical advice." | Presenting sample flag rules as the clinic's policy |

Labels are sentence case with specific verbs ("Publish to patient", "Mark reviewed", "Send link"). The same word for the same thing everywhere: always "check-in", never "survey" or "questionnaire"; always "Day Plan" for the schedule; always "Staff-only", never "private".

## Component Patterns

Behavioral rules. Visual specs live in `DESIGN.md.Components`.

| Component | Use | Behavioral rules |
|---|---|---|
| Bottom bar | Patient, staff phone | Four items, always icon plus label. Current item has a teal bar and bold label. Never hides on scroll. Switching tabs keeps each tab's scroll position. |
| Sidebar | Staff laptop | Same items as the phone bar plus Settings. Collapsible to icons only above 1280px; labels return on hover and focus. |
| Journey bar | Patient Home; record header | Shows six phases. Tapping a completed phase on patient Home opens a read-only summary of what the clinic shared for it. On staff screens tapping a phase filters the record tabs. |
| Phase chip | Lists, headers | Number plus name. Not a button except inside the move-phase control. |
| Alert row | Today | One sentence, patient name, time, one "Open" action. Opening resolves nothing by itself; resolution happens in the destination (for example reviewing the check-in). |
| Patient list row | Patients | Name, phase chip, one status badge (Needs review, Arriving today, Nothing due), last activity. Whole row is the target. |
| Onboarding stepper | Onboard | Three steps with "Step 2 of 3". Back keeps input. After "Send invite" the success screen shows an "Add documents now" card (passport, medical records) that opens the Documents tab; documents attach only to the saved patient record, never to a draft. "Save draft" always visible; leaving prompts "Save as draft?". Step 2 (Consent) shows the sample text with a visible "Sample wording. Not legal text." badge and records version, time and who ticked it. |
| Duplicate warning | Onboard step 1 | Appears on blur of email, phone or passport. Shows the match with "Open that record" and "Continue anyway". |
| Document uploader | Success-screen card, Documents tab | Camera or file chooser. HEIC photos are converted before upload with a visible "Preparing photo…" line. Each file shows name, size, visibility toggle (Shared or Staff-only) and a Remove action behind a confirmation. Limits shown before choosing: "PDF, JPG, PNG or HEIC, up to 15 MB". |
| Visibility toggle | Notes, assessments, documents | A two-option control, "Shared with patient" or "Staff-only", default Staff-only. The current choice is stated in words beside the control. |
| Day Plan builder | Care | Date strip across the top. "Copy yesterday" fills a Draft; items are editable rows grouped Morning, Midday, Evening. "Publish to patient" is the only primary action; it shows a confirmation with the patient name and date. Draft versus Published is a status badge. Publishing twice does nothing new and says "Already published." |
| Medicine row | Plan, Care | Name, dose, schedule, "Taken" toggle with time. The patient toggle can be undone for 10 minutes. |
| Check-in flow | Patient Check-in | One question per screen, "Question 2 of 5", large answer buttons, Back at every step, Review screen before Send. Medicines answer: Yes, Partly, No. Score answers 1 to 5 with word anchors ("Poor" to "Very good"). Free text up to 1,000 characters with a counter. |
| Review Queue | Doctor | List sorted Flagged first, then time. A Flagged row states the rule in words ("Medicines: No"). The review pane shows answers, the patient's recent notes and medicines, and actions: Add note (Shared or Staff-only), Change medicine, Mark reviewed. |
| Alert and notification inbox | Today, Home | Newest first. Unread are marked "New" in text. Read state is stored. |
| Time display | Everywhere | "Thu 12 Nov, 14:35 IST", and "(Pune 17:05)" in brackets when the viewer's zone differs. |
| Demo ribbon | Every screen | Fixed at top. Not interactive. |

## State Patterns

| State | Surface | Treatment |
|---|---|---|
| Loading | Any list or detail | Skeleton of the final layout and the words "Loading". Never a blank screen. |
| Empty | Patients | "No patients yet. Add the first patient." with the Add patient button. |
| Empty | Patient Plan | "Your plan for this day has not been published yet. Your coordinator will publish it." |
| Empty | Patient Documents | "No documents yet. Your clinic will add documents here. You can add your own." |
| Empty | Review Queue | "Nothing to review right now." |
| Empty | Today | "Nothing needs attention." |
| Not yet entered | Arrival fields | "Not yet confirmed." on each missing field; the card still shows what is known. |
| Draft | Onboarding, Day Plan | Status badge "Draft" and the date it was saved. |
| Error, field | Forms | Message under the field in words that fix it ("Enter the phone number with country code, for example +43 1 234 5678."), icon, first invalid field takes focus, error announced to assistive technology. Input is kept. |
| Error, action | Any save | Banner on the screen: what failed, that input is kept, "Try again". Never loses data. |
| Link or code problem | Sign-in | "That link has already been used or has expired. Type the code from the email, or ask for a new link." with both actions. A "Send a new link" cooldown shows the seconds left. Same message whether or not the email exists. |
| Forbidden | Any route | "You do not have access to this page." with a link to the user's home. No details about the record. |
| Offline | Any | App shell loads. Health data is not cached. Banner: "You are offline. Connect to see your information." Writes are not queued. |
| Upload in progress | Uploader | Per-file progress in words and a Cancel action. |
| Upload rejected | Uploader | "This file is larger than 15 MB. Choose a smaller file or compress it." or "Upload a PDF, JPG, PNG or HEIC file." |
| Check-in done | Check-in tab | "Received. Your doctor reviews check-ins each day." plus the clinic phone line. The tab then shows the next check-in time. |
| Check-in not due | Check-in tab | "Your next check-in is Friday 13 November at 08:00." |
| Flagged | Staff lists | Badge "Needs review" with the rule that raised it. The patient is never told they were flagged. |
| Sample content | Clinical rules | Persistent badge "Sample rules. Not clinical advice." on the page and on each flag reason. |
| Session expired | Any | "You have been signed out. Sign in again." returns to the same page after sign-in. |

## Interaction Primitives

- Tap or click to act. No long-press, no double-tap, no hover-only controls. Swipe is never the only way to do something.
- Typing a code: one field, six digits, `autocomplete="one-time-code"` so the phone can fill it; paste allowed.
- Dates and times use native pickers on phone and a text field with a picker on laptop.
- Destructive actions (remove a file, move a phase back, decline a request) always ask once, naming the thing.
- Keyboard on laptop: all actions reachable by Tab; "/" focuses search on Patients; Enter submits the focused form; Escape closes a sheet.
- Pull-to-refresh on Updates and Review Queue only, with a visible "Refresh" button as well.
- **Banned:** carousels, auto-advancing anything, countdown timers, streaks, badges with counts that imply urgency, push-style nagging copy, confetti, animation longer than 200ms. Reduced motion removes all transitions.

## Accessibility Floor

Behavioral. Visual contrast lives in `DESIGN.md`.

- Target WCAG 2.2 AA on patient screens, and the same on clinic screens where practical.
- Every interactive element has an accessible name, role and state. Status changes announce through a polite live region ("Plan published", "Saved", "Check-in received").
- Tap targets 48px minimum, 56px on patient screens, at least 8px apart.
- Layouts work at 200% text size and at 320px width without horizontal scroll; labels wrap, never truncate.
- Focus is visible on every element, follows reading order, moves to the first error on a failed submit, and returns to the trigger when a sheet closes.
- No information by colour alone; status is always icon plus words; the phase is its number and name.
- Forms use real labels, helper text linked to the field, and error text linked to the field.
- Time limits: none on patient screens except the sign-in link and code, which tell the user how long they last and how to get a new one.
- Plain language, aim for a reading age of about 12 on patient screens. No jargon without a gloss ("Programme: the treatment plan agreed before you travel").
- Screen reader: the journey bar reads as "Step 4 of 6, Arrival, now".

## Responsive & Platform

| Width | Patient | Staff |
|---|---|---|
| Under 600px | Single column, bottom bar | Single column, bottom bar, tabs scroll horizontally with a visible edge fade and the active tab scrolled into view |
| 600 to 1023px | Single column capped at 560px, centred, bottom bar | Single column, wider measure, bottom bar |
| 1024px and up | Same as 600+, centred | Sidebar plus list-and-detail: Patients list on the left (360px), record on the right; Review Queue likewise |

Installable: the app shows an "Add to home screen" help page after first sign-in. Offline is the shell only (AD-18). Orientation is not locked.

## Safety & Honesty

The app records and alerts; it never advises (BR-06).
- No screen explains what an answer means medically. Check-in results are never shown back as a score interpretation.
- "I need help" on arrival is a logistics alert to the Coordinator. Its screen says so and shows the clinic phone and the line "For a medical emergency, call your local emergency number."
- Check-in and Plan carry the clinic phone line in the footer.
- Flag Rules are configuration set by the Doctor. Prototype sample rules are labelled as such and are never shown to patients.
- Demo data ribbon on every screen; no real patient may be entered (BR-08).

## Inspiration & Anti-patterns

- **Lifted from airline check-in flows:** one question per step, a review step before sending, and a calm confirmation. The patient already knows this pattern.
- **Lifted from clinic reception boards:** a single Today list of who is arriving and who needs attention.
- **Rejected — chat-style patient communication:** the prototype has no message thread; WhatsApp stays the conversation channel (BR-01).
- **Rejected — dashboards of charts for staff:** the prototype lists, it does not chart. A check-in trend view is a later candidate.
- **Rejected — gamified health tracking:** no streaks, scores shown as grades, or encouragement copy.

## Key Flows

### Flow 1 — Anna opens the invite and sees the arrival details (UJ-1)

1. Anna taps the link in the Invite email on a phone.
2. The Redeem page says "Open your AyurSaathi account" with one button. Anna presses it.
3. Home opens with "Step 4 of 6, Arrival" and the arrival-day card.
4. The card shows "Flight: Not yet confirmed". Anna taps "Add flight", types "LX 148" and the arrival time, and saves.
5. The card now shows the flight in Anna's own time zone with the Pune time in brackets, the car and driver, and where Anna stays.
6. After landing Anna taps "I have landed". The screen says "Thank you. Your coordinator has been told." and shows the clinic phone.
7. **Climax:** the arrival-day card shows who meets Anna and where, in one place, and the landed confirmation proves the clinic knows.

Failure: the mail scanner already opened the link. Redeem still works because the link needs a button press; if the link has expired, the sign-in screen offers the code (Foundation, State Patterns).

### Flow 2 — Meera onboards a patient and publishes tomorrow's plan (UJ-2)

1. Meera taps Patients, then "Add patient".
2. Step 1: name, email, phone, nationality. The duplicate check runs on blur.
3. Step 2: the sample consent text with its Sample badge; Meera records that the patient agreed.
4. Step 3: review, "Send invite". The success screen shows the Invite status "Sent" and an "Add documents now" card.
5. Meera taps the card, photographs the passport; the uploader shows "Preparing photo…" then the file with Staff-only selected. The record opens on Overview.
6. Later, in the Care tab Meera opens Day Plan, picks tomorrow, taps "Copy yesterday", changes two items, and taps "Publish to patient".
7. **Climax:** the badge changes to "Published at 17:42" and the confirmation names the patient.

Failure: a duplicate email. The warning shows the existing record with "Open that record"; Meera does not lose what was typed.

### Flow 3 — Dr. A reviews the morning's check-ins (UJ-3)

1. Dr. A opens Review (phone) or the Review Queue (laptop).
2. Flagged check-ins are listed first, each with the rule in words.
3. Dr. A opens one and reads the answers and the recent notes.
4. Dr. A adds a Note, chooses Shared with patient, changes a medicine's dose, and taps "Mark reviewed".
5. **Climax:** the row leaves the queue and the Today count drops; the patient will see the Shared note and the changed medicine.

Failure: the sample rules flag too many. Dr. A opens Settings, Clinical rules, edits the rule, and the queue re-sorts on the next evaluation.

### Flow 4 — Anna, back home, answers a follow-up and asks for a call (UJ-4)

1. Anna signs in with the emailed link; the Check-in tab shows "Your follow-up check-in".
2. Five one-question screens: medicines (Yes, Partly, No), how they feel, diet, free text.
3. A review screen; Anna taps "Send".
4. **Climax:** "Received. Your doctor reviews check-ins each day." with the clinic phone line.
5. From Home Anna taps "Request a consultation", picks a time and gives a reason. The request shows "Waiting for the clinic".
6. The coordinator approves it; the status becomes "Approved for Thursday 19 Nov, 16:00 your time".

Failure: Anna is in a different time zone. Every time shows Anna's local time with the Pune time in brackets.

### Flow 5 — Marc returns for a second visit (UJ-5)

1. The coordinator searches "Marc" in Patients and opens the record.
2. On Overview the coordinator taps "Start new episode" and chooses Assessment or Planning.
3. **Climax:** the record keeps Marc's details and documents; nothing is re-entered, and the first episode is still visible as closed.

### Flow 6 — Meera and Dr. A record the journey (UJ-6)

1. Meera logs the WhatsApp enquiry and the first Quotation on Before arrival.
2. Dr. A logs the assessment call and its outcome, marking the findings Staff-only and the outcome summary Shared.
3. Meera records the Programme and the deposit received.
4. After care, Meera records treatments given and the departure assistance.
5. **Climax:** each step moves the Episode forward and the phase history on Overview reads as a complete record in order.
