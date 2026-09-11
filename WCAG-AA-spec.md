---
title: Accessibility Specification — WCAG 2.2 AA
description: Project-ready translation of WCAG 2.2 Level AA. Framework-agnostic baseline for web UIs.
status: stable
version: 1.0
audience:
  - Design
  - Engineering
  - QA
  - Content
conformance:
  level: AA
  standard: WCAG 2.2
  url: https://www.w3.org/TR/WCAG22/
scope: Web-based user interfaces (HTML/CSS/JS). Framework-agnostic.
relatedSpecs:
  - WCAG-AAA-spec.md
---

This document translates **WCAG 2.2 AA** into project-ready rules. Terms **MUST**, **SHOULD**, and **MAY** follow [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119).

**How to use:** Link this file from `README.md`, `CONTRIBUTING.md`, or `AGENTS.md`. Treat it as the baseline for UI and interaction accessibility; project-specific design tokens MAY extend but MUST NOT weaken these thresholds.

**Legal note:** WCAG 2.2 AA is widely used for accessibility conformance (e.g. alignment with Section 508, EN 301 549). This spec does not provide legal advice. Out of scope: PDF remediation, native app-only guidelines, and backend-only systems without a user interface.

## 1. Purpose & conventions

**Rule** — Products MUST meet WCAG 2.2 Level AA for all user-facing web content and functionality unless an exception is documented (e.g. third-party embed with no feasible fix, with a documented alternative).

**Why** — Predictable, testable baseline for users who rely on assistive tech, keyboard, or adjusted display settings.

**How to verify** — Run automated checks (Section 16), complete the PR/QA checklist (Section 17), and document any exceptions.

**SC** — Full WCAG 2.2 AA set (all Level A and AA success criteria in the standard).

