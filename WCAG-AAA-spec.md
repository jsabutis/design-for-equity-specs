# Accessibility Specification

**Conformance target:** [WCAG 2.2](https://www.w3.org/TR/WCAG22/) Level AAA  
**Audience:** Design, engineering, QA, and content owners  
**Scope:** Web-based user interfaces (HTML/CSS/JS). Framework-agnostic.

This document translates WCAG 2.2 AAA into project-ready rules. Terms **MUST**, **SHOULD**, and **MAY** follow [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119).

**How to use:** Link this file from `README.md`, `CONTRIBUTING.md`, or `AGENTS.md`. Treat it as the baseline for UI and interaction accessibility; project-specific design tokens MAY extend but MUST NOT weaken these thresholds.

**AAA caveat (W3C):** It is not recommended that Level AAA conformance be required as a general policy for entire sites because it is not possible to satisfy all Level AAA success criteria for some content (for example, sign language interpretation for all live audio). Products SHOULD aim for AAA where feasible and MUST document any **documented exception** (per page, per view, or per component) with business/technical justification, user impact, timeline or alternative, and owner—without weakening criteria elsewhere.

**Legal note:** WCAG 2.2 AAA is the most stringent published conformance level. This spec does not provide legal advice. Out of scope: PDF remediation, native app-only guidelines, and backend-only systems without a user interface.

---

## 1. Purpose & conventions

| Field | Content |
|-------|---------|
| **Rule** | Products MUST meet WCAG 2.2 Level AAA for all user-facing web content and functionality unless a **documented exception** applies (see intro). Exceptions MUST NOT be used to avoid criteria that are feasible for that content type. |
| **Why** | Maximum predictability and inclusion for users who rely on assistive tech, keyboard, adjusted display, reduced motion, or simplified language. |
| **How to verify** | Run automated checks (Section 16), complete the PR/QA checklist (Section 17), and maintain a register of documented exceptions with review dates. |
| **SC** | Full WCAG 2.2 AAA set (all Level A, AA, and AAA success criteria in the standard, subject to documented exceptions where genuinely inapplicable). |

Each following section lists **SC** (Success Criterion IDs) for traceability to [Understanding WCAG 2.2](https://www.w3.org/WAI/WCAG22/Understanding/).

---

## 2. Color & contrast

| Field | Content |
|-------|---------|
| **Rule** | Text and images of text MUST meet enhanced contrast ratios. User interface components (controls, focus indicators, form field boundaries) and graphical objects needed to understand content MUST meet 3:1 against adjacent colors. Color MUST NOT be the only visual means of conveying information, indicating an action, prompting a response, or distinguishing a visual element. |
| **Why** | Low contrast and color-only cues exclude users with low vision, color vision deficiency, or situational glare. |
| **How to verify** | Use a contrast checker on foreground/background pairs. Confirm state changes (error, success, required) use text, icon, or pattern in addition to color. |
| **SC** | 1.4.1 Use of Color (A), 1.4.6 Contrast (Enhanced) (AAA), 1.4.11 Non-text Contrast (AA). |

**MUST (text):**

- Normal text (under ~18pt / 24px, or under ~14pt / 18.67px if bold): **contrast ratio at least 7:1** against its background.
- Large text (at least 18pt / 24px, or at least 14pt / 18.67px if bold): **at least 4.5:1**.

**MUST (non-text):**

- UI components (default, focus, and state where applicable) and graphical objects essential to understanding: **at least 3:1** against adjacent colors.

**MUST:** Provide consistent focus and hover styles that meet **1.4.11** (see Section 5 for focus appearance).

**Disabled controls:** If a control is inactive, contrast requirements for inactive user interface components MAY follow Understanding guidance; still avoid relying on color alone for meaning.

**Light/dark:** Each theme MUST independently meet the same ratios.

---

## 3. Typography & text

| Field | Content |
|-------|---------|
| **Rule** | Text MUST be resizable to 200% without loss of content or functionality. No loss of content or functionality SHALL occur when users apply text spacing (line height, paragraph spacing, letter spacing, word spacing) within specified bounds. Images of text MUST be used only when essential to the information being conveyed (e.g. logotypes) or when the presentation cannot be achieved with text. Visual presentation of blocks of text MUST allow foreground and background colors to be chosen by the user; width, spacing, and justification MUST meet **1.4.8**; at 200% zoom and viewport width up to 1024 CSS pixels, content MUST reflow without horizontal scrolling. |
| **Why** | Many users need larger text, more spacing, shorter line length, or self-selected colors without horizontal scrolling or clipped content. |
| **How to verify** | Zoom browser to 200%; apply bookmarklet or styles for 1.4.12 spacing; confirm no clipping, overlap that hides meaning, or broken layout. Verify user-selectable themes or system colors where applicable; measure line length and spacing against **1.4.8**; test 200% at widths up to 1024px without horizontal scroll for reflowed text blocks. |
| **SC** | 1.3.2 Meaningful Sequence (A), 1.4.4 Resize text (AA), 1.4.8 Visual Presentation (AAA), 1.4.9 Images of Text (No Exception) (AAA), 1.4.12 Text Spacing (AA). |

**SHOULD (baseline for body copy):**

- Base body size at least **16px** (1rem typical).
- Line height at least **1.5** times the font size.
- Paragraph spacing at least **2** times the font size.
- Letter spacing at least **0.12em**.
- Word spacing at least **0.16em**.

**MUST:** **Meaningful sequence** — when the order of content affects meaning, that order MUST be preserved in the DOM and assistive technology reading order (see also Sections 4, 11).

**MUST (1.4.8 summary):** For blocks of text: user can select fg/bg; line length at most **80** characters (**40** if CJK); spacing at least **1.5** line height, **2×** font size paragraph spacing, **0.12em** letter spacing, **0.16em** word spacing; no full justification.

---

## 4. Layout, spacing & reflow

| Field | Content |
|-------|---------|
| **Rule** | Content MUST reflow without requiring two-dimensional scrolling at a viewport width equivalent to 320 CSS pixels (vertical scroll is acceptable). Orientation MUST not be restricted to a single mode unless **essential** to the activity (document why if claiming essential). |
| **Why** | Users magnify, use narrow viewports, or split screens; reflow avoids loss of content. |
| **How to verify** | Resize to 320px width (or use browser zoom to achieve equivalent CSS px); check tables, modals, and wide components. Test portrait and landscape on mobile. |
| **SC** | 1.3.4 Orientation (AA), 1.4.10 Reflow (AA). |

**Exceptions:** Content that requires 2D layout for usage or meaning (e.g. large data tables, maps, diagrams) MAY scroll in two dimensions only when **essential**; the exception MUST be documented and alternatives provided where possible.

### Content on hover or focus (1.4.13)

| Field | Content |
|-------|---------|
| **Rule** | Where receiving and then removing pointer hover or keyboard focus triggers additional content to become visible and then hidden, the additional content MUST be dismissible, hoverable, and persistent until dismissed or no longer relevant—unless **essential**. |
| **Why** | Unexpected overlays block reading and trap pointer users. |
| **How to verify** | Open tooltips, submenus, and custom popovers: confirm Esc or dismiss control works, content can be hovered without vanishing, and content stays visible until dismissed. |
| **SC** | 1.4.13 Content on Hover or Focus (AA). |

---

## 5. Focus

| Field | Content |
|-------|---------|
| **Rule** | Keyboard focus MUST be visible and MUST meet **2.4.13 Focus Appearance** (area, contrast, and adjacency). When a component receives focus, **no part** of the focus indicator or focused element MUST be hidden by author-created content (**2.4.12**). Focus order MUST be logical and intuitive. |
| **Why** | Keyboard and assistive technology users need to see where they are; obscured or weak focus causes disorientation and errors. |
| **How to verify** | Tab through all interactive elements; measure focus ring per [Understanding Focus Appearance](https://www.w3.org/WAI/WCAG22/Understanding/focus-appearance.html); confirm no sticky headers, toasts, or overlays clip or hide any part of the indicator or focused control. |
| **SC** | 2.4.3 Focus Order (A), 2.4.7 Focus Visible (AA), 2.4.11 Focus Not Obscured (Minimum) (AA), 2.4.12 Focus Not Obscured (Enhanced) (AAA), 2.4.13 Focus Appearance (AAA). |

**MUST:** Custom `:focus` / `:focus-visible` styles MUST meet **1.4.11** for the focus indicator vs adjacent colors and MUST satisfy **2.4.13** (non-thin indicator, **≥ 2 CSS px** of perimeter contrast difference vs unfocused state, **3:1** contrast for the indicator, not fully obscured).

---

## 6. Target size & pointer

| Field | Content |
|-------|---------|
| **Rule** | Pointer targets MUST be at least **44 by 44 CSS pixels**, except where exceptions in **2.5.5** apply. Web content MUST not restrict use of input modalities except where **essential** or where security requires it (**2.5.6**). Functionality operated by dragging MUST have a single-pointer alternative unless dragging is essential. Pointer gestures MUST have a single-pointer alternative unless essential. |
| **Why** | Small targets cause mis-taps; modality restrictions and drag-only paths block many users. |
| **How to verify** | Measure clickable/tappable areas; confirm **44×44px** minimum or equivalent spacing per **2.5.5**. Do not disable touch, keyboard, or voice where users expect them. Test drag workflows with keyboard or tap alternatives. |
| **SC** | 2.5.1 Pointer Gestures (A), 2.5.2 Pointer Cancellation (A), 2.5.5 Target Size (Enhanced) (AAA), 2.5.6 Concurrent Input Mechanisms (AAA), 2.5.7 Dragging Movements (AA). |

**Exceptions (2.5.5):** Equivalent control elsewhere, inline body text link, author-determined **essential** size/shape, user-agent default unmodified.

---

## 7. Motion, animation & auto-updating content

| Field | Content |
|-------|---------|
| **Rule** | Web pages MUST not contain anything that flashes more than three times in any one-second period (**2.3.2**). Motion from interaction MUST be disableable unless **essential** (**2.3.3**). For speech-dominant prerecorded audio, foreground MUST be at least **20 dB** above background (**1.4.7**). Auto-updating content that starts automatically, lasts more than five seconds, and is presented with other content MUST provide a way to pause, stop, or hide it. |
| **Why** | Flashing can trigger seizures; motion can cause vestibular symptoms; low signal-to-noise audio excludes hard-of-hearing users; auto-updating content distracts or prevents reading. |
| **How to verify** | Implement `prefers-reduced-motion: reduce` to disable or reduce non-essential motion; provide pause controls for carousels/tickers; run flash analysis on video or animated hero sections; measure audio foreground/background for speech tracks. |
| **SC** | 1.4.7 Low or No Background Audio (AAA), 2.2.2 Pause, Stop, Hide (A), 2.3.2 Three Flashes (AAA), 2.3.3 Animation from Interactions (AAA). |

**MUST:** `prefers-reduced-motion: reduce` MUST disable or minimize non-essential animation from user interaction.

---

## 8. Icons & non-text content

| Field | Content |
|-------|---------|
| **Rule** | All non-text content MUST have a text alternative that serves the equivalent purpose, except for decorative-only content, which MUST be ignored by assistive technologies. Purpose of icons, regions, and controls SHOULD be programmatically identifiable where **1.3.6** applies (see Section 11). |
| **Why** | Screen reader users and voice control users need names for icons and images; programmatic purpose supports personalization and AT. |
| **How to verify** | Inspect each icon/image: meaningful content gets descriptive `alt` or visible text; decorative gets `alt=""` and/or `aria-hidden="true"` on redundant icons. |
| **SC** | 1.1.1 Non-text Content (A). |

**MUST:** Icon-only buttons/links MUST have an accessible name (`aria-label`, `aria-labelledby`, or visible text).

---

## 9. Forms, labels & errors

| Field | Content |
|-------|---------|
| **Rule** | All form fields MUST have programmatic labels. Required fields, format constraints, and errors MUST be identified and described in text. Error suggestions MUST be provided when known. **All** submissions MUST be reversible, checked, or confirmed (**3.3.6**). Context-sensitive help MUST be available where users are expected to enter information (**3.3.5**). Autocomplete MUST be available for common personal data fields where appropriate. Authentication MUST meet **3.3.9** (no reliance on cognitive function tests; no object-recognition or personal-content workarounds). |
| **Why** | Labels, help, and clear errors prevent mistakes; universal error prevention protects all transactions; autocomplete and accessible auth reduce cognitive and motor load. |
| **How to verify** | Associate `<label for>` / implicit label, or `aria-label` / `aria-labelledby`. Provide inline help, glossary links, or instructions near complex fields. On error, expose message in text, link to field with `aria-describedby`, use `aria-invalid="true"`, and for dynamic updates use `aria-live` as needed. Confirm confirm/review steps or undo where appropriate. |
| **SC** | 1.3.1 Info and Relationships (A), 1.3.5 Identify Input Purpose (AA), 3.3.1 Error Identification (A), 3.3.2 Labels or Instructions (A), 3.3.3 Error Suggestion (AA), 3.3.4 Error Prevention (Legal, Financial, Data) (AA), 3.3.5 Help (AAA), 3.3.6 Error Prevention (All) (AAA), 3.3.9 Accessible Authentication (Enhanced) (AAA), 4.1.2 Name, Role, Value (A). |

**MUST:** Errors MUST NOT rely on color alone (combine with 1.4.1).

**Note:** **3.3.8** (AA) is subsumed by stricter **3.3.9** for AAA conformance where authentication is in scope.

---

## 10. Keyboard

| Field | Content |
|-------|---------|
| **Rule** | All functionality MUST be operable through a keyboard **without exception** (**2.1.3**). Keyboard focus MUST not be trapped. A mechanism MUST be available to bypass blocks of repeated content. If a keyboard shortcut uses only printable characters, it MUST be remappable, only active on focus, or preceded by a modifier. |
| **Why** | Many users cannot use a mouse or touch; path-dependent or partial keyboard support blocks completion. |
| **How to verify** | Unplug mouse: complete all tasks with no path-only gestures. Confirm Escape closes modals, focus returns logically. First focusable element SHOULD be skip link to main content. |
| **SC** | 2.1.2 No Keyboard Trap (A), 2.1.3 Keyboard (No Exception) (AAA), 2.1.4 Character Key Shortcuts (A), 2.4.1 Bypass Blocks (A). |

---

## 11. Semantic HTML & landmarks

| Field | Content |
|-------|---------|
| **Rule** | Information, structure, and relationships MUST be programmatically determinable or available in text. **Purpose** of icons, UI regions, and controls MUST be programmatically determinable where **1.3.6** applies. Headings and labels MUST describe topic or purpose. **Section** headings MUST be used to organize content (**2.4.10**). Each page MUST have exactly one `main` landmark where applicable; use semantic regions (`header`, `nav`, `main`, `aside`, `footer`). Each page or view MUST have a descriptive title (`<title>` and/or in-app title exposed to assistive technologies). Primary actions that trigger in-page behavior SHOULD use `<button>`; navigation to a URL SHOULD use `<a href>`. |
| **Why** | Correct semantics and explicit purpose enable navigation by heading/landmark, personalization, and predictable interaction patterns; titles orient users in tabs and history. |
| **How to verify** | Run accessibility tree inspection; heading levels MUST not skip inappropriately; one `h1` per primary view where applicable; document title reflects current view; use `autocomplete`, appropriate roles, and documented patterns for purpose (see Understanding 1.3.6). |
| **SC** | 1.3.1 Info and Relationships (A), 1.3.6 Identify Purpose (AAA), 2.4.2 Page Titled (A), 2.4.6 Headings and Labels (AA), 2.4.10 Section Headings (AAA), 4.1.2 Name, Role, Value (A). |

---

## 12. ARIA & dynamic content

| Field | Content |
|-------|---------|
| **Rule** | Prefer native HTML elements over ARIA when possible. Custom components MUST expose correct name, role, and value/states and MUST notify assistive technologies of changes when required. Status messages MUST be programmatically determinable without receiving focus. Widget patterns MUST follow APG unless a documented, tested alternative exists. |
| **Why** | Incorrect ARIA breaks assistive technologies; live regions communicate async updates. |
| **How to verify** | For widgets (tabs, dialogs, menus), follow [WAI-ARIA Authoring Practices Guide](https://www.w3.org/WAI/ARIA/apg/). Use `role="status"` / `aria-live="polite"` for non-critical updates; `role="alert"` or `aria-live="assertive"` sparingly for critical errors. |
| **SC** | 4.1.2 Name, Role, Value (A), 4.1.3 Status Messages (AA). |

---

## 13. Images, audio & video

| Field | Content |
|-------|---------|
| **Rule** | Alternatives MUST be provided per media type: captions for synchronized media; standard and **extended** audio description or **full text alternative** for prerecorded video as required; **sign language** interpretation for prerecorded synchronized media; transcripts or alternatives for audio-only; **live** captions for live synchronized media; **text alternative for live audio-only** (**1.2.9**). |
| **Why** | Deaf/hard-of-hearing, blind, and deaf-blind users need equivalent information including sign language and extended description where standard AD is insufficient. |
| **How to verify** | All prerecorded video has synchronized captions; provide sign language (embedded or separate sync); provide extended AD or sufficient pauses/full script; provide full text alternative where required; audio-only prerecorded has transcript; live synchronized media has captions; live audio-only has text alternative. |
| **SC** | 1.1.1 Non-text Content (A), 1.2.1 Audio-only and Video-only (Prerecorded) (A), 1.2.2 Captions (Prerecorded) (A), 1.2.3 Audio Description or Media Alternative (Prerecorded) (AA), 1.2.4 Captions (Live) (AA), 1.2.5 Audio Description (Prerecorded) (AA), 1.2.6 Sign Language (Prerecorded) (AAA), 1.2.7 Extended Audio Description (Prerecorded) (AAA), 1.2.8 Media Alternative (Prerecorded) (AAA), 1.2.9 Audio-only (Live) (AAA). |

---

## 14. Time, language & navigation consistency

| Field | Content |
|-------|---------|
| **Rule** | Time limits MUST NOT be imposed unless **essential** (**2.2.3**). Interruptions MUST be postponable or suppressible except emergencies (**2.2.4**). Users MUST be warned about duration of inactivity that could cause data loss if it lasts longer than **20 hours** (**2.2.6**). When an authenticated session expires, the user MUST be able to continue the activity without loss of data after re-authenticating (**2.2.5**). Page language MUST be programmatically determined; passages in other languages MUST be marked. **Unusual** words, **abbreviations**, and **pronunciation** MUST be available in text (**3.1.3–3.1.6**). Reading level MUST be lower secondary education level or a supplemental easy-to-read version MUST exist (**3.1.5**). Context changes MUST occur only on user request or a mechanism MUST exist to turn them off (**3.2.5**). When receiving focus or changing a setting, MUST NOT automatically change context unless the user has been advised. Navigation mechanisms that repeat MUST occur in the same relative order; components with the same functionality MUST be labeled consistently. Users MUST be informed of their **location** in a set of pages (**2.4.8**). Link purpose MUST be clear from link text alone (**2.4.9**). Within a set of pages, more than one way MUST be available to locate pages (e.g. nav, search, sitemap), except during steps of a process. |
| **Why** | Predictability, plain language, and location awareness assist comprehension; interruptions and timeouts cause data loss; unexpected navigation disorients. |
| **How to verify** | Set `<html lang="...">`; use `lang` on substrings; provide definitions, expansions, and pronunciation where needed; run reading-level checks or publish simplified summaries. No time limits except documented essential cases. Breadcrumbs or equivalent for **2.4.8**. Link text self-describing. Session timeout warnings per **2.2.6** where applicable. |
| **SC** | 2.2.3 No Timing (AAA), 2.2.4 Interruptions (AAA), 2.2.5 Re-authenticating (AA), 2.2.6 Timeouts (AAA), 2.4.5 Multiple Ways (AA), 2.4.8 Location (AAA), 2.4.9 Link Purpose (Link Only) (AAA), 3.1.1 Language of Page (A), 3.1.2 Language of Parts (AA), 3.1.3 Unusual Words (AAA), 3.1.4 Abbreviations (AAA), 3.1.5 Reading Level (AAA), 3.1.6 Pronunciation (AAA), 3.2.1 On Focus (A), 3.2.2 On Input (A), 3.2.3 Consistent Navigation (AA), 3.2.4 Consistent Identification (AA), 3.2.5 Change on Request (AAA). |

**Note:** 2.4.5 exceptions include processes with a prescribed sequence (e.g. checkout).

---

## 15. Cognitive & WCAG 2.2 additions

| Field | Content |
|-------|---------|
| **Rule** | When help is available, the mechanism MUST appear in the same relative order on each page where it appears. Information previously entered MUST be auto-populated or available for selection unless re-entry is essential. **3.3.5**, **3.3.6**, and **3.3.9** (Sections 9) MUST be satisfied. **3.1.5** reading level and **2.4.8** / **2.4.9** / **3.2.5** (Section 14) MUST be satisfied as cognitive and navigational aids. |
| **Why** | Reduces burden for cognitive disabilities, memory limitations, and motor fatigue; aligns AAA auth and error prevention with broad user needs. |
| **How to verify** | Place Help link in a consistent location; avoid duplicate data entry when safe; verify context help, universal confirmation/reversal, and **3.3.9** auth flows (no cognitive-object or personal-content tests). |
| **SC** | 3.2.6 Consistent Help (A), 3.3.7 Redundant Entry (A), 3.3.8 Accessible Authentication (Minimum) (AA), 3.3.9 Accessible Authentication (Enhanced) (AAA), plus cross-SC in Sections 9 and 14. |

**Note:** For strict AAA product claims, treat **3.3.9** as the authentication bar; **3.3.8** remains in the conformance stack but is exceeded by **3.3.9** where both apply.

---

## 16. Testing & tooling

**Automated (MUST run on CI or before release):**

- [axe-core](https://github.com/dequelabs/axe-core) or equivalent in build/CI — configure rulesets and manual review for AAA gaps axe does not fully cover.
- Lighthouse accessibility audit (or equivalent) — fix violations mapped to WCAG; do not rely on score alone.

**Manual (MUST for each major feature or release):**

- Full keyboard-only pass (no mouse); confirm **no keyboard exception** paths (Section 10).
- Screen reader spot-check: at least one of VoiceOver (macOS/iOS), NVDA (Windows), TalkBack (Android).
- **200%** browser zoom; **400%** zoom for reflow checks where 1.4.10 applies; **1024px** width check for **1.4.8** horizontal scroll at 200%.
- `prefers-reduced-motion` simulation — motion from interaction MUST stop (Section 7).
- Forced-colors / Windows High Contrast mode for critical UI.
- Color contrast verification: **7:1** / **4.5:1** text (Section 2); focus indicator per **2.4.13** (Section 5).
- Target size: **44×44 CSS px** (Section 6).
- Reading level or simplified-summary review (**3.1.5**); link purpose in isolation (**2.4.9**); location/breadcrumbs (**2.4.8**).
- Media: sign language, extended AD, and live audio text-alternative workflows where applicable (Section 13).

**SHOULD:** User testing with assistive technology users for high-risk flows (auth, payments, health).

---

## 17. PR / QA checklist (copy-pasteable)

Paste into pull requests or QA tickets. Check all that apply.

### Visual & layout

- [ ] Text contrast meets **7:1** (normal) / **4.5:1** (large) per Section 2
- [ ] Non-text UI (borders, icons, focus) meets **3:1** where required per Section 2
- [ ] Information is not conveyed by **color alone** (Section 2)
- [ ] **Meaningful sequence** preserved when order matters (Section 3)
- [ ] **1.4.8** visual presentation (line length, spacing, user colors, no full justification) satisfied (Section 3)
- [ ] Content usable at **200%** zoom; reflow at **320px** width; no horizontal scroll up to **1024px** at 200% for text blocks (Sections 3–4)
- [ ] **Orientation** works in portrait and landscape unless essential exception documented (Section 4)
- [ ] **Hover/focus** popovers/tooltips are dismissible, hoverable, persistent per Section 4
- [ ] Touch/click targets meet **44×44px** minimum or valid **2.5.5** exception (Section 6)
- [ ] **Images of text** only where essential (Section 3)

### Keyboard & focus

- [ ] All actions work with **keyboard only** with **no exceptions**; no **keyboard traps** (Section 10)
- [ ] **Skip link** or equivalent bypass of repeated blocks (Section 10)
- [ ] **Focus visible**; **2.4.13** focus appearance (area, contrast, not obscured) (Section 5)
- [ ] **Focus not obscured** — no part hidden by sticky UI (**2.4.12**) (Section 5)
- [ ] **Focus order** matches reading order (Sections 5, 11)
- [ ] **Concurrent input** not restricted (e.g. touch not disabled for “desktop only”) (Section 6)

### Screen reader & semantics

- [ ] **Page title** (`<title>` / view title) describes the page or view (Section 11)
- [ ] **Landmarks**, **section headings**, and **headings** sensible; one **`main`** where applicable (Section 11)
- [ ] **Purpose** of icons/regions/controls programmatically identifiable where required (**1.3.6**) (Section 11)
- [ ] Images have appropriate **`alt`**; decorative images hidden from AT (Sections 8, 13)
- [ ] Icon-only controls have **accessible names** (Section 8)
- [ ] Dynamic updates use **`aria-live`** / **status** where appropriate (Section 12)

### Forms

- [ ] Every control has a **programmatic label** (Section 9)
- [ ] **Context-sensitive help** available for expected user input (**3.3.5**) (Section 9)
- [ ] **Required**, **format**, and **errors** explained in **text** (Section 9)
- [ ] Errors identify the field and suggest a fix; **`aria-invalid`** / **`describedby`** as needed (Section 9)
- [ ] **`autocomplete`** on personal data fields where applicable (Section 9)
- [ ] **All submissions** reversible, checked, or confirmed (**3.3.6**) (Section 9)
- [ ] **Authentication** meets **3.3.9** — no cognitive / object / personal-content tests (Section 9)

### Pointer & motion

- [ ] **Dragging** has **single-pointer alternative** unless essential (Section 6)
- [ ] **No flash** more than three times per second (**2.3.2**) (Section 7)
- [ ] **Auto-updating** content over 5s has pause/stop/hide (Section 7)
- [ ] **`prefers-reduced-motion`** disables/minimizes **non-essential** motion from interaction (**2.3.3**) (Section 7)
- [ ] Prerecorded **speech** foreground **≥ 20 dB** above background where applicable (**1.4.7**) (Section 7)

### Media & time

- [ ] **Captions**, **sign language**, **extended AD**, **media text alternative**, **live captions**, **live audio text** per Section 13
- [ ] **No time limits** unless essential (**2.2.3**); **interruptions** postponable (**2.2.4**) (Section 14)
- [ ] **20h+ inactivity** data-loss warning if applicable (**2.2.6**) (Section 14)
- [ ] After **re-authentication**, work can continue **without data loss** where applicable (Section 14)
- [ ] **`lang`** set on page and foreign phrases (Section 14)
- [ ] **No unexpected context change** on focus alone or on input alone; **3.2.5** change on request (Section 14)
- [ ] **Multiple ways** to find pages (nav, search, etc.) where applicable (Section 14)
- [ ] **Location** (e.g. breadcrumbs) in page sets (**2.4.8**) (Section 14)
- [ ] **Link purpose** clear from link text alone (**2.4.9**) (Section 14)
- [ ] **Reading level** / simplified version; **unusual words**, **abbreviations**, **pronunciation** (Section 14)

### Cognitive & 2.2-specific

- [ ] **Help** in consistent location when present (Section 15)
- [ ] **Redundant entry** avoided where appropriate (Section 15)
- [ ] **Documented exceptions** for any AAA criteria not met, with review date (Section 1)

### Automated

- [ ] **axe** (or equivalent) passes on changed UI with no unresolved WCAG **AAA** violations within tool coverage
- [ ] **Lighthouse** a11y (or equivalent) reviewed; issues triaged

---

## 18. References

- [WCAG 2.2 Recommendation](https://www.w3.org/TR/WCAG22/)
- [How to Meet WCAG 2.2 (quick reference, AAA filter)](https://www.w3.org/WAI/WCAG22/quickref/?versions=2.2&levels=aaa)
- [Understanding WCAG 2.2](https://www.w3.org/WAI/WCAG22/Understanding/)
- [WAI-ARIA Authoring Practices Guide (APG)](https://www.w3.org/WAI/ARIA/apg/)
- [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/)

### WCAG 2.2 Level AAA success criteria (traceability)

| Criterion | Level | Where addressed in this spec |
|-----------|-------|------------------------------|
| 1.2.6 Sign Language (Prerecorded) | AAA | Section 13 |
| 1.2.7 Extended Audio Description (Prerecorded) | AAA | Section 13 |
| 1.2.8 Media Alternative (Prerecorded) | AAA | Section 13 |
| 1.2.9 Audio-only (Live) | AAA | Section 13 |
| 1.3.6 Identify Purpose | AAA | Sections 8, 11 |
| 1.4.6 Contrast (Enhanced) | AAA | Section 2 |
| 1.4.7 Low or No Background Audio | AAA | Section 7 |
| 1.4.8 Visual Presentation | AAA | Section 3 |
| 1.4.9 Images of Text (No Exception) | AAA | Section 3 |
| 2.1.3 Keyboard (No Exception) | AAA | Section 10 |
| 2.2.3 No Timing | AAA | Section 14 |
| 2.2.4 Interruptions | AAA | Section 14 |
| 2.2.6 Timeouts | AAA | Section 14 |
| 2.3.2 Three Flashes | AAA | Section 7 |
| 2.3.3 Animation from Interactions | AAA | Section 7 |
| 2.4.8 Location | AAA | Section 14 |
| 2.4.9 Link Purpose (Link Only) | AAA | Section 14 |
| 2.4.10 Section Headings | AAA | Section 11 |
| 2.4.12 Focus Not Obscured (Enhanced) | AAA | Section 5 |
| 2.4.13 Focus Appearance | AAA | Section 5 |
| 2.5.5 Target Size (Enhanced) | AAA | Section 6 |
| 2.5.6 Concurrent Input Mechanisms | AAA | Section 6 |
| 3.1.3 Unusual Words | AAA | Section 14 |
| 3.1.4 Abbreviations | AAA | Section 14 |
| 3.1.5 Reading Level | AAA | Sections 14, 15 |
| 3.1.6 Pronunciation | AAA | Section 14 |
| 3.2.5 Change on Request | AAA | Section 14 |
| 3.3.5 Help | AAA | Sections 9, 15 |
| 3.3.6 Error Prevention (All) | AAA | Sections 9, 15 |
| 3.3.9 Accessible Authentication (Enhanced) | AAA | Sections 9, 15 |

---

*Document version: 1.0 — WCAG 2.2 AAA baseline spec.*
