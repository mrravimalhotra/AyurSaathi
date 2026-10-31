---
name: AyurSaathi
description: Calm, legible companion for an Ayurvedic clinic's international patients and its staff. Warm paper surfaces, one teal action colour, large type, status always in words.
status: draft
updated: 2026-10-31
colors:
  surface-base: '#FBF8F2'
  surface-raised: '#FFFFFF'
  surface-sunken: '#F1ECE2'
  ink-primary: '#1D2A2B'
  ink-secondary: '#4A5A5B'
  border-strong: '#8C8574'
  border-hairline: '#D9D2C3'
  primary: '#17575A'
  on-primary: '#FFFFFF'
  highlight: '#F2B63D'
  on-highlight: '#1D2A2B'
  focus-ring: '#0B5FFF'
  status-positive: '#1F6B3A'
  status-caution: '#7A4F00'
  status-critical: '#A32A2A'
  status-info: '#1F4F8F'
  phase-enquiry: '#E6E4DE'
  phase-assessment: '#D6E4F5'
  phase-planning: '#F5E6BC'
  phase-arrival: '#F4D6C6'
  phase-care: '#D3EBD3'
  phase-continuity: '#CBE9E8'
  surface-base-dark: '#101A1B'
  surface-raised-dark: '#17262A'
  surface-sunken-dark: '#0B1314'
  ink-primary-dark: '#EDF2F0'
  ink-secondary-dark: '#B5C3C1'
  border-strong-dark: '#5F7273'
  border-hairline-dark: '#2A3B3E'
  primary-dark: '#6CC5C0'
  on-primary-dark: '#08201F'
  status-positive-dark: '#7DD39A'
  status-caution-dark: '#F2C46B'
  status-critical-dark: '#FF9A9A'
  status-info-dark: '#9CC2FF'
typography:
  display:
    fontFamily: 'Source Serif 4, Georgia, serif'
    fontSize: 32px
    fontWeight: 600
    lineHeight: 40px
  title:
    fontFamily: 'Source Serif 4, Georgia, serif'
    fontSize: 24px
    fontWeight: 600
    lineHeight: 32px
  heading:
    fontFamily: 'Atkinson Hyperlegible Next, system-ui, sans-serif'
    fontSize: 20px
    fontWeight: 700
    lineHeight: 28px
  body-patient:
    fontFamily: 'Atkinson Hyperlegible Next, system-ui, sans-serif'
    fontSize: 18px
    fontWeight: 400
    lineHeight: 28px
  body-staff:
    fontFamily: 'Atkinson Hyperlegible Next, system-ui, sans-serif'
    fontSize: 16px
    fontWeight: 400
    lineHeight: 24px
  label:
    fontFamily: 'Atkinson Hyperlegible Next, system-ui, sans-serif'
    fontSize: 16px
    fontWeight: 700
    lineHeight: 24px
  meta:
    fontFamily: 'Atkinson Hyperlegible Next, system-ui, sans-serif'
    fontSize: 14px
    fontWeight: 400
    lineHeight: 20px
rounded:
  sm: 8px
  md: 12px
  lg: 16px
  full: 9999px
spacing:
  '1': 4px
  '2': 8px
  '3': 12px
  '4': 16px
  '5': 24px
  '6': 32px
  '7': 48px
  gutter-phone: 16px
  gutter-laptop: 24px
  tap-min: 48px
  tap-patient: 56px
components:
  button-primary:
    backgroundColor: '{colors.primary}'
    textColor: '{colors.on-primary}'
    typography: '{typography.label}'
    rounded: '{rounded.md}'
    height: '{spacing.tap-patient}'
  button-secondary:
    backgroundColor: '{colors.surface-raised}'
    textColor: '{colors.primary}'
    borderColor: '{colors.primary}'
    rounded: '{rounded.md}'
    height: '{spacing.tap-min}'
  card:
    backgroundColor: '{colors.surface-raised}'
    borderColor: '{colors.border-hairline}'
    rounded: '{rounded.lg}'
    padding: '{spacing.4}'
  input:
    backgroundColor: '{colors.surface-raised}'
    borderColor: '{colors.border-strong}'
    textColor: '{colors.ink-primary}'
    rounded: '{rounded.sm}'
    height: '{spacing.tap-min}'
  phase-chip:
    typography: '{typography.label}'
    rounded: '{rounded.full}'
    textColor: '{colors.ink-primary}'
  status-badge:
    typography: '{typography.label}'
    rounded: '{rounded.sm}'
  bottom-bar:
    backgroundColor: '{colors.surface-raised}'
    borderColor: '{colors.border-hairline}'
    height: 72px
  demo-ribbon:
    backgroundColor: '{colors.highlight}'
    textColor: '{colors.on-highlight}'
    typography: '{typography.meta}'
