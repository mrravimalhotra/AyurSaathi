# BMAD Pickup Guide
## Ayurvedic Clinic Patient Journey App

Version 0.1, 2026-10-20. Read this first, then `brd.md`, `architecture.md` and `parked-decisions.md`.

## 1. What is in the bundle

| File | Purpose |
|---|---|
| `brd.md` | Business requirements: scope, as-is and to-be, 80 functional requirements plus business rules and non-functional requirements, all with status tags, business rules, NFRs, compliance notes, assumptions, risks, candidate epics |
| `architecture.md` | Architecture: stack, decision records, data model, authorisation matrix, application layout, security, validation and error conventions, flows, spikes |
| `parked-decisions.md` | Register of everything undecided: 30 open questions (Part A) and every unconfirmed proposal (Part B) |
| `ux/mockups.html` | Visual mockups of twelve screens (dummy data). Open in a browser |
| `source/Ayurveda_Journey_App_MASTER.md` | Full background: research notes with sources, blueprint, text wireframes, decision log, mockup source |
| `BMAD_PICKUP.md` | This guide |

## 2. Rules for every agent

1. **Decided items** (tagged `[DECIDED]`) are requirements. Build to them.
2. **Proposed items** (`[PROPOSED]`) are suggestions the owner has not confirmed. They are **parked until confirmed**. You may carry them into the PRD as "candidate, unconfirmed". Do not commit them to a sprint without the owner's confirmation.
3. **Parked items** (`PK-nn`) are open questions. Do not implement them and do not guess. Use the working default only where one is listed, and flag it.
4. **No code until the owner gives the go signal** (PK-20). Planning documents, PRD, epics and stories are fine.
5. **Dummy data only.** Never real patient data in code, seed files, tests or screenshots (BR-08, BR-09).
6. This is a health product. The app records and alerts; it never gives medical advice or interprets answers medically. Clinical fields and flag rules come from a doctor (PK-09, PK-10).
7. If a requirement conflicts with another, stop and record the conflict for the owner rather than choosing.
8. Keep the decision trail: when you resolve or add something, update the status tag and the register.

## 3. Inputs BMAD needs, and where each lives

| BMAD need | Source in this bundle |
|---|---|
| Project brief / problem and goals | `brd.md` sections 1 to 3 |
| Users and personas | `brd.md` section 5 |
| Scope | `brd.md` section 4 |
| Requirements for the PRD | `brd.md` sections 8 to 11 (decided items first) |
| Constraints (stack, web first, owner process) | `brd.md` section 13; `architecture.md` section 2 |
| Compliance context | `brd.md` section 12; `source/...MASTER.md` part B |
| Architecture input | `architecture.md` |
| UX input | `ux/mockups.html`; `architecture.md` section 7.4; wireframes in the master file part D |
| Epics seed | `brd.md` section 15 |
| What not to build or decide | `parked-decisions.md` |

## 4. Suggested BMAD flow

1. **Analyst:** turn `brd.md` sections 1 to 3 into a project brief. Confirm the open questions that block it (PK-01, PK-02, PK-04, PK-05, PK-20) with the owner.
2. **PM:** write the PRD from the decided requirements first; list proposed items in a separate "candidate" section; carry parked items as open questions with their defaults.
3. **UX expert:** review `ux/mockups.html` with the owner screen by screen; record changes in a change log before editing; produce the front-end specification.
4. **Architect:** take `architecture.md` as the starting design; resolve spikes S-1 to S-7; check vendor limits and regions; confirm or change each ADR marked `[PROPOSED]`.
5. **Product owner:** shard the PRD and architecture; check that every epic only contains decided or confirmed items.
6. **Scrum master / developer / QA:** only after the go signal. Start with the walking skeleton (architecture section 10) and write the row-level security tests for every table as part of each story.

BMAD versions and default file locations differ between releases. Check the installed version's expected paths (commonly a `docs` folder with a PRD and an architecture file) and copy or rename these files to match.

## 5. Before the first agent runs: owner checklist

Minimum answers that unblock planning (the rest can proceed on defaults):
- [x] PK-01 Clinic is Ayurvedgram, Pune; design clinic-agnostic. [ ] Still open: name the sponsor.
- [x] PK-02 Coordinator and doctor use either phone or laptop (BR-12).
- [ ] PK-04 Consent: who approves the wording, and when it is captured (can stay parked for planning, must be resolved before real data).
- [ ] PK-05 Hosting region (can stay parked; spike S-3 first).
- [ ] PK-20 The go signal and first sprint scope.

Accounts and setup the owner will need at build time:
- [ ] Vercel account and project (as used for the owner's Invento app)
- [ ] Supabase organisation and projects (development, staging, production) in the chosen region
- [ ] Email provider and a verified sending domain (PK-22)
- [ ] Domain name for the app
- [ ] Claude Code and BMAD installed in the repository
- [ ] A doctor available for one working session on clinical fields, flags and follow-up templates (PK-09, PK-10, PK-11)
- [ ] A lawyer or advisor engaged for consent, GDPR and DPDP (PK-04, PK-18)

## 6. Starter prompts (paste into the agents)

**Analyst:**
> Read `docs/BMAD_PICKUP.md`, `docs/brd.md` and `docs/parked-decisions.md`. Produce a project brief from BRD sections 1 to 3. List the open questions that block planning and ask me them one at a time. Do not write code. Treat every `[PROPOSED]` and `[PARKED]` item as unconfirmed.

**PM:**
> Using the brief and `docs/brd.md`, write the PRD. Put `[DECIDED]` requirements in the main body. Put `[PROPOSED]` items in a section called "Candidate requirements, unconfirmed". Carry every `PK-nn` as an open question with its working default. Do not invent decisions.

**Architect:**
> Read `docs/architecture.md`. Review each ADR marked `[PROPOSED]`, list your changes with reasons, resolve the spikes S-1 to S-7 or say what you need, and produce the final architecture. Keep the owner's decided stack: Next.js, Vercel, Supabase.

## 7. What this bundle does not contain
- No application code, no database, no Supabase project, no deployment. A Supabase tool connection was available in the session that wrote these documents; it was not used and nothing was created.
- No real patient data. All mockup names, flights and medicines are invented.
- No legal advice. Compliance notes are first-pass findings from public pages.