Each following section lists **SC** (Success Criterion IDs) for traceability to [Understanding WCAG 2.2](https://www.w3.org/WAI/WCAG22/Understanding/).

## 2. Color & contrast

**Rule** — Text and images of text MUST meet minimum contrast ratios. UI components (controls, focus indicators, form field boundaries) and graphical objects needed to understand content MUST meet 3:1 against adjacent colors. Color MUST NOT be the only visual means of conveying information.

**Why** — Low contrast and color-only cues exclude users with low vision, color vision deficiency, or situational glare.

**How to verify** — Use a contrast checker on foreground/background pairs. Confirm state changes (error, success, required) use text, icon, or pattern in addition to color.

**SC** — `1.4.1` Use of Color (A) · `1.4.3` Contrast (Minimum) (AA) · `1.4.11` Non-text Contrast (AA).

**MUST (text)**

- **Normal text** (under ~18pt / 24px, or under ~14pt / 18.67px if bold): contrast ratio at least **4.5:1** against its background.
- **Large text** (at least 18pt / 24px, or at least 14pt / 18.67px if bold): at least **3:1**.

**MUST (non-text)**

- UI components (default, focus, and state where applicable) and graphical objects essential to understanding: at least **3:1** against adjacent colors.

**SHOULD**

- Meet **7:1** for normal text where practical (AAA enhancement; not required for AA).
- Provide consistent focus and hover styles that meet 1.4.11.

**Disabled controls:** If a control is inactive, contrast requirements MAY follow Understanding guidance; still avoid relying on color alone for meaning.

**Light/dark:** Each theme MUST independently meet the same ratios.

## 3. Typography & text

**Rule** — Text MUST be resizable to 200% without loss of content or functionality. No loss of content or functionality SHALL occur when users apply text spacing within specified bounds. Avoid images of text except where essential (e.g. logos) or user-controllable.

**Why** — Many users need larger text or more spacing without horizontal scrolling or clipped content.

**How to verify** — Zoom browser to 200%; apply bookmarklet or styles for 1.4.12 spacing; confirm no clipping, overlap that hides meaning, or broken layout.

**SC** — `1.3.2` Meaningful Sequence (A) · `1.4.4` Resize text (AA) · `1.4.5` Images of Text (AA) · `1.4.12` Text Spacing (AA).

**SHOULD (baseline for body copy):**

| Property | Minimum |
|---|---|
| Base body size | **16px** (1rem typical) |
| Line height | **1.5×** font size |
| Paragraph spacing | **2×** font size |
| Letter spacing | **0.12em** |
| Word spacing | **0.16em** |

**Meaningful sequence** — when the order of content affects meaning, that order MUST be preserved in the DOM and assistive technology reading order (see also Sections 4, 11).

## 4. Layout, spacing & reflow

**Rule** — Content MUST reflow without requiring two-dimensional scrolling at a viewport width equivalent to **320 CSS pixels** (vertical scroll is acceptable). Orientation MUST not be restricted to a single mode unless essential.

**Why** — Users magnify, use narrow viewports, or split screens; reflow avoids loss of content.

**How to verify** — Resize to 320px width (or use browser zoom to achieve equivalent CSS px); check tables, modals, and wide components. Test portrait and landscape on mobile.

**SC** — `1.3.4` Orientation (AA) · `1.4.10` Reflow (AA).

**Exceptions:** Content that requires 2D layout for usage or meaning (e.g. large data tables, maps, diagrams) MAY scroll in two dimensions if clearly communicated; still provide alternatives where possible.

### Content on hover or focus (1.4.13)

**Rule** — Where receiving and then removing pointer hover or keyboard focus triggers additional content to become visible and then hidden, the additional content MUST be **dismissible**, **hoverable**, and **persistent** until dismissed or no longer relevant — unless essential.

**Why** — Unexpected overlays block reading and trap pointer users.

**How to verify** — Open tooltips, submenus, and custom popovers: confirm Esc or dismiss control works, content can be hovered without vanishing, and content stays visible until dismissed.

**SC** — `1.4.13` Content on Hover or Focus (AA).

## 5. Focus

**Rule** — Keyboard focus MUST be visible. When a component receives focus, any part of the focused element MUST NOT be hidden by author-created content (sticky headers, footers, non-modal dialogs, etc.). Focus order MUST be logical and intuitive.

**Why** — Keyboard and assistive technology users need to see where they are; obscured focus causes disorientation and errors.

**How to verify** — Tab through all interactive elements; confirm a visible focus ring (or equivalent) that meets non-text contrast; scroll sticky UI away or adjust layout so the focused control is not covered.

**SC** — `2.4.3` Focus Order (A) · `2.4.7` Focus Visible (AA) · `2.4.11` Focus Not Obscured (Minimum) (AA).

**SHOULD:** Focus indicator area and contrast — follow [Understanding Focus Appearance](https://www.w3.org/WAI/WCAG22/Understanding/focus-appearance.html) for robust rings (AAA criterion 2.4.13 is stricter; use as enhancement).

**Warning:** Custom `:focus` / `:focus-visible` styles MUST meet **1.4.11** (non-text contrast) for the focus indicator vs adjacent colors.

## 6. Target size & pointer

**Rule** — Pointer targets MUST be at least **24 by 24 CSS pixels**, except where exceptions apply. Functionality operated by dragging MUST have a single-pointer alternative unless dragging is essential. Pointer gestures MUST have a single-pointer alternative unless essential.

**Why** — Small targets cause mis-taps; drag-only paths block many users.

**How to verify** — Measure clickable/tappable areas; confirm minimum size or spacing that yields an equivalent 24×24px target. Test drag workflows with keyboard or tap alternatives.

**SC** — `2.5.1` Pointer Gestures (A) · `2.5.2` Pointer Cancellation (A) · `2.5.7` Dragging Movements (AA) · `2.5.8` Target Size (Minimum) (AA).

**Exceptions (2.5.8):** Inline links in sentence text, default browser controls, or when a conforming alternative target for the same action exists on the same page.

**SHOULD:** For touch-primary layouts, use **44×44 CSS pixels** or larger where feasible (best practice, not WCAG AA).

## 7. Motion, animation & auto-updating content

**Rule** — Web pages MUST not contain anything that flashes more than three times in any one-second period. Auto-updating content that starts automatically, lasts more than five seconds, and is presented with other content MUST provide a way to pause, stop, or hide it.

**Why** — Flashing can trigger seizures; motion can cause vestibular symptoms; auto-updating content distracts or prevents reading.

**How to verify** — Respect `prefers-reduced-motion` in CSS; provide pause controls for carousels/tickers; run flash analysis on video or animated hero sections.

**SC** — `2.2.2` Pause, Stop, Hide (A) · `2.3.1` Three Flashes or Below Threshold (A).

**Tip:** - **SHOULD:** Implement `prefers-reduced-motion: reduce` to reduce or disable non-essential animation (aligns with AAA **2.3.3 Animation from Interactions**; not required for AA).
- **MAY:** Adopt AAA **2.3.3** by ensuring motion from interaction can be disabled unless essential.

## 8. Icons & non-text content

**Rule** — All non-text content MUST have a text alternative that serves the equivalent purpose, except for decorative-only content, which MUST be ignored by assistive technologies.

**Why** — Screen reader users and voice control users need names for icons and images.

**How to verify** — Inspect each icon/image: meaningful content gets descriptive `alt` or visible text; decorative gets `alt=""` and/or `aria-hidden="true"` on redundant icons.

**SC** — `1.1.1` Non-text Content (A).

**Warning:** Icon-only buttons/links MUST have an accessible name (`aria-label`, `aria-labelledby`, or visible text).

## 9. Forms, labels & errors

**Rule** — All form fields MUST have programmatic labels. Required fields, format constraints, and errors MUST be identified and described in text. Error suggestions MUST be provided when known. Legal/financial data submissions MUST be reversible, checked, or confirmed. Autocomplete MUST be available for common personal data fields where appropriate.

**Why** — Labels and clear errors prevent mistakes; autocomplete reduces cognitive and motor load.

**How to verify** — Associate `<label for>` / implicit label, or `aria-label` / `aria-labelledby`. On error, expose message in text, link to field with `aria-describedby`, use `aria-invalid="true"`, and for dynamic updates use `aria-live` as needed.

**SC** — `1.3.1` Info and Relationships (A) · `1.3.5` Identify Input Purpose (AA) · `3.3.1` Error Identification (A) · `3.3.2` Labels or Instructions (A) · `3.3.3` Error Suggestion (AA) · `3.3.4` Error Prevention (Legal, Financial, Data) (AA) · `4.1.2` Name, Role, Value (A).

**Warning:** Errors MUST NOT rely on color alone (combine with 1.4.1).

## 10. Keyboard

**Rule** — All functionality MUST be operable through a keyboard without requiring specific timings for individual keystrokes. Keyboard focus MUST not be trapped. A mechanism MUST be available to bypass blocks of repeated content. If a keyboard shortcut uses only printable characters, it MUST be remappable, only active on focus, or preceded by a modifier.

**Why** — Many users cannot use a mouse or touch; traps and traps in modals block completion.

**How to verify** — Unplug mouse: complete all tasks. Confirm Escape closes modals, focus returns logically. First focusable element SHOULD be skip link to main content.

**SC** — `2.1.1` Keyboard (A) · `2.1.2` No Keyboard Trap (A) · `2.1.4` Character Key Shortcuts (A) · `2.4.1` Bypass Blocks (A).

## 11. Semantic HTML & landmarks

**Rule** — Information, structure, and relationships MUST be programmatically determinable or available in text. Headings and labels MUST describe topic or purpose. Each page MUST have exactly one `main` landmark where applicable; use semantic regions (`header`, `nav`, `main`, `aside`, `footer`). Each page or view MUST have a descriptive title. Primary actions that trigger in-page behavior SHOULD use `<button>`; navigation to a URL SHOULD use `<a href>`.

**Why** — Correct semantics enable navigation by heading/landmark and predictable interaction patterns; titles orient users in tabs and history.

**How to verify** — Run accessibility tree inspection; heading levels MUST not skip inappropriately; one `h1` per primary view where applicable; document title reflects current view.

**SC** — `1.3.1` Info and Relationships (A) · `2.4.2` Page Titled (A) · `2.4.6` Headings and Labels (AA) · `4.1.2` Name, Role, Value (A).

## 12. ARIA & dynamic content

**Rule** — Prefer native HTML elements over ARIA when possible. Custom components MUST expose correct name, role, and value/states and MUST notify assistive technologies of changes when required. Status messages MUST be programmatically determinable without receiving focus.

**Why** — Incorrect ARIA breaks assistive technologies; live regions communicate async updates.

**How to verify** — For widgets (tabs, dialogs, menus), follow [WAI-ARIA Authoring Practices Guide](https://www.w3.org/WAI/ARIA/apg/). Use `role="status"` / `aria-live="polite"` for non-critical updates; `role="alert"` or `aria-live="assertive"` sparingly for critical errors.

**SC** — `4.1.2` Name, Role, Value (A) · `4.1.3` Status Messages (AA).

## 13. Images, audio & video

**Rule** — Alternatives MUST be provided per media type: captions for synchronized media; audio description or text alternative for video when needed; transcripts or alternatives for audio-only; live captions for live audio (AA).

**Why** — Deaf/hard-of-hearing and blind users need equivalent information.

**How to verify** — All pre-recorded video has synchronized captions; pre-recorded video that needs visual context has audio description (or full text alternative); audio-only has transcript; live audio has captions.

**SC** — `1.1.1` Non-text Content (A) · `1.2.1` Audio-only and Video-only (Prerecorded) (A) · `1.2.2` Captions (Prerecorded) (A) · `1.2.3` Audio Description or Media Alternative (Prerecorded) (AA) · `1.2.4` Captions (Live) (AA) · `1.2.5` Audio Description (Prerecorded) (AA).

## 14. Time, language & navigation consistency

**Rule** — Time limits MUST be adjustable, turn-offable, or extendable unless essential. When an authenticated session expires, the user MUST be able to continue the activity without loss of data after re-authenticating. Page language MUST be programmatically determined; passages in other languages MUST be marked. When receiving focus or changing a setting, MUST NOT automatically change context unless the user has been advised. Navigation mechanisms that repeat MUST occur in the same relative order; components with the same functionality MUST be labeled consistently. Within a set of pages, more than one way MUST be available to locate pages (e.g. nav, search, sitemap), except during steps of a process.

**Why** — Predictability and language support assist comprehension; unexpected navigation disorients; multiple paths aid discovery; preserving work after timeout prevents data loss.

**How to verify** — Set `<html lang="...">`; use `lang` on substrings. Session timeout warnings with extend option; after re-login, form data preserved where applicable. No auto-submit on focus alone. Same nav order across pages. Site search or secondary nav where appropriate.

**SC** — `2.2.1` Timing Adjustable (A) · `2.2.5` Re-authenticating (AA) · `3.1.1` Language of Page (A) · `3.1.2` Language of Parts (AA) · `3.2.1` On Focus (A) · `3.2.2` On Input (A) · `3.2.3` Consistent Navigation (AA) · `3.2.4` Consistent Identification (AA) · `2.4.5` Multiple Ways (AA).

**Note:** 2.4.5 exceptions include processes with a prescribed sequence (e.g. checkout).

## 15. Cognitive & WCAG 2.2 additions

**Rule** — When help is available, the mechanism MUST appear in the same relative order on each page where it appears. Information previously entered MUST be auto-populated or available for selection unless re-entry is essential. Authentication MUST NOT rely on cognitive function tests alone; alternatives (password managers, copy-paste, two-factor without puzzle) MUST be allowed per SC text.

**Why** — Reduces burden for cognitive disabilities, memory limitations, and motor fatigue.

**How to verify** — Place Help link in a consistent location; avoid duplicate data entry when safe; allow password fields and paste; avoid CAPTCHA-only flows without an accessible alternative.

**SC** — `3.2.6` Consistent Help (A) · `3.3.7` Redundant Entry (A) · `3.3.8` Accessible Authentication (Minimum) (AA).

**Note:** 3.3.9 Accessible Authentication (Enhanced) is Level AAA in WCAG 2.2; MAY adopt as extra hardening — see [WCAG-AAA-spec.md](./WCAG-AAA-spec.md).

## 16. Testing & tooling

**Automated (CI / pre-release)**

- [axe-core](https://github.com/dequelabs/axe-core) or equivalent in build/CI.
- Lighthouse accessibility audit (or equivalent) — fix violations mapped to WCAG; **do not rely on score alone**.

**Manual (each major feature/release)**

- Full keyboard-only pass (no mouse).
- Screen reader spot-check: at least one of VoiceOver (macOS/iOS), NVDA (Windows), TalkBack (Android).
- **200%** browser zoom; **400%** zoom for reflow checks where 1.4.10 applies.
- `prefers-reduced-motion` simulation.
- Forced-colors / Windows High Contrast mode for critical UI.
- Color contrast verification with a documented tool (e.g. WebAIM Contrast Checker, browser DevTools).

**Recommended (SHOULD)**

User testing with assistive technology users for high-risk flows (auth, payments, health).

## 17. PR / QA checklist (copy-pasteable)

Paste into pull requests or QA tickets. Check all that apply.

### Visual & layout

- [ ] Text contrast meets **4.5:1** (normal) / **3:1** (large) per Section 2
- [ ] Non-text UI (borders, icons, focus) meets **3:1** where required per Section 2
- [ ] Information is not conveyed by **color alone** (Section 2)
- [ ] **Meaningful sequence** preserved when order matters (Section 3)
- [ ] Content usable at **200%** zoom; reflow at **320px** width without loss (Sections 3–4)
- [ ] **Orientation** works in portrait and landscape (Section 4)
- [ ] **Hover/focus** popovers/tooltips are dismissible, hoverable, persistent per Section 4
- [ ] Touch/click targets meet **24×24px** minimum or valid exception (Section 6)

### Keyboard & focus

- [ ] All actions work with **keyboard only**; no **keyboard traps** (Section 10)
- [ ] **Skip link** or equivalent bypass of repeated blocks (Section 10)
- [ ] **Focus visible**; focus ring meets **non-text contrast** (Sections 2, 5)
- [ ] **Focus not obscured** by sticky headers, toasts, or overlays (Section 5)
- [ ] **Focus order** matches reading order (Sections 5, 11)

### Screen reader & semantics

- [ ] **Page title** (`<title>` / view title) describes the page or view (Section 11)
- [ ] **Landmarks** and **headings** sensible; one **`main`** where applicable (Section 11)
- [ ] Images have appropriate **`alt`**; decorative images hidden from AT (Sections 8, 13)
- [ ] Icon-only controls have **accessible names** (Section 8)
- [ ] Dynamic updates use **`aria-live`** / **status** where appropriate (Section 12)

### Forms

- [ ] Every control has a **programmatic label** (Section 9)
- [ ] **Required**, **format**, and **errors** explained in **text** (Section 9)
- [ ] Errors identify the field and suggest a fix; **`aria-invalid`** / **`describedby`** as needed (Section 9)
- [ ] **`autocomplete`** on personal data fields where applicable (Section 9)

### Pointer & motion

- [ ] **Dragging** has **single-pointer alternative** unless essential (Section 6)
- [ ] No **flash** more than three times per second (Section 7)
- [ ] **Auto-updating** content over 5s has pause/stop/hide (Section 7)
- [ ] **`prefers-reduced-motion`** respected for non-essential animation (Section 7)

### Media & time

- [ ] **Captions** / **audio description** / **transcripts** per Section 13
- [ ] **Session timeouts** can be extended or turned off unless essential (Section 14)
- [ ] After **re-authentication**, work can continue **without data loss** where applicable (Section 14)
- [ ] **`lang`** set on page and foreign phrases (Section 14)
- [ ] **No unexpected context change** on focus alone or on input alone (Section 14)
- [ ] **Multiple ways** to find pages (nav, search, etc.) where applicable (Section 14)

### Cognitive & 2.2-specific

- [ ] **Help** in consistent location when present (Section 15)
- [ ] **Redundant entry** avoided where appropriate (Section 15)
- [ ] **Authentication** does not rely on cognitive tests alone; paste/password manager allowed (Section 15)

### Automated

- [ ] **axe** (or equivalent) passes on changed UI with no unresolved WCAG AA violations
- [ ] **Lighthouse** a11y (or equivalent) reviewed; issues triaged

## 18. References

- [WCAG 2.2 Recommendation](https://www.w3.org/TR/WCAG22/)
- [How to Meet WCAG 2.2 (quick reference)](https://www.w3.org/WAI/WCAG22/quickref/)
- [Understanding WCAG 2.2](https://www.w3.org/WAI/WCAG22/Understanding/)
- [WAI-ARIA Authoring Practices Guide (APG)](https://www.w3.org/WAI/ARIA/apg/)
- [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/)

### WCAG 2.2 success criteria new or changed in 2.2 (traceability)

| Criterion | Level | Where addressed in this spec |
|-----------|-------|------------------------------|
| 2.4.11 Focus Not Obscured (Minimum) | AA | Section 5 |
| 2.4.12 Focus Not Obscured (Enhanced) | AAA | Optional (Section 5 SHOULD) |
| 2.4.13 Focus Appearance | AAA | Optional (Section 5 SHOULD) |
| 2.5.7 Dragging Movements | AA | Section 6 |
| 2.5.8 Target Size (Minimum) | AA | Section 6 |
| 3.2.6 Consistent Help | A | Section 15 |
| 3.3.7 Redundant Entry | A | Section 15 |
| 3.3.8 Accessible Authentication (Minimum) | AA | Section 15 |
| 3.3.9 Accessible Authentication (Enhanced) | AAA | Section 15 (MAY) |

**Note:** *Document version: 1.0 — WCAG 2.2 AA baseline spec.*