---

## Brand & Style

AyurSaathi should feel like a well-run clinic reception: warm, unhurried and exact. It is a tool for people who are travelling far, often tired, often not at ease with apps, and for staff who use it between other tasks. The design has one job, which is to make the next thing obvious and the current state unmistakable.

The look is calm clinical warmth. Warm paper surfaces rather than stark white, one deep teal for every action, and a single turmeric highlight reserved for the prototype's "Demo data" ribbon and for the one thing that deserves a second look. It deliberately avoids the visual shorthand of wellness branding (lotus marks, saffron washes, leaf textures) and the visual shorthand of hospital software (cold blues, dense grids). Information is the decoration.

Two voices share one system. Patient screens are generous: large type, one idea per screen, large targets. Staff screens are denser but never cramped: the same tokens at a smaller size scale with the same status language, so a coordinator who has seen a patient's screen understands it.

## Colors

- **Paper (`{colors.surface-base}`)** is the canvas. It is warmer than white to reduce glare and the clinical feel. Cards sit on it as `{colors.surface-raised}`; `{colors.surface-sunken}` holds quiet grouped content such as a closed phase.
- **Ink (`{colors.ink-primary}`)** is all body text at 14:1 on paper. `{colors.ink-secondary}` is for supporting text and clears 6:1; nothing the user must read is lighter than it.
- **Teal (`{colors.primary}`)** is the only action colour: primary buttons, links, the selected tab and the focus-adjacent accents. If it is teal, you can press or follow it.
- **Highlight (`{colors.highlight}`)** is turmeric. It is used for the Demo data ribbon, and sparingly to mark the single most important item on a screen. It is never used for status.
- **Status colours** (`{colors.status-positive}`, `-caution`, `-critical`, `-info`) always appear with a word and an icon, never alone. Each clears 6:1 on a card. Critical is for things that need action now (a flagged check-in, a failed upload), not for decoration.
- **Phase colours** are soft fills that tint the six journey phases. They always carry the phase number and name in dark ink (every pairing is above 10:1). A phase is identified by its number and name; the tint only helps scanning.
- **Dark theme** mirrors every token (`*-dark`). The same pairings hold: text at 7.6:1 or better, borders at 3.4:1. The theme follows the system setting and can be overridden in settings.
- **Focus ring (`{colors.focus-ring}`)** is a 3px outline with a 2px offset on every focusable element, above 3:1 against paper in both themes.

Avoid: red used for anything but action-needed states; green or red as the only signal; gradients; coloured text on coloured fills other than the pairings above.

## Typography

Two families. **Atkinson Hyperlegible Next** carries all interface and body text. It was designed for readers with low vision and separates look-alike characters, which matters for flight numbers, passport numbers and doses. **Source Serif 4** carries `display` and `title` only, to give pages a human, unhurried headline.

- Patient body is `{typography.body-patient}` at 18px with 28px line height, the floor for patient text. Staff body is `{typography.body-staff}` at 16px.
- Layouts must remain usable at 200% text zoom and with the largest system font setting. No control may truncate its label at that size; labels wrap.
- No all-caps labels, no text in images, no italics for emphasis. Emphasis is weight.
- Numbers that must be exact (flight numbers, doses, times) use tabular numerals and are never abbreviated.

## Layout & Spacing

Spacing scale: 4 / 8 / 12 / 16 / 24 / 32 / 48. Phone margins are `{spacing.gutter-phone}`; laptop gutters are `{spacing.gutter-laptop}`.

