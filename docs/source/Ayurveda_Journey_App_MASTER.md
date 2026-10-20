# Ayurvedic Clinic Patient Journey App: Master File

Owner: Ravi. Last updated 2026-10-17.
Purpose: one file holding everything so work can resume in any new session. Paste or attach this file and say "continue the Ayurveda journey app project".
Contents: (A) context and decisions, (B) research, (C) blueprint, (D) text wireframes, (E) design decisions and pending decisions, (F) HTML source of the visual mockups. Visual mockups also exist as an HTML page (04_mockups.html); the text wireframes below are the durable copy.

---

# A. Context and decisions

## A1. Project in brief
An app for one Ayurvedic clinic to give each international patient a single record and journey, replacing scattered WhatsApp, email and phone communication. The clinic is the customer; patients are onboarded into the app. First deployment is a single clinic.

## A2. Background from the WAC presentation (handoff file, provided by Ravi)
- Related work: a World Ayurveda Congress oral presentation, "Technology-enabled Ayurveda Medical Tourism: A Framework for a Global Ayurveda Tourism Model", authors Reema Sakhuja and Rajni Saluja, based on practice at Ayurvedgram, Pune (Atharva Nature Healthcare Pvt. Ltd.).
- The deck says: 510+ patients from 13 countries, about 9 years of operations; WhatsApp and email used for almost everything, plus video consultations.
- Its six journey stages: Enquiry, Assessment, Planning, Arrival, Care, Continuity. The journey loops back to the next visit.
- The deck grades technologies In use / Piloting / Proposed. The "patient app / portal" and "longitudinal digital record" are listed as Proposed. Some "Piloting" items were placeholders by an earlier Claude session and must be confirmed before presenting.
- Real case used in the deck: Petra Lehner (Austria): met the doctor in Europe, Nadi Pariksha, about three months of medicines, travelled to Pune, 14-day Panchakarma, video follow-up, returned a year later. Use her name only with consent. The mockups in this file use invented dummy patients.
- OPEN: Ravi has not yet confirmed the app's clinic is Ayurvedgram, Pune.

## A3. Decisions made by Ravi (from the saved project notes)
1. The clinic is the customer, not patients directly. Start with one specific clinic.
2. Problem: no central place for clinic records (travel plans, medical history); patients check many channels and can lose vital information.
3. One shared patient record behind a clinic dashboard and a patient app. One single app with role-based logins (not two apps).
4. Web app first, installable to the home screen of both the patient's and the clinic's phones. A path to native apps later if needed. All development is cloud driven.
5. Stack: Next.js frontend, Vercel hosting, Supabase (database, auth, storage), same as Ravi's Invento app.
6. Six phases: Enquiry, Assessment, Planning, Arrival, Care, Continuity.
7. Enquiry: first contact stays on WhatsApp, email or phone. The clinic logs the enquiry and quotation in the app and onboards the patient so Assessment onward happens in the app.
8. Assessment: stays as it is today (in-person Nadi Pariksha when the doctor is abroad; otherwise a remote WhatsApp call). The app logs the method used and the findings or outcome.
9. Planning: a preliminary programme and approximate cost (quotation) are settled before the patient travels; the doctor may refine on arrival. Consent timing is PARKED.
10. Arrival: flight details (number, arrival time) entered by clinic or patient; pickup (car and driver) entered by clinic; accommodation and check-in entered by clinic. All visible to the patient.
11. Care: clinic enters post-arrival assessment, doctor's notes, prescribed medication, daily treatments, daily diet, daily accommodation. Daily check-ins cover whether medicines are taken and how the treatment is going.
12. Continuity: travel assistance on departure; post-departure diet and medication follow-ups as an interactive loop; check-ins are clinic-initiated and scheduled; WhatsApp and phone consultations after the patient is home are logged; the record persists for repeat visits.
13. Returning patients skip Enquiry and go to Assessment or Planning.
14. Onboarding is a dedicated clinic screen. Mandatory: name, email, phone, nationality. Optional but captured: photo, date of birth, passport number, emergency contact. Optional uploads: passport scan, previous medical records.
15. Process: no building or coding yet. Produce a blueprint with mockups for review, then go phase by phase.

## A4. Working preferences
- Reply in English unless asked otherwise.
- In voice, let Ravi finish before responding (pause about two seconds).
- End each session with a concrete next step.
- Ravi reviews one phase or one recommendation at a time and wants a persistent record before building.

## A5. Open questions (ranked)
1. Is the clinic Ayurvedgram, Pune?
2. Who at the clinic enters data daily, and on what device?
3. Do therapists and the kitchen need logins in v1?
4. Consent timing and wording (parked); who approves it legally?
5. Hosting region: India or EU?
6. Payments in the app, or record only?
7. Languages needed beyond English for the patient side?
8. Should staff send WhatsApp from the app (needs the WhatsApp Business API)?
9. What does the doctor count as a "flag" in check-ins?
10. Which doctor will define the Ayurveda-specific fields (prakriti, pulse findings, Panchakarma protocols)?

## A6. Next steps
1. Ravi reviews the mockups (twelve screens) and the blueprint phase by phase; start with the doctor's review queue because the flag rules shape Care.
2. Answer the open questions above.
3. Legal review of consent, GDPR and DPDP before any real patient data.
4. Then decide the first build slice (suggested: foundation, then Arrival and Care).

## A7. File index
- 00_context_and_decisions.md: this section
- 01_research.md: research notes with sources
- 02_blueprint.md: application blueprint
- 03_mockups.md: text wireframes
- 04_mockups.html: visual mockups (published as a private artifact)
- 05_design_decisions_and_pending.md: decision log, visual system, pending decisions (also section E below)
- HANDOFF_Ayurveda_Journey_App.md: how to resume in a new session

---

# B. Research notes

Status: IN PROGRESS. Written incrementally so nothing is lost. Last updated 2026-10-16.
Only claims that a fetched source actually stated are recorded as findings. Gaps are listed as gaps.

## 1. Public landscape: what exists

