# Color by Country Specification

**Conformance target:** No shipped surface uses a color or color pairing that the market it serves reads as political, oppressive, or offensive, and no state is told apart by color alone
**Audience:** Design, brand, marketing, engineering, and whoever owns the release gate
**Scope:** Product screens, printed receipts and tickets, charts, decks, marketing, packaging, and brand marks shipped into a named market
**Companion specs:** `bias-audit-spec.md` (§2 axis register), `disability-and-ableism-spec.md`, `WCAG-AA-spec.md` (1.4.1 Use of Color), `WCAG-AAA-spec.md`

Terms **MUST**, **SHOULD**, and **MAY** follow [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119).

**The core claim:** a palette carries history. Colors that read as neutral success and error states in one market can read as a dictatorship's flag or a party's campaign in another, and a team that picks colors on the screen they are looking at will not see it. The market register comes first; the product's own color semantics sit under it.

**Out of scope:** Contrast ratios, which are `WCAG-AA-spec.md` and `WCAG-AAA-spec.md`. Brand strategy. Color meaning that is the same in every market.

---

## 1. Purpose and conventions

| Field | Content |
|---|---|
| **Rule** | Each market the product ships into MUST have a dated color register (§3). Where the register and the product's own color semantics disagree, the register wins and the product semantics change. |
| **Why** | A color rule set for one market gets copied to the next one with the codebase. The register is the only place the difference is written down before it ships. |
| **How to verify** | For each market in the release, the register exists, carries a date and an owner, and every surface in the release has been checked against it. |

Each section below uses the Field/Content table format and lists **MUST / SHOULD / MAY** rules.

---

## 2. Color is never the only cue

| Field | Content |
|---|---|
| **Rule** | Every state a color marks MUST also be carried by a word, an icon, or a sign. Green SHOULD be avoided as a state color where another hue works, because red-green color blindness is the most common form. |
| **Why** | Palettes that pass contrast can still collapse into one color for a color-blind user. Measured with the Machado 2009 deuteranopia simulation, a common money palette fails as a code on its own while every color passes 7:1 on white (table below). |
| **How to verify** | Run every state color pair through a deuteranopia and protanopia simulation, then grayscale the screen. Every state is still identifiable from its text or icon. |

| Pair | Normal vision | Deuteranopia |
|---|---|---|
| Green `#065F46` and amber `#7A460C` | different hue, luminance ratio 1.01:1 | told apart only by a faint hue shift |
| Amber `#7A460C` and red `#991B1B` | amber and red | nearly the same color |

**MUST**

- Pair every colored state (in, out, blocked, success, error) with its word on the same element.
- Separate any two state colors by luminance as well as hue when they can appear side by side.

**SHOULD**

- Prefer a non-green hue for positive states when the market register (§3) does not require green.

---

## 3. The market register

| Field | Content |
|---|---|
| **Rule** | Each register entry MUST name the color or pairing, what is ruled out, why, and a source. An entry with no source MUST be labeled unconfirmed and still be followed until research confirms or removes it. |
| **Why** | Folklore about color spreads fast and is hard to retire. Labeling it keeps the team honest about what is known, without shipping the risk while it is checked. |
| **How to verify** | Every entry has a source link or the label "unconfirmed". |

**What counts as a pairing:** two colors as the dominant colors of one composition. A color on the other, a stripe or split of the two, a two-series chart in the pair, a logo or brand built on it. A small colored element on a neutral surface beside body text is not a pairing. In a dark theme, the near-black background counts as black.

---

## 4. Haiti

**MUST NOT pair red and black.** François Duvalier changed the flag's blue to black in 1964, and the black and red flag became the emblem of the dictatorship and the Tonton Macoute until the blue and red flag returned in 1986 ([Flag of Haiti](https://en.wikipedia.org/wiki/Flag_of_Haiti)).

- Red error text on a white surface beside black body copy is not the pairing.
- A red tag on a near-black dark-theme card is.

**SHOULD avoid green.** Unconfirmed: reported as disliked, with no negative meaning found in a web search. One candidate: green and yellow are the colors of Inite, the governing party in the disputed 2010 election ([Duke World Cultures](https://sites.duke.edu/wcwp/2010/11/28/yellow-and-green-in-haiti-a-footnote-to-the-election-crisis/)). §2 gives the same answer.

**Red reads as error or warning,** never as a reward or a win.

---

## 5. Dominican Republic

Nothing ruled out yet. To check: party colors, which are strongly partisan in the Dominican Republic.

---

## 6. Democratic Republic of the Congo

Nothing ruled out yet.

---

## 7. Conformance checklist

- [ ] Every market in the release has a dated color register with an owner.
- [ ] Every register entry has a source or is labeled unconfirmed.
- [ ] No surface shipped into Haiti pairs red and black, in light or dark theme.
- [ ] Every colored state carries a word, icon, or sign on the same element.
- [ ] Every state color pair passes a deuteranopia, protanopia, and grayscale check.
