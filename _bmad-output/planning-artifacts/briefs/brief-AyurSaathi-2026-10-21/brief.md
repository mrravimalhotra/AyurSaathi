---
title: "Product Brief: AyurSaathi"
status: draft
created: 2026-10-21
updated: 2026-10-22
---

# Product Brief: AyurSaathi

## Executive Summary

AyurSaathi is a web app, installable on a phone's home screen, that runs the international patient journey for an Ayurvedic clinic: enquiry, assessment, planning, arrival, care and follow-up, on one shared patient record that lasts across visits. Clinic staff and doctors work in a clinic area; patients see their own plan, travel details and check-ins.

The first clinic is Ayurvedgram, Pune, which has treated more than 510 patients from 13 countries over about nine years. The product is built as a common core that every clinic shares, with each clinic's terminology, templates and clinical rules held as its own settings. The goal beyond the first clinic is a platform on which several Ayurveda clinics run.

This brief covers a prototype. It uses invented data only and is not rolled out to users. Its purpose is for the owner to see how the journey works end to end and decide whether to take it to Ayurvedgram.

## The Problem

International patients' whole journey runs over WhatsApp, email and phone. Three things follow:
- The clinic has no single place for a patient's travel plan, medical history, quotation or assessment outcome.
- Patients check several channels and can lose vital information.
- Information depends on individual staff members' inboxes and phones.

The pain is felt but has not been measured. No specific incident has been recorded and no baseline exists, so the cost is unknown. Measuring it, for example by counting "where is my pickup or plan" messages for two weeks, is a task for the pilot, before any target is set.

## The Solution

One place for the journey. Staff record the outcome and lineage of each phase; the app runs the structured parts: flight, pickup and stay, the daily care plan, check-ins, and follow-up after the patient goes home. Patients see consolidated information, scheduled reminders, pickup details and their medical records instead of hunting across channels. First contact, quotations and assessment calls stay on WhatsApp, email and phone; the app does not replace them.

The app records and alerts. It never gives medical advice or interprets answers. Clinical rules come from the clinic's doctor.

## What Makes This Different

Public medical-tourism platforms are marketplaces and Ayurveda clinic software is built around outpatient visits. Neither was found to cover the international journey for one clinic with WhatsApp as its front door. The edge here is not technical: it is Ayurvedgram's track record, closeness to the clinic, and a product shaped around its real workflow. A shared core with per-clinic settings lets that fit be reused for other clinics.

## Who This Serves

- **Coordinator:** enters flight, pickup, stay and the daily plan; works on a phone or a laptop.
- **Doctor:** records assessments, medicines and notes, and reviews check-ins; phone or laptop.
- **Patient:** often older and not very technical; opens an email link on a phone, signs in without a password, sees today's plan and answers a short check-in.
- **Admin:** manages users and settings.

## Success Criteria (prototype)

Judged by the owner alone. The prototype is a success if:
1. **The full demo journey works end to end** with dummy data: sign-in, onboarding a patient, the patient opening the invite, flight and pickup, the day plan, a check-in, and the doctor's review.
2. **Isolation is proven by tests:** no patient can read another's data, and no clinic can read another clinic's data.

Short data entry for staff and ease of use for older patients are deliberately out of the prototype's pass mark and become pilot criteria. Numeric targets wait for the baseline measurement.

## Scope

**In (prototype):** an end-to-end working prototype of the whole journey, built on invented data: sign-in and roles, clinic isolation, patient record and episodes, onboarding with documents and the consent step, enquiry and quotation log, assessment log, planning, arrival (flight, pickup, stay), care (daily plan, patient day view, check-in, doctor review) and continuity (follow-up check-ins, consultation log). Each phase works at a simple level so the journey can be walked from start to finish. English only.

**Later (not prototype work):** finer details within each phase, WhatsApp setup, and email provider configuration with a verified domain. Until then, sign-in links and notifications use a development mail setup or appear in the app.

**Out:** real patient data; rollout to users; online payments (payments are only recorded); native apps; web push; therapist, kitchen and attendant logins; return-visit nudges; running other clinics; national health-record integration; any automated clinical advice.

## Dependencies and Risks

- Ayurvedgram is not yet engaged. A sponsor, one doctor session (clinical fields, flag rules, follow-up templates, check-in questions), and time with the coordinator are needed before a pilot.
- Legal review of consent, retention and cross-border rules is needed before any real data.
- Patient screens are untested with older users until the pilot.
- Reminders reach patients only by email and in-app messages while WhatsApp sending is out, which is weaker than today's WhatsApp contact.
- The core-versus-customizable boundary is a draft and must be settled in the PRD and architecture.

## Vision

If the prototype and then a pilot with Ayurvedgram succeed, AyurSaathi becomes a platform that several Ayurveda clinics run on, each with its own settings. Anything beyond that is direction, not commitment.