### 1.1 Generic medical-tourism platforms (patient side)
Source: [Aalpha, medical tourism website development](https://www.aalpha.net/blog/medical-tourism-website-development/) (first ~100k characters read)
- Enquiry form as a short first step; document upload and medical history collected after initial contact.
- Secure encrypted document upload (imaging, labs, discharge summaries); access limited to assigned staff and logged.
- Scheduled video consultation; recording only with explicit patient consent.
- Itemised quote viewer where the patient accepts or declines.
- Booking and itinerary: deposit/payment, visa invitation letter, admission dates, transfer and interpreter details.
- Persistent secure messaging thread with coordinator and clinical team.
- Follow-up: recovery milestones, symptom logging, photo uploads, medication reminders, scheduled remote reviews, escalation path for complications.

### 1.2 Generic medical-tourism platforms (coordinator / provider side)
Same source.
- Lead pipeline with ownership, ageing and escalation for stalled cases.
- Case file combining records, correspondence and quotes.
- Travel coordination: visas, flights, accommodation, transfers, interpreters (many platforms start manual).
- Reminders tied to treatment dates; templated multilingual messages.
- Full audit log of patient data access; role-based permissions.

### 1.3 Ayurveda clinic software (India)
Source: [DoctorsApp, Ayurvedic clinic software](https://www.doctorsapp.in/emr/best-clinic-management-software-for-ayurvedic-practices)
- Modules for Panchakarma therapies and Ayurvedic prescriptions; herbal medicine tracking mentioned.
- Appointment scheduling, customisable treatment plans with progress tracking.
- Digital prescriptions; automated reminders; WhatsApp communication integration; billing.
- NOT found on that page: prakriti, nadi, diet planning. Patient app is referenced with little detail.
- Other Ayurveda software exists (AyurGrid, M-Techsoft; search hits only, not read).

### 1.4 Patient-journey management (non-Ayurveda)
Source: [EngagedMD](https://www.engagedmd.com/blog/engagedmd-expands-patient-journey-management-suite-establishing-one-platform-for-the-entire-patient-journey)
- Intake questionnaires, patient education before consults, digital signing, task management.
- Page does NOT describe status dashboards or referral lineage. Not verified.

### 1.5 Search hits seen but not read (candidate follow-ups)
Cross Border Care (aiir.in), Welltara case study (appsquadz), qmed referral hub, Attelia health tour app, Medical Tourism CRM (marketmuscles).

## 2. Regulation and policy

### 2.1 Ayush (AY) visa
Source: [Indian Consulate Edinburgh, Ayush visa](https://www.cgiedinburgh.gov.in/page/ayush-ay-visa/)
- For foreigners travelling for Ayush-system treatment, including wellness and Yoga. Main applicant AY-1, attendants AY-2.
- Needs a supporting letter from an accredited Ayush institution (not for wellness-only visits) plus prescription/medical history stamped by an accredited hospital in the home country.
- Treating facility must be accredited and registered, or NABH / NCH / NCISM accredited.
- Max two attendants at a time; AY-2 is co-terminus with AY-1.
- Can be applied via paper process or e-visa portal. Validity period NOT stated on that page.
- Another source says 123 regular Ayush and 221 e-Ayush visas were issued in one year ([IANS](https://ianslive.in/123-regular-ayush-221-e-ayush-visas-issued-to-foreigners-in-1-year-centre--20241210173305)); snippet only, not verified.
- APP IMPLICATION: the app should generate or store the supporting/invitation letter and track visa status per patient and attendant.

### 2.2 DPDP Act and Rules (India)
Source: [KPMG, DPDP in healthcare](https://assets.kpmg.com/content/dam/kpmgsites/in/pdf/2025/12/the-privacy-prescription-impact-of-dpdp-act-and-rules-in-healthcare-and-life-sciences-sector.pdf.coredownload.pdf)
- Explicit, informed consent required; blanket or implied consent invalid; consent should be revocable.
- Patients can access, correct and erase data.
- Data minimisation and purpose limitation.
- Breach reporting within 72 hours.
- DPO and impact assessments for high-risk processing; extra duties for large entities.
- Exemptions for medical emergencies.
- Document does NOT cover retention periods, notice wording, or cross-border transfer rules. Needs legal review.

### 2.3 GDPR (European patients)
Source: [GDPR Article 49 text](https://gdpr-text.com/en/read/article-49/)
- Where no adequacy decision or safeguard applies, a transfer to a third country can rest on the data subject's explicit consent, given after being told the risks, or on necessity for a contract or pre-contractual steps the patient requested. "Necessary" is read strictly.
- The page sets no special conditions for health data under Art. 49.
- Takeaway for the app: capture explicit, versioned, timestamped consent that names the transfer to India and its risks, at onboarding; keep a log. Whether a clinic in India has other obligations (e.g. EU representative) was NOT established. Needs legal advice.

### 2.3b Hosting and data residency (Supabase)
Source: [Supabase GDPR guide](https://supabase.com/docs/guides/security/gdpr-compliance)
- Supabase says it supports building GDPR-compliant apps; responsibility is shared. A project sits in one primary region (database, auth, storage).
- Choosing a region is a data-location control only; it does not make the app compliant. Backups, logs, exports, Edge Functions and sub-processors affect residency.
- A Data Processing Agreement is available on request.
- HIPAA is on a separate Supabase page (not read). Not relevant to India or EU directly.
- Decision needed: which region (India vs EU) given patients come from Europe and the clinic is in Pune.

### 2.3c WhatsApp Business API
Source: [Baat.ai pricing explainer](https://baat.ai/blog/whatsapp-api-pricing-india)
- Meta bills per delivered template message since 1 July 2025; categories: marketing (highest), utility, authentication.
- Customer messages to the business are never charged. Replies within the 24-hour service window are free for the first 1,000 per number each month; after that, India utility rate applies. Exact INR rates are not printed on that page; check Meta's pricing page.
- Opt-in and template approval rules were NOT covered; check Meta documentation.
- App implication: automated reminders (medication, check-in prompts) would be utility templates and cost per message; plan a budget. Clinic-initiated check-ins could also be sent as in-app push or email to avoid cost, with WhatsApp as a nudge.

### 2.4 ABDM / Ayush Grid
- Named in the WAC deck as a policy tailwind. Not yet researched. Follow-up needed before promising alignment.

## 3. Gaps found (opportunity for this app)
1. Generic platforms are marketplace-style (many hospitals, commissions). This clinic needs single-clinic, relationship-based care.
2. Ayurveda clinic software focuses on in-clinic OPD, not the international journey (visa, pickup, stay, remote follow-up).
3. Few products unify enquiry lineage, assessment log, travel logistics, daily care and post-departure loop in one record.
4. Nothing found that treats WhatsApp as the front door and logs it into a record (the clinic's real behaviour).

## 4. Open research items
- Legal advice: GDPR obligations of an India-based clinic with EU patients; DPDP notice wording, retention.
- Vercel compliance posture for health data (not researched; Supabase partly done above).
- WhatsApp Business API: opt-in rules, template approval, whether inbound messages can be logged into the record.
- ABDM / Ayush Grid integration feasibility.
- Ayurveda records: prakriti, nadi, Panchakarma protocol structures (domain input from the doctor needed).
- Payments for international patients.


---

# C. Application blueprint

# Application Blueprint: Ayurvedic Clinic Patient Journey App

Status: DRAFT for Ravi's phase-by-phase review. No code written. Built in parts so nothing is lost.
Legend: **[DECIDED]** = Ravi said it. **[PROPOSED]** = Claude's suggestion, needs Ravi's yes/no. **[OPEN]** = question to resolve.

---

## Part 1. Concept, users, principles

### 1.1 One-line concept [DECIDED]
A single web app (installable to the phone home screen) that gives one Ayurvedic clinic a single source of truth for each international patient's journey, from first enquiry to repeat visits, and gives the patient one place to see their plan.

### 1.2 Problem [DECIDED]
Communication runs on WhatsApp, email and phone. Records, travel plans and medical history are scattered. Patients juggle channels and can lose vital information.

### 1.3 Design principles [PROPOSED]
1. **Do not replace the front door.** First contact, assessment calls and quotations stay on WhatsApp / email / phone. The app captures the outcome and the lineage. (Matches Ravi's Enquiry and Assessment decisions.)
2. **One record per patient, for life.** Repeat visits add a new "episode" to the same record; nothing resets.
3. **Clinic enters, patient sees.** Default is clinic-entered, patient read-only. Exceptions are explicit (flight details, check-ins, documents).
4. **Physician stays in charge.** The app records and reminds; it never gives clinical advice by itself. (Same stance as the WAC deck.)
5. **Low-friction for patients.** Link-based access, no install needed, works on a phone, simple English first.
6. **Consent and audit by default.** Every access to a patient's record is logged.

### 1.4 Roles [PROPOSED, extends the decided clinic/patient split]
| Role | Who | Can do |
|---|---|---|
| Patient | The traveller | See own plan, upload documents, enter flight details, answer check-ins, message the clinic |
| Attendant (optional) | Family member travelling (Ayush visa allows up to two) | View-only access to the patient's logistics if the patient grants it |
| Front desk / coordinator | Clinic operations | Onboard patients, log enquiries and quotations, enter travel, pickup, stay |
| Doctor | Physician | Log assessments, doctor's notes, prescriptions, review check-ins |
| Therapist / kitchen (optional) | Panchakarma and diet teams | View daily schedule; record therapy given and meals served |
| Admin | Clinic owner / IT | Manage users, templates, audit log, consent text |

[OPEN] Do therapists and the kitchen need logins, or does the coordinator enter on their behalf for the first version?

### 1.5 Platform [DECIDED]
Web app, installable to home screen (PWA), Next.js on Vercel with Supabase (database, auth, storage), same stack as Invento. One codebase, role-based views.

---

## Part 2. The patient record (the heart of the app) [PROPOSED]

One **Patient** has many **Episodes** (one per visit/treatment cycle). Each Episode moves through the six phases. A returning patient starts a new Episode at Assessment or Planning (DECIDED), skipping Enquiry.

Patient (permanent): identity, contact, nationality, DOB, passport number, emergency contact, photo, language, consent history, prior medical records, documents.
Episode (per visit): enquiry log, quotation(s), assessment log, plan, travel, stay, daily care entries, check-ins, post-departure follow-ups, consultations.

Phase status per Episode: Enquiry → Assessment → Planning → Arrival → Care → Continuity. Staff can move a patient forward or back; every change is logged.

---

## Part 3. Phase by phase

For each phase: what happens today, what the app adds, who enters what, who sees what, and open questions.

### Phase 0. Onboarding (a screen/flow, not a phase) [DECIDED + PROPOSED]
Triggered when an enquiry turns serious (Ravi: patient is "onboarded into the app").
- Mandatory: name, email, phone, nationality. [DECIDED]
- Optional but captured: photo, date of birth, passport number, emergency contact. [DECIDED]
- Optional uploads: passport scan, previous medical records. [DECIDED]
- [PROPOSED] Preferred language, time zone, dietary preferences, attendant details (name, relation, passport).
- [PROPOSED] On creation the app sends the patient an invite link (email and WhatsApp) to set a password or use a one-time link.
- [OPEN, parked by Ravi] Where consent is captured: at onboarding (suggested) or later when the programme and payment are confirmed. Claude's suggestion stands: capture at onboarding, since documents and medical records are uploaded here.

### Phase 1. Enquiry [DECIDED]
Today: patient writes on WhatsApp / email / phone; clinic replies with information and quotation on the same channels; nothing logged centrally.
App: clinic logs the enquiry and quotation after the fact so lineage is kept.
- Enquiry log entry: date, channel (WhatsApp / email / phone / other), what was asked (treatment interest, condition, dates), who handled it, free-text summary, attachments (screenshot or file).
- Quotation entry: version number, date sent, amount and currency, what it includes and excludes, validity date, status (sent / accepted / revised / lapsed), file attachment.
- [PROPOSED] Enquiry source field (referral, website, event such as the Congress, repeat) for later reporting.
- [PROPOSED] "Lead without record" list so staff can see enquiries not yet onboarded and follow up.
- Patient sees: nothing until onboarded, then their enquiry history and quotations read-only.

### Phase 2. Assessment [DECIDED]
Today: Nadi Pariksha in person when the doctor is on a foreign trip; otherwise a remote assessment over WhatsApp call. Kept as is.
App: logs how and what.
- Assessment entry: date, method (in person / WhatsApp call / phone / video / email), doctor, findings, outcome (e.g. advised to visit India, medicines for N months, further tests), attachments.
- [PROPOSED] Structured fields to be agreed with the doctor (e.g. prakriti, pulse findings, chief complaint) alongside free text. Ayurveda-specific fields could not be confirmed from public software pages; the doctor should define them.
- [PROPOSED] Medicines prescribed at this stage logged with start date and duration, so they feed the check-in loop even before travel (Petra took about three months of medicines before coming).
- Patient sees: summary of outcome and advice, doctor's choice (clinic can mark entries "private" for internal notes).

### Phase 3. Planning [DECIDED + PROPOSED]
Decided: a wider/preliminary programme and approximate cost are settled before travel; doctor may refine on arrival.
- Plan: programme name, intended duration, treatments included, diet approach, status (provisional / confirmed / refined on arrival), approximate cost, link to the accepted quotation.
- [PROPOSED] Pre-arrival checklist (visa, documents, vaccines if any, payment, flight details, attendant details), each with owner (patient or clinic) and status.
- [PROPOSED] Visa tracker per traveller: type (Ayush AY-1 for the patient, AY-2 for attendants, up to two), supporting-letter generated or uploaded, application status, expiry. Source: the Edinburgh consulate page lists the accredited-institution letter and attendant rules.
- [PROPOSED] Pre-arrival information pack (what to bring, weather, diet before arrival, airport and transfer info) in the patient's language, delivered in the app. The WAC deck lists a templated multilingual pack as a pilot idea.
- [PROPOSED] Pre-arrival Q&A thread: Petra had nine questions; keep them in one threaded place rather than scattered.
- [OPEN] Payments: deposit and balance in the app, or only recorded manually? International card payments add compliance work; first version could just record payments received.
- [OPEN, parked] Consent timing (see onboarding).

### Phase 4. Arrival [DECIDED]
- Flight details (flight number, arrival time, airport, terminal): entered by clinic or patient. [DECIDED]
- Pickup: car, driver name, phone, plate, pickup point and time, entered by clinic, visible to patient. [DECIDED]
- Accommodation and check-in details: entered by clinic. [DECIDED]
- [PROPOSED] Mumbai-to-Pune transfer leg handled as a second pickup item (Petra's story included a Mumbai Airport to Pune transfer).
- [PROPOSED] "Arrival day card" on the patient home screen: flight status, who is meeting you, where, phone number, what happens next.
- [PROPOSED] One-tap "I have landed" and "I need help" buttons for the patient; alerts the coordinator.
- [PROPOSED] Flight changes: if the patient edits the flight, the coordinator is notified so pickup can change.

### Phase 5. Care (in treatment) [DECIDED]
Clinic-entered, patient-visible:
- Post-arrival assessment findings, doctor's notes, prescribed medication, daily treatments given, daily diet, daily accommodation/stay details. [DECIDED]
Daily check-ins [DECIDED]: whether the patient is taking medicines, and how the treatment is going.
- [PROPOSED] Day view for the patient: today's schedule (therapies with times), today's diet (meals), today's medicines with tick boxes, today's doctor review time.
- [PROPOSED] Check-in form kept short (under a minute): medicines taken yes/no, energy/sleep/appetite on a simple scale, "anything to tell the doctor", optional photo.
- [PROPOSED] A "flag" if the patient reports something concerning; shows in the doctor's queue.
- [PROPOSED] Therapy record per session: therapy, therapist, duration, notes.
- [PROPOSED] Doctor's daily review log tied to the check-in answers.
- [OPEN] Which signals count as "concerning" must be defined by the doctor, not by the app.

### Phase 6. Continuity (departure and after) [DECIDED]
- Departure travel assistance (drop-off, flight home) logged. [DECIDED]
- Post-departure diet and medication follow-ups as an interactive loop. [DECIDED]
- Check-ins are clinic-initiated and scheduled. [DECIDED]
- Log of WhatsApp / phone consultations given after the patient is home. [DECIDED]
- Record persists for repeat visits. [DECIDED]
- [PROPOSED] Follow-up schedule builder: the doctor picks a template (e.g. weekly for 4 weeks, then monthly), and the app creates the prompts.
- [PROPOSED] Medicine supply tracker (Petra received about three months of medicines at a time): shows when a supply runs out so the clinic can reorder.
- [PROPOSED] Return-visit nudge: after N months, prompt the coordinator to reach out (Petra returned after a year).
- [PROPOSED] Feedback form at the end of the programme (the WAC deck lists this as a pilot item).

---

## Part 4. Data model (conceptual, no code) [PROPOSED]

| Entity | Key fields | Notes |
|---|---|---|
| User | id, role, name, email, phone, language | Login identity (Supabase Auth) |
| Patient | user link, nationality, DOB, passport no., emergency contact, photo, dietary prefs | Permanent |
| Attendant | patient link, name, relation, passport, visa status | Up to two per episode |
| Episode | patient, phase, start/end dates, primary doctor, source | One per visit |
| Enquiry | episode, date, channel, summary, attachments, handled by | Logged after the fact |
| Quotation | episode, version, amount, currency, inclusions, validity, status, file | Versioned |
| Assessment | episode, date, method, doctor, findings, outcome, attachments | |
| Plan | episode, programme, duration, treatments, diet approach, status, approx. cost | Provisional → confirmed → refined |
| ChecklistItem | episode, title, owner, status, due date | Pre-arrival tasks |
| TravelLeg | episode, type (inbound flight / transfer / outbound), flight no., times, airport, entered by | Patient or clinic can enter |
| Pickup | travel leg, driver, car, plate, phone, point, time | Clinic-entered |
| Stay | episode, place, room, check-in/out, per-day location | Daily accommodation |
| DailyPlan | episode, date, therapies, meals, medicines, doctor review | The day view |
| TherapyRecord | daily plan, therapy, therapist, duration, notes | |
| DoctorNote | episode, date, author, text, visibility | Private vs patient-visible |
| Medication | episode, name, dose, schedule, start, duration, supply end | Feeds check-ins |
| CheckIn | episode, date, medicines taken, scores, free text, photo, flag | Clinic-scheduled |
| Consultation | episode, date, channel (WhatsApp / phone / video), doctor, summary | Post-departure log |
| Document | owner, type, file, uploaded by, visibility | Passport, reports, letters |
| Consent | patient, version, text, timestamp, scope, withdrawn at | Versioned, revocable |
| AuditLog | who, what, when, record | Every view/change |
| Message | episode, sender, text, attachments | In-app thread |
| Notification | recipient, channel, template, sent at, status | |

Storage: documents in Supabase Storage with row-level access rules; patients see only their own records; staff see by role.

## Part 5. Notifications and channels [PROPOSED]

Principle: meet people where they already are, but keep the truth in the app.
- **In-app inbox and web push** for installed home-screen users (works on Android Chrome; behaviour on iPhone depends on installation to the home screen, to be verified at build time).
- **Email** for invites, documents and summaries.
- **WhatsApp** as a nudge ("You have a new check-in") rather than the place where answers are typed, to keep records structured. Costs: Meta bills per delivered template; replies in the 24-hour window are free for the first 1,000 per number per month. Budget needed.
- Reminder types: check-in due, medicine due, pickup details updated, document requested, visa checklist item due, quotation expiring, follow-up due, supply running out.
- Clinic-side alerts: patient flagged a concern, patient landed / needs help, flight changed, document uploaded, check-in overdue.
- Quiet hours by patient time zone.
- [OPEN] Should clinic staff be able to send WhatsApp from inside the app, or only log WhatsApp conversations manually? Sending requires the WhatsApp Business API and approved templates.

## Part 6. Privacy, consent, security [PROPOSED; legal review needed]

- **Consent**: explicit, versioned, timestamped, revocable; covers use of medical history, storage, and transfer to India for EU patients. DPDP guidance says blanket or implied consent is invalid. GDPR Art. 49 allows transfer on explicit consent after the risks are explained. [Needs a lawyer to confirm for this clinic.]
- **Access**: role-based; patients see only their own record; doctor's private notes hidden from patients; every view logged.
- **Data rights**: export, correct and erase on request (DPDP rights). Build admin tools for this early.
- **Breach readiness**: DPDP guidance cited a 72-hour reporting window; keep an incident procedure.
- **Minimisation**: only collect what the journey needs; passport scans retained only as long as visa/travel requires.
- **Hosting**: Supabase single primary region; backups and logs can cross regions. [OPEN] India vs EU region; Supabase offers a DPA.
- **Security basics**: encryption in transit and at rest, MFA for staff, short sessions on shared devices, signed URLs for files.
- **Clinical boundary**: the app does not give medical advice or diagnoses; flags go to the doctor.
- Governance: appoint someone responsible for data protection at the clinic; keep a record of processing.

## Part 7. Roadmap and open questions

### 7.1 Suggested build order [PROPOSED]
Ravi's earlier voice suggestion was to start with the daily-use core. Claude's suggested slices (each demoable on its own):
1. **Foundation**: login, roles, patient list, onboarding screen, documents, audit log, consent capture.
2. **Arrival + Care**: travel/pickup/stay entries, day view, daily check-ins. (Highest daily use.)
3. **Enquiry + Assessment + Planning**: logs, quotation versions, plan, checklist, visa tracker.
4. **Continuity**: scheduled follow-ups, consultation log, supply tracker, return nudges, feedback.
5. **Polish**: notifications via WhatsApp/email, multilingual pack, reporting.

### 7.2 Success measures [PROPOSED]
- Share of active patients with a complete record.
- Time for staff to find a patient's travel / medicine info.
- Check-in response rate during Care and Continuity.
- Fewer "where is my pickup?" style messages on WhatsApp.
- Repeat-visit conversion tracked from the record.

### 7.3 Open questions for Ravi (ranked)
1. Is the clinic Ayurvedgram, Pune? (Decides real terms and stages.)
2. Who at the clinic will enter data daily, and on what device?
3. Do therapists and kitchen need logins in v1?
4. Consent timing and wording (parked) and who approves it legally.
5. Hosting region: India or EU?
6. Payments in the app, or record only?
7. Languages needed beyond English for the patient side?
8. Should staff send WhatsApp from the app (needs WhatsApp Business API)?
9. What does the doctor consider a "flag" in check-ins?
10. Who is the doctor sponsor who will review Ayurveda-specific fields?

### 7.4 Risks
- Staff adoption: if entering data feels like double work, the app fails. Mitigation: very short forms, templates, bulk entry for daily plans.
- Patient adoption: older or non-technical patients. Mitigation: link-based access, large text, optional attendant access.
- Compliance gaps (GDPR/DPDP) before real patient data is stored. Mitigation: legal review before go-live; use dummy data in the prototype.
- Over-claiming: do not call features "piloting" in public material until they are (WAC deck risk #1).


---

# D. Mockups (text wireframes)

# Mockups (low-fidelity wireframes, text form)

Status: DRAFT. These are layout sketches for review, not designs and not code. All names and data are invented dummy data (not real patients).
A visual HTML version of the same screens is produced separately; this file is the durable fallback.

Screens covered: C1 Clinic patient list, C2 Onboard new patient, C3 Patient record (clinic view), P1 Patient home, P2 Patient day view and check-in.

---

## C1. Clinic: patient list (home screen for staff)

```
┌─────────────────────────────────────────────────────────────┐
│ ☰  Ayurveda Clinic            🔍 Search         [+ Onboard] │
├─────────────────────────────────────────────────────────────┤
│ Needs attention (3)                                         │
│  ⚠ Anna K.  – flagged: poor sleep (Day 6)       [Open]      │
│  ✈ Marc D.  – flight changed, pickup to update  [Open]      │
│  ⏰ Lena S.  – check-in overdue 2 days           [Open]      │
├─────────────────────────────────────────────────────────────┤
│ Filter: [All] Enquiry Assess Plan Arrival Care Continuity   │
├─────────────────────────────────────────────────────────────┤
│ Anna K.   🇦🇹 Austria   ● CARE        Day 6 of 14   Dr. A   │
│ Marc D.   🇩🇪 Germany   ● ARRIVAL     lands Fri 14:35       │
│ Lena S.   🇨🇭 Switz.    ● CONTINUITY  week 3 follow-up      │
│ John P.   🇬🇧 UK        ● PLANNING    visa pending (AY-1)   │
│ Sofia R.  🇪🇸 Spain     ● ASSESSMENT  call booked Mon       │
│ Tom H.    🇺🇸 USA       ○ ENQUIRY     quote sent 3 days ago │
└─────────────────────────────────────────────────────────────┘
```
Notes: status chip = current phase. "Needs attention" is computed from flags, overdue check-ins, travel changes. Filter chips match the six phases.

---

## C2. Clinic: onboard a new patient

```
┌─────────────────────────────────────────────────────────────┐
│ ←  Onboard new patient                          Step 1 of 3 │
├─────────────────────────────────────────────────────────────┤
│ Required                                                    │
│  Full name *        [ ______________________ ]              │
│  Email *            [ ______________________ ]              │
│  Phone *            [ +__ ___________________ ]             │
│  Nationality *      [ Select country  ▾ ]                   │
│                                                             │
│ Optional (captured when available)                          │
│  Photo              [ Upload ]                              │
│  Date of birth      [ DD / MM / YYYY ]                      │
│  Passport number    [ ______________________ ]              │
│  Emergency contact  [ name ______ phone ______ ]            │
│  Preferred language [ English ▾ ]                           │
│                                                             │
│ Documents (optional)                                        │
│  Passport scan      [ Upload ]                              │
│  Previous medical records   [ Upload (multiple) ]           │
│                                                             │
│ Link existing history (optional)                            │
│  [ + Add enquiry notes / quotation already sent ]           │
│                                                             │
│                       [ Save draft ]   [ Next: Consent → ]  │
└─────────────────────────────────────────────────────────────┘
```
Notes: Steps 2 and 3 (proposed): consent capture, send invite link by email/WhatsApp. Consent timing is parked by Ravi; shown here as a proposal only.

---

## C3. Clinic: patient record (tabs follow the six phases)

```
┌─────────────────────────────────────────────────────────────┐
│ ←  Anna K.   🇦🇹  ● CARE (Day 6/14)     Episode 1  ▾        │
│ Dr. A • Stay: Room 12, Guest House • [Message] [Add entry ▾]│
├─────────────────────────────────────────────────────────────┤
│ Enquiry│Assessment│Planning│Arrival│ CARE │Continuity│Docs  │
├─────────────────────────────────────────────────────────────┤
│ Today – Fri 17 Oct                                          │
│  Therapies   07:30 Abhyanga (Therapist M)  ☑ done           │
│              10:00 Shirodhara              ☐                │
│  Diet        Breakfast: kitchari ☑  Lunch: ☐  Dinner: ☐     │
│  Medicines   Morning ☑ taken   Evening ☐                    │
│  Doctor      Review 17:00                                   │
│                                                             │
│ Today's check-in (from patient)                             │
│  Medicines taken: Yes   Sleep: 2/5 ⚠   Appetite: 4/5        │
│  Note: "Slept badly, felt warm after treatment"             │
│  [ Mark reviewed ]   [ Add doctor note ]                    │
│                                                             │
│ Earlier days ▸ Day 5 │ Day 4 │ Day 3 │ …                    │
└─────────────────────────────────────────────────────────────┘
```
Notes: "Add entry" menu offers: enquiry, quotation, assessment, plan item, flight/pickup/stay, therapy record, doctor note, medicine, consultation, document.

---

## P1. Patient: home screen (arrival-day state)

```
┌───────────────────────────────┐
│  Welcome, Marc                │
│  Your journey: ● ● ● ◐ ○ ○    │
│  Enquiry Assess Plan [Arrive] │
├───────────────────────────────┤
│ ✈ Arriving today              │
│  Flight LX 148  → Mumbai      │
│  Lands 14:35   Terminal 2     │
│  [ I have landed ]            │
│                               │
│ 🚗 Who is meeting you         │
│  Driver: Ramesh               │
│  Car: white Innova MH12 ••••  │
│  📞 +91 •••••  [ Call ]       │
│  Meeting point: Arrivals,     │
│  holding a sign with your name│
│                               │
│ 🏡 Where you will stay        │
│  Guest House, Baner, Pune     │
│  Check-in after 18:00         │
│                               │
│ [ Need help? ]  [ Messages ]  │
├───────────────────────────────┤
│ Home │ Plan │ Docs │ Messages │
└───────────────────────────────┘
```
Notes: Same screen after arrival becomes Today's plan. Flight details can be edited by the patient (DECIDED).

---

## P2. Patient: day view and check-in (Care phase)

```
┌───────────────────────────────┐
│  Day 6 of 14  •  Fri 17 Oct   │
├───────────────────────────────┤
│ Today's plan                  │
│  07:30  Abhyanga        ✓     │
│  10:00  Shirodhara            │
│  17:00  Doctor review         │
│                               │
│ Meals                         │
│  Breakfast  kitchari   ✓      │
│  Lunch      khichdi with …    │
│  Dinner     light soup …      │
│                               │
│ Medicines                     │
│  Morning  ☑ taken             │
│  Evening  ☐ not yet           │
├───────────────────────────────┤
│ Daily check-in (1 minute)     │
│  Did you take all medicines?  │
│   (Yes) (No) (Partly)         │
│  How did you sleep? ① ② ③ ④ ⑤ │
│  How is your appetite? ① … ⑤  │
│  How is the treatment going?  │
│   (Good) (OK) (Not well)      │
│  Anything for the doctor?     │
│  [ type or speak … ]          │
│            [ Send ]           │
├───────────────────────────────┤
│ Home │ Plan │ Docs │ Messages │
└───────────────────────────────┘
```
Notes: after departure, the same check-in appears on the schedule the clinic sets (DECIDED: clinic-initiated). The app never interprets answers medically; "Not well" or low scores raise a flag to the doctor.

---

## More Care and Departure screens (visual versions are in 04_mockups.html)

### C4. Clinic: build tomorrow's plan (Care)
```
┌─────────────────────────────────────────────────────────────┐
│ Anna K. • Day 7  ● CARE     Sat 18 Oct (draft)  [Copy yday] │
├─────────────────────────────────────────────────────────────┤
│ Therapies                     │ Meals (doctor's diet plan)  │
│  07:30 Abhyanga  Therapist M  │  Breakfast  kitchari        │
│  10:00 Shirodhara Therapist R │  Lunch      moong dal, rice │
│  [+ Add therapy]              │  Dinner     light soup      │
│ Doctor review                 │ Medicines                   │
│  17:00 Dr. A, in person       │  Morning  Medicine 1 (dummy)│
│                               │  Evening  Medicine 2 (dummy)│
│ Stay today: Guest house, room 12                            │
│                       [ Save draft ]  [ Publish to patient ]│
└─────────────────────────────────────────────────────────────┘
```

### C5. Clinic: doctor's review queue (Care)
```
┌─────────────────────────────────────────────────────────────┐
│ Anna K.  Day 7 sleep 2/5       ⚠ Flagged  "Slept badly..."  │
│ Pierre L. Day 3 partly taken   ⚠ Flagged  "Missed evening.."│
│ Sara W.  Day 10 all good       ✓ Reviewed                   │
├─────────────────────────────────────────────────────────────┤
│ Anna K. note: [ ______________________________ ]            │
│ (• Share with patient  ○ Private)  [Change medicine] [Save] │
└─────────────────────────────────────────────────────────────┘
```

### P3. Patient: doctor's notes and medicines (Care)
```
┌───────────────────────────────┐
│ My care • Day 7               │
├───────────────────────────────┤
│ From Dr. A today              │
│  "Rest this afternoon. Warm   │
│   water through the day."     │
│ My medicines                  │
│  Medicine 1  morning, before  │
│  Medicine 2  evening, after   │
│  Course until 31 October      │
│ Diet guidance                 │
│  Warm, light, fresh food      │
│ [ Ask the clinic a question ] │
├───────────────────────────────┤
│ Home │ Plan │ Docs │ Messages │
└───────────────────────────────┘
```

### D1. Clinic: plan departure and follow-up (Departure)
```
┌─────────────────────────────────────────────────────────────┐
│ Travel home                   │ Documents to hand over      │
│  Fri 31 Oct • OS 118 02:05    │  Prescription + med list ✓  │
│  Pickup 22:30, Ramesh         │  Diet guidance for home  ✓  │
│  Flight entered by: Patient   │  Treatment summary  doctor  │
│                               │  Feedback form  sent on day │
├─────────────────────────────────────────────────────────────┤
│ Follow-up schedule: (• Weekly x4 then monthly) ○ Fortnightly│
│  Check-ins Mondays 09:00 patient's time • Call week 2       │
│  Medicine supply: 3 months, runs out about 31 Jan           │
│                    [ Save draft ]  [ Confirm, start follow-up ]│
└─────────────────────────────────────────────────────────────┘
```

### D2. Patient: departure day
```
┌───────────────────────────────┐
│ Safe travels, Anna            │
│ ●●●●● ◐  Enq…Care  [Home]     │
│ Your trip home                │
│  Pickup 22:30  Flight 02:05   │
│ Take with you                 │
│  Prescription • Diet • Summary│
│ What happens next             │
│  Weekly check-ins from Mon 3  │
│ [ Share your feedback ]       │
└───────────────────────────────┘
```

### D3. Patient: weekly check-in at home (Continuity)
```
┌───────────────────────────────┐
│ Weekly check-in • week 2      │
│ Medicines taken as advised?   │
│  (Yes) (Partly) (No)          │
│ Diet working at home?         │
│  (Easy) (Some difficulty) (Hard)│
│ Energy this week ① ② ③ ④ ⑤    │
│ Anything for the doctor? […]  │
│ [ Send ]                      │
│ Next: video call Thu 13 Nov   │
│ [ Ask to reschedule ]         │
└───────────────────────────────┘
```

### D4. Clinic: Continuity tab
```
┌─────────────────────────────────────────────────────────────┐
│ Anna K.  ● CONTINUITY week 6   [Log consultation][New episode]│
├─────────────────────────────────────────────────────────────┤
│ Sleep by week:  2 2 3 4 4 5  (bars)   │ Consultations       │
│ Medicine supply: ▓▓▓▓▓░░░ ~6 wks left │  13 Nov WhatsApp vid│
│ Reorder prompt: early January         │  27 Nov Phone call  │
│                                       │  11 Dec Message     │
│                                       │ Return nudge: Sep 27│
└─────────────────────────────────────────────────────────────┘
```

---

## Review checklist for Ravi
- Does C1's "needs attention" list match what the coordinator would check first each morning?
- C2: is a 3-step flow (details, consent, invite) right, or one page?
- C3: tab order follows the six phases; should Docs be a separate tab?
- P1: is arrival-day info complete? (Missing ideas: SIM/payment advice, emergency number.)
- P2: is the 5-question check-in the right length for daily use?


---

# E. Design decisions and pending decisions

# Design decisions, status and pending decisions

Last updated 2026-10-17. Status key: **LOCKED** = Ravi decided. **DIRECTION OK** = shown to Ravi, he said "this is good" about the mockup set, but details were not confirmed one by one. **PROPOSED** = Claude's suggestion, not yet answered. **PARKED** = Ravi deferred it.

## 1. Product and scope decisions

| # | Decision | Status |
|---|---|---|
| 1 | Clinic is the customer; patients are onboarded into the app | LOCKED |
| 2 | First deployment is one specific clinic, not a multi-clinic platform | LOCKED |
| 3 | One app, role-based logins for clinic staff and patients, one shared backend and patient record | LOCKED |
| 4 | Web app first, installable to the home screen of patient and clinic phones; native later only if needed | LOCKED |
| 5 | Cloud-driven development; stack Next.js + Vercel + Supabase (as in Invento) | LOCKED |
| 6 | Six phases: Enquiry, Assessment, Planning, Arrival, Care, Continuity | LOCKED |
| 7 | First contact, quotations and assessment calls stay on WhatsApp/email/phone; the app logs and preserves lineage | LOCKED |
| 8 | Returning patients skip Enquiry and start at Assessment or Planning | LOCKED |
| 9 | Post-departure check-ins are clinic-initiated and scheduled | LOCKED |
| 10 | Flight details can be entered by clinic or patient; pickup and accommodation by clinic | LOCKED |
| 11 | Onboarding is a dedicated clinic screen with four required fields and optional extras | LOCKED |
| 12 | No coding yet; blueprint and mockups first, then review phase by phase | LOCKED |
| 13 | Consent timing and wording | PARKED |

## 2. Design decisions (look, feel, structure)

| # | Decision | Status |
|---|---|---|
| D1 | Two surfaces: desktop-style layouts for clinic screens, phone layouts for patient screens | DIRECTION OK |
| D2 | Clinic home is a patient list with a "Needs attention" block on top and phase filter chips | DIRECTION OK |
| D3 | Patient record uses tabs that mirror the six phases, plus Documents | DIRECTION OK (Documents tab is a question) |
| D4 | Patient home shows a six-step journey bar and a card for what matters today (arrival day card, day view, departure card) | DIRECTION OK |
| D5 | Daily check-in is short: medicines (Yes/Partly/No), sleep 1-5, treatment (Good/Okay/Not well), free text | DIRECTION OK (length is a question) |
| D6 | Clinic enters, patient reads; patient-editable items are flight details, check-ins, documents | LOCKED/PROPOSED mix (flight details LOCKED) |
| D7 | The app records and alerts; it never interprets answers medically. The doctor defines what counts as a flag | PROPOSED principle |
| D8 | Doctor notes can be marked "share with patient" or "private to clinic" | PROPOSED |
| D9 | Daily plan is built once per day by the coordinator with "copy from yesterday" and doctor-set templates for diet and medicines | PROPOSED |
| D10 | Departure planner: travel home, documents to hand over, follow-up schedule chosen from a doctor-set template | PROPOSED |
| D11 | Continuity tab shows a simple trend of check-in scores, medicine supply left, consultation log, return-visit nudge | PROPOSED |
| D12 | Mockups use invented dummy patients, never real patients | LOCKED rule (privacy) |

### Visual system used in the mockups
- Palette (from the WAC deck): deep green #2E5E4E (accent), leaf green #4E8B6F, gold #D4A02C (mockups use a slightly deeper #B98A1D), terracotta #B8553A, blue #3F6E8C, teal #2F7F78. Neutrals are green-tinted: page #F3F6F4, card #FFFFFF, line #D3DDD7, text #1C2B25, muted #5B6D64.
- Dark theme mirrors this: page #111A16, card #18241F, accent #7CC3A3, text #E4EEE9.
- Phase chip colours: Enquiry grey, Assessment blue, Planning gold, Arrival terracotta, Care leaf green, Continuity teal. A chip is a coloured dot plus text so it stays readable in both themes.
- Type: Literata (headings), Public Sans (body). Both from Google Fonts with system fallbacks.
- Status words: "Flagged" (amber), "Reviewed"/"Ready" (green), "Pending" (plain).
- Patient screens are phone width (about 340 px) with a four-item bottom bar: Home, Plan, Documents, Messages.

## 3. Pending decisions (ranked)

| ID | Question | Options | Claude's recommendation | Blocks |
|---|---|---|---|---|
| PD1 | Is the clinic Ayurvedgram, Pune? | Yes / another clinic | Confirm, then use its real terms and stages | Terminology, doctor review |
| PD2 | Who enters data daily and on which device? | Coordinator on phone / on desktop / both | Design for coordinator on a phone plus a desktop for the doctor | Form length, bulk entry |
| PD3 | Do therapists and kitchen get logins in v1? | Yes / coordinator enters for them | Coordinator enters for them in v1 | Roles, scope |
| PD4 | Consent timing and wording (PARKED) | At onboarding / at plan confirmation | At onboarding, versioned and timestamped, reviewed by a lawyer | Onboarding step 2, privacy |
| PD5 | Hosting region | India / EU | Decide with legal advice; Supabase offers a DPA | Setup |
| PD6 | Payments in the app? | Record only / online payments | Record only for v1 | Scope, compliance |
| PD7 | Languages for patient side | English only / add German etc. | English first; add a second language when real patients need it | Content |
| PD8 | WhatsApp: log only or send from the app? | Manual logging / WhatsApp Business API | Start with manual logging plus email and in-app prompts; add API later | Cost, build |
| PD9 | What counts as a "flag" in check-ins? | Doctor defines rules | Doctor defines (for example sleep 2 or lower, missed dose, "Not well") | Care review |
| PD10 | Which doctor defines Ayurveda-specific fields (prakriti, pulse, Panchakarma protocols)? | Named doctor | Sit with the doctor for one session | Assessment, Care forms |
| PD11 | Follow-up templates the doctor actually uses | Weekly then monthly / fortnightly / custom | Collect real examples from the doctor | Departure planner |
| PD12 | Should the patient see the whole medicine history or only the current course? | Whole / current | Current course, history on request | Patient Plan tab |
| PD13 | Documents as its own tab? | Own tab / inside each phase | Own tab | Record layout |
| PD14 | Daily check-in length | 5 questions / fewer | Keep 5, review after pilot | Adoption |
| PD15 | Can patients request an extra consultation in the app? | Yes / reply only | Yes, as a request the clinic approves | Continuity |
| PD16 | Return-visit nudge | On / off, timing | On, about 11 months for a yearly visitor, coordinator can change | Continuity |
| PD17 | Attendant access (up to two travel companions on an Ayush visa) | View-only logistics / none | View-only logistics if the patient grants it | Roles |
| PD18 | Data retention and erasure rules (passport scans, medical records) | Define periods | Legal advice first | Privacy |
| PD19 | Build order | Foundation then Arrival + Care first / Enquiry first | Foundation, then Arrival + Care, then Enquiry/Assessment/Planning, then Continuity | Roadmap |
| PD20 | Does Ravi want the WAC deck statements about the app updated once decisions land? | Yes / no | Confirm, and keep "Proposed" wording until something is in use | Presentation accuracy |

## 4. Research gaps that affect decisions
- GDPR obligations of an India-based clinic with EU patients: not established; needs a lawyer.
- DPDP: notice wording and retention not covered by sources read.
- WhatsApp Business API opt-in and template approval rules: not covered.
- ABDM and Ayush Grid integration: not researched; do not promise alignment.
- Vercel compliance posture for health data: not researched.
- iPhone web push behaviour for installed web apps: to verify at build time.

## 5. Change log
- 2026-10-15: voice sessions defined six phases, onboarding fields, stack. Memory file updated.
- 2026-10-16: research, blueprint (7 parts), five-screen mockup set, then expanded to twelve screens (added Care and Departure/Continuity).
- 2026-10-17: master markdown file, this decisions log, and a handoff document created.


---

# F. Visual mockups: HTML source (12 screens)

Save the block below as a .html file to open it in a browser, or publish it as an artifact. Self-contained; fonts load from Google Fonts with fallbacks.

```html
<title>Ayurveda Journey App Mockups</title>
<meta name="claude:viewport-fit-sides" content="cover">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Literata:opsz,wght@7..72,500;7..72,700&family=Public+Sans:wght@400;500;600&display=swap">
<style>
/* Layout: a review sheet. Intro band, then each screen in its own device frame, clinic screens in desktop frames, patient screens in phone frames. */
:root{
  --bg:#f3f6f4; --surface:#ffffff; --surface-2:#eaf0ec; --line:#d3ddd7;
  --fg:#1c2b25; --muted:#5b6d64; --accent:#2e5e4e; --accent-fg:#ffffff;
  --gold:#b98a1d; --terra:#b8553a; --blue:#3f6e8c; --teal:#2f7f78; --grey:#7c8a83; --leaf:#4e8b6f;
  --warn-bg:#fbefd0; --warn-fg:#6b4a05; --alert-bg:#f8dfd6; --alert-fg:#7a2d18;
  --ok-bg:#dcebe2; --ok-fg:#1f4a38;
  --display:'Literata',Georgia,serif; --body:'Public Sans',system-ui,sans-serif;
}
@media (prefers-color-scheme: dark){:root:not([data-theme="light"]){
  --bg:#111a16; --surface:#18241f; --surface-2:#203029; --line:#2f4339;
  --fg:#e4eee9; --muted:#9bb0a6; --accent:#7cc3a3; --accent-fg:#0d1c15;
  --gold:#e0b84f; --terra:#e58b6f; --blue:#7fb0cf; --teal:#6dc2ba; --grey:#98a79f; --leaf:#86c7a6;
  --warn-bg:#3a3012; --warn-fg:#f2dc9a; --alert-bg:#43231a; --alert-fg:#f4c3b2;
  --ok-bg:#1f3a2e; --ok-fg:#bfe4d0; color-scheme:dark}}
:root[data-theme="dark"]{
  --bg:#111a16; --surface:#18241f; --surface-2:#203029; --line:#2f4339;
  --fg:#e4eee9; --muted:#9bb0a6; --accent:#7cc3a3; --accent-fg:#0d1c15;
  --gold:#e0b84f; --terra:#e58b6f; --blue:#7fb0cf; --teal:#6dc2ba; --grey:#98a79f; --leaf:#86c7a6;
  --warn-bg:#3a3012; --warn-fg:#f2dc9a; --alert-bg:#43231a; --alert-fg:#f4c3b2;
  --ok-bg:#1f3a2e; --ok-fg:#bfe4d0; color-scheme:dark}
*{box-sizing:border-box}
body{background:var(--bg);color:var(--fg);font-family:var(--body);font-size:14px;line-height:1.45;
  padding-left:max(16px,env(safe-area-inset-left,0px));padding-right:max(16px,env(safe-area-inset-right,0px));padding-block:28px 48px}
.wrap{max-width:1120px;margin:0 auto;display:flex;flex-direction:column;gap:40px}
h1,h2,h3{font-family:var(--display);margin:0;text-wrap:balance;line-height:1.2}
h1{font-size:30px}
h2{font-size:20px}
.lead{max-width:68ch;color:var(--muted);margin:8px 0 0}
.note{background:var(--warn-bg);color:var(--warn-fg);padding:10px 14px;border-radius:6px;max-width:68ch;margin-top:14px}
.screen{display:flex;flex-direction:column;gap:12px}
.screen-head{display:flex;flex-wrap:wrap;gap:6px 14px;align-items:baseline}
.tag{font-size:12px;letter-spacing:.06em;text-transform:uppercase;color:var(--muted);font-weight:600}
.ask{color:var(--muted);max-width:70ch;margin:0}
.dev{border:1px solid var(--line);background:var(--surface);border-radius:10px;overflow:hidden;min-width:0}
.dev-bar{display:flex;gap:6px;align-items:center;padding:8px 12px;background:var(--surface-2);border-bottom:1px solid var(--line);color:var(--muted);font-size:12px}
.dot{width:9px;height:9px;border-radius:50%;background:var(--line);display:inline-block}
.pane{padding:14px;display:flex;flex-direction:column;gap:12px}
.phone{width:100%;max-width:340px;border:1px solid var(--line);border-radius:26px;background:var(--surface);overflow:hidden;margin:0}
.phone .pane{padding:16px}
.phone-top{background:var(--accent);color:var(--accent-fg);padding:14px 16px}
.phone-top b{font-family:var(--display);font-size:17px;font-weight:700;display:block}
.phone-top span{font-size:12px;opacity:.85}
.tabs{display:flex;justify-content:space-around;border-top:1px solid var(--line);padding:10px 4px;font-size:12px;color:var(--muted)}
.tabs b{color:var(--accent)}
.two{display:grid;grid-template-columns:1fr;gap:20px;align-items:start}
@media(min-width:760px){.two{grid-template-columns:minmax(0,1fr) minmax(0,1fr)}}
.phones{display:flex;flex-wrap:wrap;gap:24px;justify-content:center}
.toolbar{display:flex;flex-wrap:wrap;gap:8px;align-items:center;justify-content:space-between}
.search{flex:1 1 160px;border:1px solid var(--line);border-radius:6px;padding:7px 10px;color:var(--muted);background:var(--bg)}
.btn{display:inline-block;border-radius:6px;padding:7px 12px;font-weight:600;border:1px solid var(--accent);color:var(--accent);background:transparent;font-size:13px}
.btn.solid{background:var(--accent);color:var(--accent-fg)}
.btn.block{display:block;text-align:center}
.alerts{background:var(--alert-bg);color:var(--alert-fg);border-radius:8px;padding:10px 12px;display:flex;flex-direction:column;gap:6px}
.alerts div{display:flex;justify-content:space-between;gap:10px;flex-wrap:wrap}
.chips{display:flex;flex-wrap:wrap;gap:6px}
.chip{display:inline-flex;gap:6px;align-items:center;border:1px solid var(--line);border-radius:999px;padding:3px 10px;font-size:12px;font-weight:600;background:var(--surface)}
.chip i{width:8px;height:8px;border-radius:50%;background:var(--c,var(--grey));display:inline-block}
.chip.on{background:var(--surface-2)}
.list{display:flex;flex-direction:column}
.row{display:grid;grid-template-columns:minmax(0,1.1fr) minmax(0,.9fr) minmax(0,1.2fr);gap:8px;padding:10px 2px;border-top:1px solid var(--line);align-items:center}
.row:first-child{border-top:0}
.row small{color:var(--muted);display:block}
@media(max-width:520px){.row{grid-template-columns:1fr 1fr}.row>:last-child{grid-column:1/-1}}
.e{--c:var(--grey)}.a{--c:var(--blue)}.p{--c:var(--gold)}.r{--c:var(--terra)}.c{--c:var(--leaf)}.k{--c:var(--teal)}
.field{display:flex;flex-direction:column;gap:3px}
.field label{font-size:12px;color:var(--muted);font-weight:600}
.input{border:1px solid var(--line);border-radius:6px;padding:8px 10px;background:var(--bg);color:var(--muted);min-height:36px}
.req label::after{content:" *";color:var(--terra)}
.grp{font-family:var(--display);font-weight:700;font-size:15px;margin-top:4px}
.fields{display:grid;grid-template-columns:1fr;gap:10px}
@media(min-width:560px){.fields{grid-template-columns:1fr 1fr}}
.steps{display:flex;gap:6px;color:var(--muted);font-size:12px;flex-wrap:wrap}
.steps b{color:var(--accent)}
.rtabs{display:flex;gap:2px;overflow-x:auto;border-bottom:1px solid var(--line);padding-bottom:0}
.rtabs span{padding:7px 10px;font-size:13px;color:var(--muted);white-space:nowrap;border-bottom:2px solid transparent}
.rtabs span.on{color:var(--accent);border-color:var(--accent);font-weight:600}
.panel{border:1px solid var(--line);border-radius:8px;padding:12px;background:var(--bg);display:flex;flex-direction:column;gap:6px}
.panel h3{font-size:14px;font-family:var(--body);font-weight:600}
.kv{display:flex;justify-content:space-between;gap:10px}
.kv span:first-child{color:var(--muted)}
.flag{background:var(--warn-bg);color:var(--warn-fg);border-radius:6px;padding:2px 8px;font-weight:600;font-size:12px;display:inline-block}
.ok{color:var(--ok-fg);background:var(--ok-bg);border-radius:6px;padding:2px 8px;font-weight:600;font-size:12px;display:inline-block}
.journey{display:flex;gap:4px;flex-wrap:wrap}
.journey span{flex:1 1 0;min-width:44px;text-align:center;font-size:10.5px;padding:4px 2px;border-radius:4px;background:var(--surface-2);color:var(--muted)}
.journey span.done{background:var(--ok-bg);color:var(--ok-fg)}
.journey span.now{background:var(--accent);color:var(--accent-fg);font-weight:600}
.card{border:1px solid var(--line);border-radius:10px;padding:12px;display:flex;flex-direction:column;gap:5px;background:var(--surface)}
.card h3{font-size:14px;font-family:var(--body);font-weight:600}
.scale{display:flex;gap:6px}
.scale span{width:30px;height:30px;border:1px solid var(--line);border-radius:50%;display:grid;place-items:center;color:var(--muted)}
.scale span.pick{background:var(--accent);color:var(--accent-fg);border-color:var(--accent)}
.opt{display:flex;gap:6px;flex-wrap:wrap}
.opt span{border:1px solid var(--line);border-radius:999px;padding:5px 12px}
.opt span.pick{background:var(--accent);color:var(--accent-fg);border-color:var(--accent)}
.sched{display:flex;justify-content:space-between;gap:8px;padding:5px 0;border-top:1px solid var(--line)}
.sched:first-of-type{border-top:0}
.check{color:var(--leaf);font-weight:700}
.bars{display:flex;align-items:flex-end;gap:5px;height:56px}
.bars span{flex:1;background:var(--leaf);border-radius:3px 3px 0 0;min-width:0}
.bars span.low{background:var(--gold)}
.barlab{display:flex;gap:5px;color:var(--muted);font-size:11px}
.barlab span{flex:1;text-align:center}
.track{height:8px;border-radius:4px;background:var(--surface-2);overflow:hidden}
.track i{display:block;height:100%;background:var(--leaf)}
.track.low i{background:var(--gold)}
.tl{display:flex;flex-direction:column;gap:0}
.tl div{display:grid;grid-template-columns:84px minmax(0,1fr);gap:10px;padding:8px 0;border-top:1px solid var(--line)}
.tl div:first-child{border-top:0}
.tl b{color:var(--muted);font-weight:600}
.foot{color:var(--muted);max-width:70ch}
</style>

<div class="wrap">
  <header>
    <p class="tag">Review sheet &middot; draft for Ravi</p>
    <h1>Ayurveda Journey App: key screens</h1>
    <p class="lead">Twelve screens from the blueprint, grouped as: first set (patient list, onboarding, record, arrival, daily check-in), then more for Care, then Departure and Continuity. They follow the decisions made so far and mark proposals as questions at the end of each screen.</p>
    <p class="note">These are pictures, not a working app. Every name, flight and number is invented dummy data.</p>
  </header>

  <section class="screen">
    <div class="screen-head"><span class="tag">C1 &middot; Clinic</span><h2>Patient list</h2></div>
    <p class="ask">First screen staff see. Anything needing action sits at the top; each patient shows their current phase.</p>
    <div class="dev">
      <div class="dev-bar"><span class="dot"></span><span class="dot"></span><span class="dot"></span>&nbsp; clinic.example/patients</div>
      <div class="pane">
        <div class="toolbar"><div class="search">Search patients</div><span class="btn solid">+ Onboard patient</span></div>
        <div class="alerts">
          <b>Needs attention (3)</b>
          <div><span>Anna K. flagged poor sleep, day 6</span><b>Open</b></div>
          <div><span>Marc D. flight changed, pickup to update</span><b>Open</b></div>
          <div><span>Lena S. check-in overdue by 2 days</span><b>Open</b></div>
        </div>
        <div class="chips">
          <span class="chip on">All</span>
          <span class="chip e"><i></i>Enquiry</span><span class="chip a"><i></i>Assessment</span><span class="chip p"><i></i>Planning</span>
          <span class="chip r"><i></i>Arrival</span><span class="chip c"><i></i>Care</span><span class="chip k"><i></i>Continuity</span>
        </div>
        <div class="list">
          <div class="row"><div><b>Anna K.</b><small>Austria</small></div><span class="chip c"><i></i>Care</span><div>Day 6 of 14 &middot; Dr. A</div></div>
          <div class="row"><div><b>Marc D.</b><small>Germany</small></div><span class="chip r"><i></i>Arrival</span><div>Lands Fri 14:35</div></div>
          <div class="row"><div><b>Lena S.</b><small>Switzerland</small></div><span class="chip k"><i></i>Continuity</span><div>Week 3 follow-up</div></div>
          <div class="row"><div><b>John P.</b><small>United Kingdom</small></div><span class="chip p"><i></i>Planning</span><div>Visa pending (AY-1)</div></div>
          <div class="row"><div><b>Sofia R.</b><small>Spain</small></div><span class="chip a"><i></i>Assessment</span><div>Call booked Monday</div></div>
          <div class="row"><div><b>Tom H.</b><small>United States</small></div><span class="chip e"><i></i>Enquiry</span><div>Quote sent 3 days ago</div></div>
        </div>
      </div>
    </div>
    <p class="foot">To confirm: is this the list the coordinator checks first each morning?</p>
  </section>

  <section class="screen">
    <div class="screen-head"><span class="tag">C2 &middot; Clinic</span><h2>Onboard a new patient</h2></div>
    <p class="ask">Four required fields create the record. Everything else is captured when available, and does not block onboarding.</p>
    <div class="dev">
      <div class="dev-bar"><span class="dot"></span><span class="dot"></span><span class="dot"></span>&nbsp; clinic.example/patients/new</div>
      <div class="pane">
        <div class="steps"><b>1 Details</b> &rsaquo; 2 Consent (proposed) &rsaquo; 3 Send invite (proposed)</div>
        <div class="grp">Required</div>
        <div class="fields">
          <div class="field req"><label>Full name</label><div class="input">Anna Keller</div></div>
          <div class="field req"><label>Email</label><div class="input">anna@example.com</div></div>
          <div class="field req"><label>Phone</label><div class="input">+43 ••• ••• ••</div></div>
          <div class="field req"><label>Nationality</label><div class="input">Austria</div></div>
        </div>
        <div class="grp">Optional</div>
        <div class="fields">
          <div class="field"><label>Photo</label><div class="input">Upload</div></div>
          <div class="field"><label>Date of birth</label><div class="input">DD / MM / YYYY</div></div>
          <div class="field"><label>Passport number</label><div class="input">&nbsp;</div></div>
          <div class="field"><label>Emergency contact</label><div class="input">Name and phone</div></div>
          <div class="field"><label>Passport scan</label><div class="input">Upload</div></div>
          <div class="field"><label>Previous medical records</label><div class="input">Upload, several files allowed</div></div>
        </div>
        <div class="field"><label>Earlier enquiry or quotation (optional)</label><div class="input">+ Add notes or a file from WhatsApp or email</div></div>
        <div class="toolbar"><span class="btn">Save draft</span><span class="btn solid">Next: consent</span></div>
      </div>
    </div>
    <p class="foot">To confirm: should consent be a second step here (suggested), or captured later? You parked this.</p>
  </section>

  <section class="screen">
    <div class="screen-head"><span class="tag">C3 &middot; Clinic</span><h2>Patient record, Care tab</h2></div>
    <p class="ask">One record per patient. Tabs follow the six phases, so staff always know where to look.</p>
    <div class="dev">
      <div class="dev-bar"><span class="dot"></span><span class="dot"></span><span class="dot"></span>&nbsp; clinic.example/patients/anna-k</div>
      <div class="pane">
        <div class="toolbar"><div><b style="font-family:var(--display);font-size:18px">Anna K.</b> <span class="chip c"><i></i>Care &middot; day 6 of 14</span><br><small style="color:var(--muted)">Austria &middot; Dr. A &middot; Guest house, room 12</small></div><span class="btn">Add entry</span></div>
        <div class="rtabs"><span>Enquiry</span><span>Assessment</span><span>Planning</span><span>Arrival</span><span class="on">Care</span><span>Continuity</span><span>Documents</span></div>
        <div class="two">
          <div class="panel">
            <h3>Today, Friday 17 October</h3>
            <div class="sched"><span>07:30 Abhyanga</span><span class="check">Done</span></div>
            <div class="sched"><span>10:00 Shirodhara</span><span>Pending</span></div>
            <div class="sched"><span>Meals: breakfast, lunch, dinner</span><span>1 of 3 served</span></div>
            <div class="sched"><span>Medicines: morning, evening</span><span>1 of 2 taken</span></div>
            <div class="sched"><span>17:00 Doctor review</span><span>Scheduled</span></div>
          </div>
          <div class="panel">
            <h3>Today's check-in from patient</h3>
            <div class="kv"><span>Medicines taken</span><span>Yes</span></div>
            <div class="kv"><span>Sleep</span><span><span class="flag">2 of 5</span></span></div>
            <div class="kv"><span>Appetite</span><span>4 of 5</span></div>
            <div class="kv"><span>Treatment</span><span>Okay</span></div>
            <div style="color:var(--muted)">&ldquo;Slept badly, felt warm after treatment.&rdquo;</div>
            <div class="toolbar"><span class="btn">Add doctor note</span><span class="btn solid">Mark reviewed</span></div>
          </div>
        </div>
      </div>
    </div>
    <p class="foot">To confirm: should Documents be its own tab? Which scores should the doctor treat as a flag?</p>
  </section>

  <section class="screen">
    <div class="screen-head"><span class="tag">P1 &middot; P2 &middot; Patient</span><h2>Home on arrival day, and the daily check-in</h2></div>
    <p class="ask">Phone view of the installed app. Left: the day the patient lands. Right: a day in Care, with the one-minute check-in.</p>
    <div class="phones">
      <figure class="phone">
        <div class="phone-top"><b>Welcome, Marc</b><span>Arrival &middot; Friday 17 October</span></div>
        <div class="pane">
          <div class="journey"><span class="done">Enquiry</span><span class="done">Assess</span><span class="done">Plan</span><span class="now">Arrival</span><span>Care</span><span>After</span></div>
          <div class="card"><h3>Arriving today</h3><div class="kv"><span>Flight</span><span>LX 148</span></div><div class="kv"><span>Lands</span><span>14:35, Mumbai T2</span></div><span class="btn solid block">I have landed</span></div>
          <div class="card"><h3>Who is meeting you</h3><div class="kv"><span>Driver</span><span>Ramesh</span></div><div class="kv"><span>Car</span><span>White Innova</span></div><div class="kv"><span>Phone</span><span>+91 ••••• •••••</span></div><div style="color:var(--muted)">Meeting point: arrivals hall, sign with your name.</div></div>
          <div class="card"><h3>Where you will stay</h3><div>Guest house, Baner, Pune</div><div style="color:var(--muted)">Check-in after 18:00</div></div>
          <span class="btn block">I need help</span>
        </div>
        <div class="tabs"><b>Home</b><span>Plan</span><span>Documents</span><span>Messages</span></div>
      </figure>
      <figure class="phone">
        <div class="phone-top"><b>Day 6 of 14</b><span>Friday 17 October</span></div>
        <div class="pane">
          <div class="card"><h3>Today</h3>
            <div class="sched"><span>07:30 Abhyanga</span><span class="check">Done</span></div>
            <div class="sched"><span>10:00 Shirodhara</span><span></span></div>
            <div class="sched"><span>17:00 Doctor review</span><span></span></div></div>
          <div class="card"><h3>Meals and medicines</h3>
            <div class="sched"><span>Breakfast: kitchari</span><span class="check">Done</span></div>
            <div class="sched"><span>Medicine, morning</span><span class="check">Taken</span></div>
            <div class="sched"><span>Medicine, evening</span><span>Not yet</span></div></div>
          <div class="card"><h3>Daily check-in &middot; 1 minute</h3>
            <div>Did you take all medicines?</div><div class="opt"><span class="pick">Yes</span><span>Partly</span><span>No</span></div>
            <div>How did you sleep?</div><div class="scale"><span>1</span><span class="pick">2</span><span>3</span><span>4</span><span>5</span></div>
            <div>How is the treatment going?</div><div class="opt"><span>Good</span><span class="pick">Okay</span><span>Not well</span></div>
            <div class="input">Anything for the doctor?</div>
            <span class="btn solid block">Send</span></div>
        </div>
        <div class="tabs"><span>Home</span><b>Plan</b><span>Documents</span><span>Messages</span></div>
      </figure>
    </div>
    <p class="foot">The app records answers and alerts the doctor. It never interprets them medically. To confirm: is five questions the right length for every day?</p>
  </section>

  <section class="screen">
    <div class="screen-head"><span class="tag">C4 &middot; Clinic &middot; Care</span><h2>Build tomorrow's plan</h2></div>
    <p class="ask">The coordinator enters the next day's schedule once. Publishing makes it appear in the patient's Plan tab. Copying from yesterday keeps daily entry short.</p>
    <div class="dev">
      <div class="dev-bar"><span class="dot"></span><span class="dot"></span><span class="dot"></span>&nbsp; clinic.example/patients/anna-k/care/day-7</div>
      <div class="pane">
        <div class="toolbar"><div><b style="font-family:var(--display);font-size:18px">Anna K. &middot; Day 7</b> <span class="chip c"><i></i>Care</span><br><small style="color:var(--muted)">Saturday 18 October &middot; draft, not yet visible to patient</small></div><span class="btn">Copy from yesterday</span></div>
        <div class="two">
          <div class="panel">
            <h3>Therapies</h3>
            <div class="sched"><span>07:30 &middot; Abhyanga</span><span>Therapist M &middot; 45 min</span></div>
            <div class="sched"><span>10:00 &middot; Shirodhara</span><span>Therapist R &middot; 40 min</span></div>
            <div class="sched"><span>+ Add therapy</span><span></span></div>
            <h3>Doctor review</h3>
            <div class="sched"><span>17:00 &middot; Dr. A</span><span>In person</span></div>
          </div>
          <div class="panel">
            <h3>Meals (diet plan from the doctor)</h3>
            <div class="sched"><span>Breakfast</span><span>Kitchari, warm water</span></div>
            <div class="sched"><span>Lunch</span><span>Moong dal, rice, steamed greens</span></div>
            <div class="sched"><span>Dinner</span><span>Light vegetable soup</span></div>
            <h3>Medicines</h3>
            <div class="sched"><span>Morning, before food</span><span>Medicine 1, 1 tablet</span></div>
            <div class="sched"><span>Evening, after food</span><span>Medicine 2, 10 ml</span></div>
          </div>
        </div>
        <div class="field"><label>Stay today</label><div class="input">Guest house, room 12 (same as yesterday)</div></div>
        <div class="toolbar"><span class="btn">Save draft</span><span class="btn solid">Publish to patient</span></div>
      </div>
    </div>
    <p class="foot">To confirm: should diet and medicines come from templates the doctor sets once, so the coordinator only picks them? Medicine names and doses are dummy text.</p>
  </section>

  <section class="screen">
    <div class="screen-head"><span class="tag">C5 &middot; Clinic &middot; Care</span><h2>Doctor's review queue</h2></div>
    <p class="ask">The doctor sees today's check-ins in one list, flagged ones first, and records notes and medicine changes without leaving the screen.</p>
    <div class="dev">
      <div class="dev-bar"><span class="dot"></span><span class="dot"></span><span class="dot"></span>&nbsp; clinic.example/review</div>
      <div class="pane">
        <div class="list">
          <div class="row"><div><b>Anna K.</b><small>Day 7 &middot; sleep 2 of 5</small></div><span class="flag">Flagged</span><div>&ldquo;Slept badly, felt warm after treatment.&rdquo;</div></div>
          <div class="row"><div><b>Pierre L.</b><small>Day 3 &middot; medicines partly taken</small></div><span class="flag">Flagged</span><div>&ldquo;Missed evening dose, stomach felt heavy.&rdquo;</div></div>
          <div class="row"><div><b>Sara W.</b><small>Day 10 &middot; all good</small></div><span class="ok">Reviewed</span><div>Appetite 5 of 5, treatment going well.</div></div>
        </div>
        <div class="panel">
          <h3>Anna K. &middot; note for today</h3>
          <div class="input">Doctor's note (shared with patient, or private to clinic)</div>
          <div class="toolbar"><div class="opt"><span class="pick">Share with patient</span><span>Private</span></div><div><span class="btn">Change medicine</span> <span class="btn solid">Save and mark reviewed</span></div></div>
        </div>
      </div>
    </div>
    <p class="foot">To confirm: what should count as a flag? The app only applies the rules the doctor sets, such as sleep 2 or lower, a missed dose, or the answer &ldquo;Not well&rdquo;.</p>
  </section>

  <section class="screen">
    <div class="screen-head"><span class="tag">P3 &middot; Patient &middot; Care</span><h2>Doctor's notes and medicines</h2></div>
    <p class="ask">What the doctor chose to share, plus the medicine list, so nothing is lost in a chat thread.</p>
    <div class="phones">
      <figure class="phone">
        <div class="phone-top"><b>My care</b><span>Day 7 &middot; Saturday 18 October</span></div>
        <div class="pane">
          <div class="card"><h3>From Dr. A &middot; today</h3><div>&ldquo;Rest this afternoon. Warm water through the day. We will review sleep at 17:00.&rdquo;</div><small style="color:var(--muted)">Shared 08:10</small></div>
          <div class="card"><h3>My medicines</h3>
            <div class="sched"><span>Medicine 1</span><span>Morning, before food</span></div>
            <div class="sched"><span>Medicine 2</span><span>Evening, after food</span></div>
            <div style="color:var(--muted)">Course until 31 October</div></div>
          <div class="card"><h3>Diet guidance</h3><div>Warm, light, freshly cooked food. No cold drinks.</div></div>
          <span class="btn block">Ask the clinic a question</span>
        </div>
        <div class="tabs"><span>Home</span><b>Plan</b><span>Documents</span><span>Messages</span></div>
      </figure>
    </div>
    <p class="foot">To confirm: should patients see the whole medicine history, or only the current course?</p>
  </section>

  <section class="screen">
    <div class="screen-head"><span class="tag">D1 &middot; Clinic &middot; Departure</span><h2>Plan the departure and follow-up</h2></div>
    <p class="ask">In the last days of treatment the coordinator arranges the trip home, and the doctor picks a follow-up schedule. The app then creates the check-in prompts.</p>
    <div class="dev">
      <div class="dev-bar"><span class="dot"></span><span class="dot"></span><span class="dot"></span>&nbsp; clinic.example/patients/anna-k/departure</div>
      <div class="pane">
        <div class="two">
          <div class="panel">
            <h3>Travel home</h3>
            <div class="kv"><span>Departure date</span><span>Fri 31 Oct</span></div>
            <div class="kv"><span>Flight</span><span>OS 118, 02:05</span></div>
            <div class="kv"><span>Pickup from guest house</span><span>22:30</span></div>
            <div class="kv"><span>Driver and car</span><span>Ramesh, white Innova</span></div>
            <div class="kv"><span>Flight entered by</span><span>Patient</span></div>
          </div>
          <div class="panel">
            <h3>Documents to hand over</h3>
            <div class="sched"><span>Prescription and medicine list</span><span class="ok">Ready</span></div>
            <div class="sched"><span>Diet guidance for home</span><span class="ok">Ready</span></div>
            <div class="sched"><span>Treatment summary</span><span class="flag">Doctor to sign</span></div>
            <div class="sched"><span>Feedback form</span><span>Sent on departure day</span></div>
          </div>
        </div>
        <div class="panel">
          <h3>Follow-up schedule (doctor picks a template)</h3>
          <div class="opt"><span class="pick">Weekly for 4 weeks, then monthly</span><span>Fortnightly for 3 months</span><span>Custom</span></div>
          <div class="kv"><span>Check-in prompts</span><span>Mondays 09:00, patient's local time</span></div>
          <div class="kv"><span>First consultation call</span><span>Week 2 &middot; WhatsApp video</span></div>
          <div class="kv"><span>Medicine supply</span><span>3 months, runs out about 31 Jan</span></div>
        </div>
        <div class="toolbar"><span class="btn">Save draft</span><span class="btn solid">Confirm and start follow-up</span></div>
      </div>
    </div>
    <p class="foot">To confirm: which follow-up templates does the doctor actually use today? The ones shown are examples.</p>
  </section>

  <section class="screen">
    <div class="screen-head"><span class="tag">D2 &middot; D3 &middot; Patient</span><h2>Departure day, and a follow-up week at home</h2></div>
    <p class="ask">Left: the day the patient flies home. Right: a Monday check-in after returning, sent on the clinic's schedule.</p>
    <div class="phones">
      <figure class="phone">
        <div class="phone-top"><b>Safe travels, Anna</b><span>Departure &middot; Friday 31 October</span></div>
        <div class="pane">
          <div class="journey"><span class="done">Enquiry</span><span class="done">Assess</span><span class="done">Plan</span><span class="done">Arrive</span><span class="done">Care</span><span class="now">Home</span></div>
          <div class="card"><h3>Your trip home</h3><div class="kv"><span>Pickup</span><span>22:30, guest house</span></div><div class="kv"><span>Flight</span><span>OS 118, 02:05</span></div><div class="kv"><span>Driver</span><span>Ramesh</span></div></div>
          <div class="card"><h3>Take with you</h3>
            <div class="sched"><span>Prescription and medicines</span><span class="check">Open</span></div>
            <div class="sched"><span>Diet guidance for home</span><span class="check">Open</span></div>
            <div class="sched"><span>Treatment summary</span><span class="check">Open</span></div></div>
          <div class="card"><h3>What happens next</h3><div>Weekly check-ins start Monday 3 November. A call with Dr. A is planned for week 2.</div></div>
          <span class="btn block">Share your feedback</span>
        </div>
        <div class="tabs"><b>Home</b><span>Plan</span><span>Documents</span><span>Messages</span></div>
      </figure>
      <figure class="phone">
        <div class="phone-top"><b>Weekly check-in</b><span>Week 2 at home &middot; Monday 10 November</span></div>
        <div class="pane">
          <div class="card"><h3>Your medicines</h3>
            <div>Have you taken them as advised this week?</div><div class="opt"><span class="pick">Yes</span><span>Partly</span><span>No</span></div>
            <div>Is the diet working at home?</div><div class="opt"><span>Easy</span><span class="pick">Some difficulty</span><span>Hard</span></div></div>
          <div class="card"><h3>How are you?</h3>
            <div>Energy this week</div><div class="scale"><span>1</span><span>2</span><span>3</span><span class="pick">4</span><span>5</span></div>
            <div class="input">Anything for the doctor?</div>
            <span class="btn solid block">Send</span></div>
          <div class="card"><h3>Next</h3><div>Video call with Dr. A, Thursday 13 November, 17:00 your time.</div><span class="btn block">Ask to reschedule</span></div>
        </div>
        <div class="tabs"><b>Home</b><span>Plan</span><span>Documents</span><span>Messages</span></div>
      </figure>
    </div>
    <p class="foot">To confirm: should the patient be able to request an extra consultation here, or only reply to clinic prompts?</p>
  </section>

  <section class="screen">
    <div class="screen-head"><span class="tag">D4 &middot; Clinic &middot; Continuity</span><h2>Patient record, Continuity tab</h2></div>
    <p class="ask">After departure the record keeps growing: check-ins, consultations the doctor gave by WhatsApp or phone, medicine supply and the nudge to invite the patient back.</p>
    <div class="dev">
      <div class="dev-bar"><span class="dot"></span><span class="dot"></span><span class="dot"></span>&nbsp; clinic.example/patients/anna-k</div>
      <div class="pane">
        <div class="toolbar"><div><b style="font-family:var(--display);font-size:18px">Anna K.</b> <span class="chip k"><i></i>Continuity &middot; week 6</span><br><small style="color:var(--muted)">Austria &middot; Episode 1 closed 31 Oct &middot; record kept for return visits</small></div><div><span class="btn">Log consultation</span> <span class="btn solid">Start new episode</span></div></div>
        <div class="rtabs"><span>Enquiry</span><span>Assessment</span><span>Planning</span><span>Arrival</span><span>Care</span><span class="on">Continuity</span><span>Documents</span></div>
        <div class="two">
          <div class="panel">
            <h3>Sleep score at each weekly check-in</h3>
            <div class="bars"><span class="low" style="height:40%"></span><span class="low" style="height:40%"></span><span style="height:60%"></span><span style="height:80%"></span><span style="height:80%"></span><span style="height:100%"></span></div>
            <div class="barlab"><span>Wk 1</span><span>Wk 2</span><span>Wk 3</span><span>Wk 4</span><span>Wk 5</span><span>Wk 6</span></div>
            <small style="color:var(--muted)">Scores 2, 2, 3, 4, 4, 5 on a 1 to 5 scale. Medicines taken at every check-in except week 2 (partly).</small>
            <h3>Medicine supply</h3>
            <div class="track low"><i style="width:55%"></i></div>
            <small style="color:var(--muted)">About 6 weeks left of 3 months. Reorder prompt due early January.</small>
          </div>
          <div class="panel">
            <h3>Consultations after departure</h3>
            <div class="tl">
              <div><b>13 Nov</b><span>WhatsApp video, Dr. A. Reviewed sleep and diet at home; no change to medicines.</span></div>
              <div><b>27 Nov</b><span>Phone call, Dr. A. Patient asked about travel and diet; advice logged.</span></div>
              <div><b>11 Dec</b><span>WhatsApp message, Dr. A. Medicine dose reminder.</span></div>
            </div>
            <h3>Return visit</h3>
            <div class="kv"><span>Suggested nudge</span><span>Sep 2027, about 11 months</span></div>
            <div class="kv"><span>Returns skip Enquiry</span><span>Start at Assessment or Planning</span></div>
          </div>
        </div>
      </div>
    </div>
    <p class="foot">To confirm: do you want a small trend chart like this for the doctor, or only the list of answers? The return-visit nudge is a proposal.</p>
  </section>
</div>

```
