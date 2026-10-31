---
title: "How AyurSaathi keeps patient information private"
audience: "Ayurvedgram clinic owner, doctors and coordinators (non-technical)"
status: draft
created: 2026-10-31
---

# How AyurSaathi keeps patient information private

*A plain-language summary for the clinic. It describes the prototype's design, not a finished product. It is not legal advice, and the prototype uses invented patients only.*

## The short version

Each patient sees only their own information. Each clinic's information lives in its own separate system. The rules about who can see what are enforced by the database itself, not only by the screens, so a mistake on a screen cannot reveal someone else's record.

## What a patient can and cannot see

- A patient sees their own plan, travel details, medicines, check-ins and the notes and documents the clinic has chosen to **share**.
- A patient never sees another patient's information.
- A patient never sees anything the clinic marks **Staff-only**, such as a private clinical note.

## What each person on your team can do

| Role | Can do | Cannot do |
|---|---|---|
| Coordinator | Add patients, enter flight, pickup and stay, build and publish the day plan, log enquiries and payments | Write clinical notes or medicines; read Staff-only notes |
| Doctor | Record assessments, notes and medicines; review check-ins; set check-in questions and flag rules | Change the clinic's branding or user accounts |
| Admin | Manage users, branding and terminology | Edit clinical rules |

This table is the prototype's starting point. Your clinic can change it.

## Your clinic's data stays with your clinic

Every clinic gets its **own separate system** (its own database and its own copy of the app). One clinic's records are never stored alongside another's. Inside each system every record is also labelled with its clinic, as a second safeguard.

## How patients sign in

Patients do not need a password. They receive an email with a link, and a code they can type if the link does not work. Staff sign in with an email and password.

## Files and passports

Uploaded files, such as passport scans and medical records, are kept in private storage. A file opens only through a short-lived link created for a signed-in person who is allowed to see it.

## How we check this works

The prototype comes with automated tests that try to break these rules. They sign in as one patient and try to read another's record, and they sign in as one clinic and try to reach another's. The build does not pass if any table or file store has no such test.

## What is not in the prototype yet

Before any real patient's information is stored, these will be added or settled:
- A record of who viewed or changed each patient's information (audit trail).
- Extra login protection for staff (an authenticator code).
- Lawyer-approved consent wording and rules on how long information is kept and how it can be erased on request.
- Confirmation of where the data is hosted. The plan is India, and the exact location will be checked.

## Questions for the clinic

- Who at the clinic should be able to see Staff-only notes?
- Should coordinators see any clinical information at all?
- How long should the clinic keep a patient's information after treatment?
