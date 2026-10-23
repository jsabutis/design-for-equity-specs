# Color Vision Deficiency Specification

**Conformance target:** Every person with a color vision deficiency can complete every task, read every state, and interpret every chart the product shows, without asking anyone what a color means
**Audience:** Design, engineering, data visualization, content, QA, and whoever owns the release gate
**Scope:** Product screens, design tokens and themes, charts, maps and dashboards, forms and validation, developer tooling, games, printed output, hardware indicators, and any instruction that refers to a color
**Companion specs:** `WCAG-AA-spec.md` (1.4.1 Use of Color, 1.4.11 Non-text Contrast, 1.3.3 Sensory Characteristics), `WCAG-AAA-spec.md`, `color-by-country-spec.md` (what a color means in a market), `disability-and-ableism-spec.md`, `constrained-path-spec.md` (sunlight, cheap panels, grayscale print)

Terms **MUST**, **SHOULD**, and **MAY** follow [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119).

**The core claim:** color is a weak channel that most teams treat as a strong one. Roughly one man in twelve of European descent, and one in fifteen to fifty elsewhere, cannot reliably tell apart the reds, greens, oranges, and browns that products use for success, error, and chart series. Passing contrast does not fix this: two colors can both clear 7:1 against white and still look identical to each other. The fix is redundant encoding, lightness separation, and validated palettes, checked on the built screen.

**Out of scope:** Contrast against the background, which is `WCAG-AA-spec.md` and `WCAG-AAA-spec.md`. What a color means politically or culturally in a market, which is `color-by-country-spec.md`. Clinical screening and correction lenses.

**How to read this document.** Sections 1 and 2 say who this covers. Sections 3 to 5 are the rules that apply to every surface. Sections 6 to 10 apply the rules to specific surfaces. Section 11 covers user settings, section 12 is testing, and section 13 is the checklist. Appendix A holds validated palettes with measured numbers, Appendix B the reference simulation.

---

## 1. Purpose and conventions

| Field | Content |
|---|---|
| **Rule** | Every surface MUST be designed on the assumption that some of its users have a color vision deficiency and have not said so, and some do not know it themselves. |
| **Why** | Congenital color vision deficiency is common, invisible, and rarely disclosed. Many people with a mild form have never been tested and have learned to compensate until a product leaves them no other cue. Acquired forms arrive later in life with diabetes, glaucoma, and some medications, often without the person noticing the change. |
| **How to verify** | For any flow, name what a user who sees the screen in grayscale would miss. If the answer is anything other than "nothing", the flow fails. |

Each section below uses the Field/Content table format and lists **MUST / SHOULD / MAY** rules.

---

## 2. Who this covers

| Field | Content |
|---|---|
| **Rule** | Design and test MUST cover the three dichromat types (protan, deutan, tritan) and full loss of color (grayscale). Design MUST NOT target only the milder anomalous forms. |
| **Why** | A screen that works for a dichromat works for the milder forms of the same type. The reverse does not hold. Simulators model dichromacy; designing to the simulator therefore covers the whole range. |
| **How to verify** | The test record for each release names all four simulations (section 12). |

**Types.** Normal color vision uses three cone types, sensitive to long (L, "red"), medium (M, "green"), and short (S, "blue") wavelengths.

| Type | What is affected | What collapses | Inheritance |
|---|---|---|---|
| Protanomaly, protanopia | L cones shifted or absent | Red with green, orange, brown; reds look darker | X-linked |
| Deuteranomaly, deuteranopia | M cones shifted or absent | Red with green, orange, brown | X-linked |
| Tritanomaly, tritanopia | S cones shifted or absent | Blue with green, yellow with pink or light gray | Autosomal, rare |
| Achromatopsia | No functioning cones | All hue; light sensitivity and low acuity too | Autosomal recessive |
| Blue cone monochromacy | Only S cones and rods | Nearly all hue | X-linked |
| Acquired | Lens, retina, or optic nerve | Most often blue-yellow first | Diabetes, glaucoma, age, drugs |

**Prevalence.** Red-green deficiency is the common case, and the deutan forms are the most frequent within it.