- **Patient screens** are a single column, content width capped at 560px on larger screens and centred. One primary action per screen.
- **Staff screens** adapt across three widths: under 600px a single column with a bottom bar; 600 to 1023px a single column with a wider reading measure and a bottom bar; 1024px and above a fixed left sidebar plus a list-and-detail split. The same data and the same actions exist at every width.
- Touch targets are at least `{spacing.tap-min}` (48px) everywhere and `{spacing.tap-patient}` (56px) on patient screens. Targets are separated by at least 8px.
- Forms are one column. Labels sit above fields, never inside them as placeholders.

## Elevation & Depth

Depth comes from tone and a hairline border, not shadow. Cards are `{colors.surface-raised}` with `{colors.border-hairline}`. The only shadow in the product is a soft one under the phone bottom bar and under modal sheets, so they read as above the content. No layered shadows, no blurred glass.

## Shapes

`{rounded.sm}` (8px) for inputs and badges, `{rounded.md}` (12px) for buttons, `{rounded.lg}` (16px) for cards and sheets, `{rounded.full}` for phase chips only. Corners are soft but the grid is straight; nothing is pill-shaped except a phase chip.

## Components

- **Primary button** — `{colors.primary}` fill, white label in `{typography.label}`, 56px high on patient screens, 48px on staff screens, full width on phone. One per screen. Disabled state keeps the label legible and adds the reason below the button.
- **Secondary button** — outlined in teal on a raised surface. Used for the second action, never for destructive actions.
- **Destructive action** — outlined in `{colors.status-critical}` with the verb in the label ("Remove file"), always behind a confirmation.
- **Card** — raised surface, hairline border, 16px padding. A card holds one subject and has one heading.
- **Phase chip** — number and name, such as "4 Arrival", on its phase tint. Current phase is also marked by a "Now" word, not only fill.
- **Journey bar** — six steps in a row on laptop; on phone, a compact "Step 4 of 6, Arrival" line with a six-segment bar below. Completed steps show a tick and the word "Done"; the current step shows "Now"; upcoming steps show nothing but their name.
- **Status badge** — icon plus word on a tinted fill: Done, Needs review, Not yet confirmed, Staff-only, Sample, Failed. Fill is a tint of the status colour; text is `{colors.ink-primary}`.
- **Staff-only marker** — a lock icon and the words "Staff-only" on any note, document or assessment hidden from the patient. It is visible to staff on the item itself, not only in settings.
- **Input** — 48px high, 1.5px `{colors.border-strong}` border, label above, helper text below, error text in `{colors.status-critical}` with an icon and the words of the fix.
- **Bottom bar** — four items on patient screens, four on staff phone screens. Each item has an icon and a text label at all times. The current item is marked with a teal bar above it and a bold label.
- **Sidebar** — laptop only, 240px, same items as the staff bottom bar plus Settings and the clinic name.
- **Demo ribbon** — a full-width strip at the very top of every screen reading "Demo data. Not real patients." in `{colors.highlight}`. It is part of the prototype shell and cannot be dismissed.
- **Medicine row** — medicine name in `{typography.heading}`, dose and schedule beneath, and a large "Taken" toggle with text. A ticked row reads "Taken at 08:10", never only a tick.
- **Check-in question** — one question per screen on the patient phone with a progress word ("Question 2 of 5"), answers as large option buttons rather than sliders.
- **Alert row** (staff) — icon, plain sentence, patient name, time, and one action button ("Open"). Unresolved alerts are listed above resolved ones.

## Do's and Don'ts

| Do | Don't |
|---|---|
| Put the next action in teal and the current state in words | Use colour, an icon or a tick alone to say what state something is in |
| Keep one primary action per screen | Show two filled buttons side by side |
| Show times with the zone, and the clinic time when the zone differs | Show a time without saying where |
| Write dose, flight and passport details in full | Abbreviate or truncate exact values |
| Mark Staff-only items on the item itself | Hide the Staff-only label in a menu |
| Keep the Demo data ribbon on every screen | Let invented data look like a real patient's record |
| Use plain, calm words ("Not yet confirmed") | Use urgency language, exclamation marks, or alarm colour for ordinary states |
| Support 200% text zoom and dark theme | Fix heights or truncate labels |