| Population | Men | Women | Source |
|---|---|---|---|
| European descent | about 8% | about 0.4% | [Birch 2012, JOSA A 29(3)](https://opg.optica.org/josaa/abstract.cfm?uri=josaa-29-3-313) |
| East Asian | 4% to 6.5% | not given | Birch 2012 |
| Africa, pooled meta-analysis | 2.1% | 0.3% | [Tilahun et al. 2024, PLoS One](https://pmc.ncbi.nlm.nih.gov/articles/PMC11616826/) |
| Global, children and adolescents | 4.4% | 0.6% | [Jeong et al. 2025, Ophthalmology 132(12)](https://pubmed.ncbi.nlm.nih.gov/40769301/) |
| Tritan defects, congenital | disputed: commonly quoted as 1 in 13,000 to 65,000; one screening found about 2 in 1,000 | | [Went and Pronk 1985](https://pubmed.ncbi.nlm.nih.gov/3872255/) |
| Achromatopsia | about 1 in 30,000 people | | [Aboshiha et al. 2016, cone dysfunction syndromes](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4717370/) |
| Blue cone monochromacy | about 1 in 100,000 men | | Aboshiha et al. 2016 |

Acquired deficiency is not in these figures. It is reported in glaucoma, macular degeneration, and optic nerve disease, usually on the blue-yellow axis first, and as a side effect of hydroxychloroquine, ethambutol, and other drugs ([Cureus 2024 review](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC11749246/)). Products whose audience skews older or chronically ill SHOULD treat tritan testing as a MUST.

**MUST**

- Test against protan, deutan, and tritan simulation and against grayscale.
- Treat the men in the audience as the primary affected group when sizing impact. A 4% to 8% rate across a user base is not an edge case.

**MUST NOT**

- Describe color vision deficiency as "seeing in black and white". Monochromacy is the rare case; most affected users see color and confuse specific pairs.
- Size the problem from the team's own population. Prevalence varies by ancestry, and the audience is the denominator.

---

## 3. Color is never the only cue

| Field | Content |
|---|---|
| **Rule** | Every piece of information that a color carries MUST also be carried by text, an icon shape, position, a pattern, or a line style on the same element. |
| **Why** | This is WCAG 1.4.1 Use of Color, and it is the rule that does the most work. Apple's App Store accessibility criteria state the failure plainly: status buttons or icons whose only distinguishing difference is red versus green ([Apple, Differentiate Without Color Alone](https://developer.apple.com/help/app-store-connect/manage-app-accessibility/differentiate-without-color-alone-evaluation-criteria)). |
| **How to verify** | Switch the screen to grayscale. Every state, series, category, and selection is still identifiable from something other than its color. |

**MUST**

- Pair every colored status (success, warning, error, info, online, offline, paid, overdue) with its word, or with an icon whose shape differs per state, on the same element. A check in a circle and a cross in an octagon differ by shape; two same-shaped dots do not.
- Mark selected, active, and current items with a change in weight, border, fill, position, or an indicator, not only a hue shift.
- Mark required fields with text or a symbol whose meaning is stated, not with a red label alone.
- Show the sign on every delta: `+4.2%` and `-1.8%`, with an up or down arrow, whatever colors the market uses for gain and loss.

**SHOULD**

- Prefer text over icons where space allows. An icon still has to be learned; a word does not.
- Keep color in the design. Apple's guidance is explicit that removing color is not the goal; color stays as the fast cue for those who see it, and the redundant cue carries everyone else.

**MUST NOT**

- Rely on a colored dot, bar, cell fill, or text color as the only marker of a state.
- Use the same icon in two state colors to mean two different things.

---

## 4. Separate by lightness, not hue

| Field | Content |
|---|---|
| **Rule** | Any two state or category colors that can appear next to each other MUST differ in lightness by a luminance contrast of at least 3:1 between themselves, or be separated by a border, label, or pattern. |
| **Why** | Red-green dichromacy removes one axis of hue but largely keeps lightness. Two colors chosen for "different hue, similar weight" are exactly the pairs that collapse. The 3:1 figure is the one WCAG uses for telling an inline link from its surrounding text ([G183](https://www.w3.org/WAI/WCAG22/Techniques/general/G183)) and for adjacent pie slices ([Understanding 1.4.11](https://www.w3.org/WAI/WCAG22/Understanding/non-text-contrast.html)). |
| **How to verify** | Compute the contrast ratio between each pair of adjacent state colors, not only against the background. Below 3:1, a non-color separator is present. |

**Measured.** Pairs below were run through the Machado 2009 simulation at full severity (Appendix B). ΔE00 is the CIEDE2000 color difference; under about 10, a small mark is hard to tell apart.

| Pair | Normal ΔE00 | Deutan ΔE00 | Protan ΔE00 | Luminance ratio | Verdict |
|---|---|---|---|---|---|
| Green `#16A34A`, red `#DC2626` | 72.5 | 7.9 | 24.0 | 1.47:1 | Collapses under deutan |
| Green `#22C55E`, red `#EF4444` | 76.2 | 7.7 | 26.0 | 1.65:1 | Collapses under deutan |
| Green `#16A34A`, amber `#D97706` | 49.9 | 11.8 | 7.5 | 1.03:1 | Identical in grayscale (ΔE00 0.9) |
| Blue `#0072B2`, orange `#E69F00` | 55.3 | 62.7 | 55.6 | 2.30:1 | Distinct under all three |

The first two rows are the default success and error colors of a popular utility framework. Both pass as a pair to a person with normal vision and nearly vanish as a pair under deuteranopia.

**MUST**

- Check every adjacent pair of state colors for luminance contrast between the two, in both light and dark themes.
- Add a border, gap, or label wherever two fills below 3:1 touch, as WCAG's pie chart example does.

**SHOULD**

- Build status palettes from a lightness ramp first and assign hue second, so the pair still reads in grayscale.
- Prefer blue and orange over green and red for a binary good and bad when the market allows (check `color-by-country-spec.md`).
- Avoid green as a state color where another hue works, because the deutan forms are the most common.

**MUST NOT**

- Pair red with green, green with brown, green with orange, or blue with purple as the only difference between two states or series.

---

## 5. Never refer to a thing by its color alone

| Field | Content |
|---|---|
| **Rule** | Instructions, help text, error messages, and support scripts MUST NOT identify a control, region, or state by color alone. |
| **Why** | "Tap the green button" fails a user who cannot find the green button, and support staff repeat it on the phone. This is WCAG 1.3.3 Sensory Characteristics. People with color vision deficiency also misname surface colors, so asking them to report a color back fails in the other direction. |
| **How to verify** | Search the string files and help center for color words (red, green, orange, blue, yellow, and their translations). Each hit names the control by its label too. |

**MUST**

- Name controls by their label: "Tap Confirm", or "Tap the green Confirm button", never "tap the green one".
- Give every color a product sells, or that a user picks, a visible name: "Forest green", not a swatch alone. Show the name in the picker, the cart, the order history, and the receipt.
- Let support identify a state by its word or code, never by asking the user what color they see.

**SHOULD**

- Show the hex value or a named color next to any user-chosen color in a theme or design tool.

---

## 6. Charts, maps, and dashboards

| Field | Content |
|---|---|
| **Rule** | Every chart MUST be readable without telling series apart by hue: series are labeled directly or carry distinct markers or line styles, categorical palettes are validated under simulation, and ordered data uses a palette whose lightness changes monotonically. |
| **Why** | Charts are where color carries the most meaning with the least backup. The default categorical palette of a widely used charting library collapses under simulation (table below). Rainbow and jet colormaps distort data for everyone and are unreadable for many readers with color vision deficiency ([Crameri, Shephard and Heron 2020, Nature Communications 11:5444](https://www.nature.com/articles/s41467-020-19160-7)). Cividis was optimized so that viewers with and without red-green deficiency read the same data the same way ([Nuñez, Anderton and Renslow 2018, PLoS One](https://pmc.ncbi.nlm.nih.gov/articles/PMC6070163)). |
| **How to verify** | Run the built chart through protan, deutan, and tritan simulation and grayscale. Each series can still be named, and every ordered scale still reads from low to high. |

| Categorical palette, 7 colors | Worst pair ΔE00, protan | Worst pair ΔE00, deutan | Worst pair ΔE00, tritan |
|---|---|---|---|
| Okabe and Ito (no black) | 12.2 | 11.6 | 10.9 |
| Tol bright | 14.2 | 14.8 | 8.6 |
| d3 category10, first 7 | 1.3 (orange and green) | 4.6 (green and red) | 9.5 |

**MUST**

- Label series directly on or beside the line, bar, or area wherever there is room. A legend forces the reader to match colors, which is the task they cannot do.
- When a legend is used, order it in the same order the series appear in the chart, and give each series a distinct marker shape or line dash too.
- Use a validated categorical palette (Appendix A) and keep categorical series to the palette's stated maximum. Beyond about 7, group into "other" or split the chart.
- Use a sequential palette with monotonic lightness for ordered data (viridis, cividis, or a single-hue ramp).
- Use a diverging palette with two hues that survive simulation (blue and orange, blue and red) and a light neutral midpoint. Never red and green.
- Give pie and donut slices, stacked bars, and map regions a separating border or a 3:1 difference between neighbors, per section 4.
- Provide the underlying numbers: a data table, tooltip values, or text labels, so no figure is reachable only through color.

**SHOULD**

- Highlight one series by making it saturated and the rest gray, rather than giving every series its own hue.
- Use pattern or texture fills for categories in print and for adjacent areas that cannot be labeled.
- Encode the most important comparison by position or length, with color as a secondary channel.

**MUST NOT**

- Use rainbow, jet, or hsv colormaps for ordered data.
- Use a red-to-green scale for heat maps, scorecards, or RAG (red, amber, green) status grids without a word or symbol in every cell.
- Interpolate a categorical palette to stretch it to more categories.

---

## 7. Forms, links, and interaction states

| Field | Content |
|---|---|
| **Rule** | Links, errors, focus, and every interaction state MUST be distinguishable without color. |
| **Why** | These are the states a user must see to act. A form whose only error signal is a red border leaves the user unable to find what to fix. |
| **How to verify** | In grayscale, tab through the form with an invalid entry. The error is found from its message and icon; focus is found from its indicator; links in a paragraph are found from their underline. |

**MUST**

- Underline links in body text. If a design removes the underline, the link MUST have 3:1 luminance contrast with the surrounding text (WCAG technique G183) and MUST gain an underline or other non-color cue on hover and on keyboard focus.
- Show each field error as a text message next to the field, with an icon, and move or announce focus to it. A red border alone is not an error state.
- Make the focus indicator a change in shape or thickness (an outline or ring), not a change in color.
- Show disabled controls with more than a hue change, and explain why the control is disabled where it matters.
- Show toggle and switch state with position, a label, or an icon, not only a fill color.

**SHOULD**

- Show success after submission as a message, not only as a field turning green.

---

## 8. Developer tools, code, and text output

| Field | Content |
|---|---|
| **Rule** | Diffs, logs, test results, and terminal output MUST carry their meaning in characters, not only in color. |
| **Why** | Red and green are the default colors for removed and added lines and for failing and passing tests, which is the exact pair that collapses. GitHub split its single colorblind theme in 2022 into a protanopia and deuteranopia theme and a separate tritanopia theme, after feedback that one theme did not serve both ([GitHub changelog](https://github.blog/changelog/2022-04-19-protanopia-deuteranopia-colorblind-themes-beta/)). |
| **How to verify** | Pipe the output through a tool that strips ANSI color, or view the diff in grayscale. Every added, removed, passing, and failing item is still marked. |

**MUST**

- Prefix diff lines with `+` and `-`, and test results with a word (`PASS`, `FAIL`) or a distinct glyph.
- Respect `NO_COLOR` and non-terminal output by keeping the words when color is removed.
- Keep syntax highlighting decorative. No error, warning, or lint state may be signaled by token color alone.

**SHOULD**

- Offer protan, deutan, and tritan theme variants where the product ships a code or diff view.

---

## 9. Games, maps, and real-time views

| Field | Content |
|---|---|
| **Rule** | Teams, factions, hazards, objectives, and map layers MUST be distinguishable without color, and where color carries a role the player or viewer MUST be able to choose the colors. |
| **Why** | The Xbox Accessibility Guidelines ask that important information be expressed through at least two channels and that color never be the only one; where reliance on color cannot be avoided, the player should be able to choose the colors for individual elements ([XAG 103](https://learn.microsoft.com/en-us/gaming/accessibility/xbox-accessibility-guidelines/103)). |
| **How to verify** | Play or operate the core loop under each simulation. Every friend, foe, pickup, hazard, and route is identifiable at speed. |

**MUST**

- Give each team or faction a shape, outline, or icon in addition to its color.
- Let the user remap colors that carry roles, per element, not only through a global filter.
- Mark map routes, zones, and transit lines with labels or line patterns as well as color.

**SHOULD**

- Ship a few preset schemes tuned for protan, deutan, and tritan players, each validated per section 12, alongside free remapping.

---

## 10. Print, physical, and hardware

| Field | Content |
|---|---|
| **Rule** | Receipts, tickets, labels, packaging, signage, and indicator lights MUST carry their meaning without color. |
| **Why** | Printed output is often grayscale, and a single bicolor LED that switches from red to green is the classic indicator a red-green dichromat cannot read. |
| **How to verify** | Print in grayscale and check every state. For hardware, cover the LED color and name the state from blink pattern, position, or an adjacent label. |

**MUST**

- Encode device states with position, blink pattern, or a labeled icon beside the light, not only with LED color.
- Print status words on receipts and tickets; never rely on a colored stamp or band alone.

**SHOULD**

- Use pattern or hatching for categories on printed maps and charts.

---

## 11. User settings and platform signals

| Field | Content |
|---|---|
| **Rule** | The default design MUST meet this spec without a setting. Where color is still the only differentiator on some surface, the product MUST offer an alternative scheme and SHOULD honor the platform's own signal. |
| **Why** | Apple's guidance calls a setting a last resort or stop-gap, and asks for a setting or alternative color schemes where color-coded content remains ([Apple](https://developer.apple.com/help/app-store-connect/manage-app-accessibility/differentiate-without-color-alone-evaluation-criteria)). Operating-system color filters shift every hue on screen, which helps some users with some content and breaks the product's own colors for others. They are the user's tool, not the product's fix. |
| **How to verify** | Turn on Differentiate Without Color on iOS or macOS, and Windows or Android color filters, and confirm the product still reads correctly and adds its extra cues where it supports the signal. |

**MUST**

- Pass sections 3 to 10 in the default theme. A colorblind mode is additional, never the fix.
- Offer an alternative scheme for any remaining color-only surface (color-coded calendars, heat maps, team colors).

**SHOULD**

- Read `UIAccessibility.shouldDifferentiateWithoutColor` on iOS and `accessibilityDisplayShouldDifferentiateWithoutColor` on macOS, and add shapes or labels when it is on.
- Support `forced-colors` (Windows High Contrast) on the web, keeping states visible with system colors.

**MUST NOT**

- Ship an automatic "daltonize" filter as the product's accessibility answer.
- Hide the alternative scheme more than one level deep in settings.

---

## 12. Testing

| Field | Content |
|---|---|
| **Rule** | Every release that changes color, a chart, or a state MUST be checked on the built product under protan, deutan, and tritan simulation and grayscale, and the palette tokens MUST be checked by script. |
| **Why** | Theming, opacity, and dark mode remap tokens, so the design file is not what ships. Simulation catches most failures cheaply; a script catches regressions before a person looks. |
| **How to verify** | The release record names the four simulations, the screens covered, and the script result. |

**Simulation.** Use a physiologically based model: Brettel, Viénot and Mollon 1997, Viénot, Brettel and Mollon 1999, or Machado, Oliveira and Fernandes 2009 ([project page](https://www.inf.ufrgs.br/~oliveira/pubs_files/CVD_Simulation/CVD_Simulation.html)). Machado's matrices are in Appendix B. WCAG does not endorse a simulator.

| Tool | Where | What it covers |
|---|---|---|
| Chrome DevTools, Rendering, Emulate vision deficiencies | Browser | Protanopia, deuteranopia, tritanopia, achromatopsia, blur ([Chrome DevTools 83](https://developer.chrome.com/blog/new-in-devtools-83)) |
| Puppeteer `page.emulateVisionDeficiency()` | CI | Same set, scriptable |
| Firefox Accessibility Inspector, Simulate | Browser | Protan, deutan, tritan, achromatopsia, contrast loss |
| Color Oracle | Desktop, whole screen | Protan, deutan, tritan, grayscale |
| Grayscale color filter | iOS, Android, macOS, Windows | Grayscale on the device |

**MUST**

- Simulate the built screen, in light and dark themes, not the design file.
- Script a check over the design tokens: every pair of status colors and every pair within each categorical palette meets the thresholds in sections 4 and 6 under protan and deutan simulation.
- Check tritan simulation for any product whose audience skews older or chronically ill.

**SHOULD**

- Include people with color vision deficiency in usability testing of dashboards, charts, and status-heavy flows. Simulation models dichromacy; people tell you whether the screen is usable at speed.
- Run the token script in CI so a palette change cannot regress silently.

**MUST NOT**

- Treat a contrast pass as a color vision pass. Contrast against the background says nothing about whether two foreground colors can be told apart.

---

## 13. Conformance checklist

- [ ] Every state, series, and selection is identifiable in grayscale (§3).
- [ ] Every colored status carries its word or a distinct icon shape on the same element (§3).
- [ ] Adjacent state colors differ by 3:1 between themselves, or a border or label separates them (§4).
- [ ] No red and green, green and orange, or green and brown pair is the only difference between two states (§4).
- [ ] No instruction, error, or support script names a control by color alone; every sold or picked color has a visible name (§5).
- [ ] Chart series are labeled directly or carry distinct markers; the legend matches series order (§6).
- [ ] Categorical palettes are validated; ordered data uses a monotonic-lightness palette; no rainbow or red-green scales (§6).
- [ ] Every chart value is reachable as text (§6).
- [ ] Body links are underlined or meet G183; errors are text plus icon; focus is a shape change (§7).
- [ ] Diffs, logs, and test results keep their meaning with color stripped (§8).
- [ ] Role colors in games and maps carry a shape and can be remapped (§9).
- [ ] Printed output and hardware lights read without color (§10).
- [ ] Default theme passes without a setting; an alternative scheme exists for remaining color-only surfaces (§11).
- [ ] Built screens simulated under protan, deutan, tritan, and grayscale in light and dark; token script passes (§12).

---

## Appendix A. Validated palettes

Worst-pair ΔE00 under Machado 2009 full-severity simulation, computed with the code in Appendix B. Higher is safer. Every palette here collapses in grayscale, so section 3 still applies.

**Okabe and Ito (Color Universal Design).** Eight colors, published by Masataka Okabe and Kei Ito, popularized by [Wong 2011, Nature Methods 8:441](https://www.nature.com/articles/nmeth.1618). Worst pair ΔE00, without black: protan 12.2, deutan 11.6, tritan 10.9.

| Name | Hex |
|---|---|
| Black | `#000000` |
| Orange | `#E69F00` |
| Sky blue | `#56B4E9` |
| Bluish green | `#009E73` |
| Yellow | `#F0E442` |
| Blue | `#0072B2` |
| Vermillion | `#D55E00` |
| Reddish purple | `#CC79A7` |

**Tol bright.** Seven colors, from [Paul Tol's colour schemes, SRON](https://sronpersonalpages.nl/~pault/). Use as given, without interpolation. Worst pair ΔE00: protan 14.2, deutan 14.8, tritan 8.6 (blue `#4477AA` and green `#228833`).

| Name | Hex |
|---|---|
| Blue | `#4477AA` |
| Cyan | `#66CCEE` |
| Green | `#228833` |
| Yellow | `#CCBB44` |
| Red | `#EE6677` |
| Purple | `#AA3377` |
| Gray | `#BBBBBB` |

Tol's note also gives muted (9 colors), vibrant (7), high-contrast (3), and light (9, for labeled cell fills) schemes, all designed to be distinct under color vision deficiency.

**Sequential and diverging.** Viridis and cividis for sequential data; Tol's sunset and BuRd, or ColorBrewer schemes flagged colorblind-safe, for diverging data.

Several of these colors fall below 3:1 against white. When a palette color is used as text, as a thin line, or as the only boundary of a shape, check it against the background per `WCAG-AA-spec.md` and darken or outline it where it fails.

---

## Appendix B. Reference simulation

Machado, Oliveira and Fernandes 2009, severity 1.0 (dichromacy). Convert sRGB to linear RGB, multiply by the matrix, clamp to 0 to 1, and convert back. Compare simulated pairs with CIEDE2000 in CIELAB (D65).

```text
Protanopia
 0.152286   1.052583  -0.204868
 0.114503   0.786281   0.099216
-0.003882  -0.048116   1.051998

Deuteranopia
 0.367322   0.860646  -0.227968
 0.280085   0.672501   0.047413
-0.011820   0.042940   0.968881

Tritanopia
 1.255528  -0.076749  -0.178779
-0.078411   0.930809   0.147602
 0.004733   0.691367   0.303900
```

```python
def to_linear(c):  # c in 0..1
    return c / 12.92 if c <= 0.04045 else ((c + 0.055) / 1.055) ** 2.4

def simulate(rgb, matrix):  # rgb: sRGB 0..1, returns linear RGB
    lin = [to_linear(c) for c in rgb]
    return [min(1, max(0, sum(matrix[i][j] * lin[j] for j in range(3)))) for i in range(3)]
```

The ΔE00 threshold of 10 used in sections 4 and 6 is a working threshold for small marks such as dots, legend chips, and thin lines, chosen because the validated palettes above clear it under red-green simulation and the failing defaults do not. It is not a perceptual standard. A project MAY set a stricter value; it MUST NOT set a looser one without testing with people who have the deficiency.

---

## References

- Birch J. Worldwide prevalence of red-green color deficiency. JOSA A 29(3):313-320, 2012.
- Brettel H, Viénot F, Mollon JD. Computerized simulation of color appearance for dichromats. JOSA A 14(10):2647-2655, 1997.
- Viénot F, Brettel H, Mollon JD. Digital video colourmaps for checking the legibility of displays by dichromats. Color Research and Application 24(4):243-252, 1999.
- Machado GM, Oliveira MM, Fernandes LAF. A physiologically-based model for simulation of color vision deficiency. IEEE TVCG 15(6):1291-1298, 2009.
- Nuñez JR, Anderton CR, Renslow RS. Optimizing colormaps with consideration for color vision deficiency to enable accurate interpretation of scientific data. PLoS One 13(7):e0199239, 2018.
- Crameri F, Shephard GE, Heron PJ. The misuse of colour in science communication. Nature Communications 11:5444, 2020.
- Wong B. Points of view: Color blindness. Nature Methods 8:441, 2011.
- Tol P. Colour schemes. SRON technical note SRON/EPS/TN/09-002, issue 3.2, 2021.
- W3C. WCAG 2.2: [1.4.1 Use of Color](https://www.w3.org/WAI/WCAG22/Understanding/use-of-color), [1.4.11 Non-text Contrast](https://www.w3.org/WAI/WCAG22/Understanding/non-text-contrast.html), [1.3.3 Sensory Characteristics](https://www.w3.org/WAI/WCAG22/Understanding/sensory-characteristics), [G183](https://www.w3.org/WAI/WCAG22/Techniques/general/G183).
- Apple. [Differentiate Without Color Alone evaluation criteria](https://developer.apple.com/help/app-store-connect/manage-app-accessibility/differentiate-without-color-alone-evaluation-criteria).
- Microsoft. [Xbox Accessibility Guideline 103](https://learn.microsoft.com/en-us/gaming/accessibility/xbox-accessibility-guidelines/103).
