# Color by Country Specification

**Conformance target:** No shipped surface uses a color or color pairing that the market it serves reads as political, oppressive, or offensive, and no state is told apart by color alone
**Audience:** Design, brand, marketing, engineering, and whoever owns the release gate
**Scope:** Product screens, printed receipts and tickets, charts, decks, marketing, packaging, and brand marks shipped into a named market
**Companion specs:** `bias-audit-spec.md` (§2 axis register), `disability-and-ableism-spec.md`, `WCAG-AA-spec.md` (1.4.1 Use of Color), `WCAG-AAA-spec.md`
**Register date:** 2026-10-20. Every country entry was checked against a source opened on or before that date; the review cadence in section 3 says when each is due again.

Terms **MUST**, **SHOULD**, and **MAY** follow [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119).

**The core claim:** a palette carries history. Colors that read as neutral success and error states in one market can read as a dictatorship's flag or a party's campaign in another, and a team that picks colors on the screen they are looking at will not see it. The market register comes first; the product's own color semantics sit under it.

**Out of scope:** Contrast ratios, which are `WCAG-AA-spec.md` and `WCAG-AAA-spec.md`. Brand strategy. Color meaning that is the same in every market.

**How to read this document.** Sections 1 to 4 are the rules that apply everywhere. Sections 5 to 10 are the register, one entry per market, grouped by region. Section 11 holds the cross-market registers: market data colors, mourning colors, rainbow restrictions, club colors, gang codes, the pan-African set and the election calendar. Sections 12 to 14 are the release sweep, what to do when the register and the brand collide, and worked examples. Section 15 is the checklist and Appendix A is the machine-readable form of the register.

---

## 1. Purpose and conventions

| Field | Content |
|---|---|
| **Rule** | Each market the product ships into MUST have a dated color register (section 3 and the country sections). Where the register and the product's own color semantics disagree, the register wins and the product semantics change. |
| **Why** | A color rule set for one market gets copied to the next one with the codebase. The register is the only place the difference is written down before it ships. |
| **How to verify** | For each market in the release, the register exists, carries a date and an owner, and every surface in the release has been checked against it. |

Each section below uses the Field/Content table format and lists **MUST / SHOULD / MAY** rules.

---

## 2. Color is never the only cue

| Field | Content |
|---|---|
| **Rule** | Every state a color marks MUST also be carried by a word, an icon, or a sign. Green SHOULD be avoided as a state color where another hue works, because red-green color blindness is the most common form. |
| **Why** | Palettes that pass contrast can still collapse into one color for a color-blind user. Measured with the Machado 2009 deuteranopia simulation, a common money palette fails as a code on its own while every color passes 7:1 on white (table below). Prevalence is lower in the product's core markets than in Europe, but a 2 to 4 percent rate across a national user base is still every fiftieth to twenty-fifth man. |
| **How to verify** | Run every state color pair through a deuteranopia and protanopia simulation, then grayscale the screen. Every state is still identifiable from its text or icon. |

| Pair | Normal vision | Deuteranopia |
|---|---|---|
| Green `#065F46` and amber `#7A460C` | different hue, luminance ratio 1.01:1 | told apart only by a faint hue shift |
| Amber `#7A460C` and red `#991B1B` | amber and red | nearly the same color |

**Prevalence of red-green color vision deficiency, by population.** Peer-reviewed figures; the simulation is Machado, Oliveira and Fernandes, "A Physiologically-based Model for Simulation of Color Vision Deficiency", IEEE TVCG 15(6), 2009 ([project page](https://www.inf.ufrgs.br/~oliveira/pubs_files/CVD_Simulation/CVD_Simulation.html)).

| Population | Men | Women | Source |
|---|---|---|---|
| European descent | about 8% | about 0.4% | [Birch 2012, JOSA A 29(3)](https://opg.optica.org/josaa/abstract.cfm?uri=josaa-29-3-313) |
| East Asian | 4% to 6.5% | not given | Birch 2012 |
| Africa, pooled meta-analysis | 2.7% | 0.3% | [Tilahun et al. 2024, PLoS One](https://pmc.ncbi.nlm.nih.gov/articles/PMC11616826/) |
| Ethiopia, university students | 3.8% | 0.7% | [Mitiku et al. 2020](https://pmc.ncbi.nlm.nih.gov/articles/PMC7364690/) |
| US preschool children by group | White 5.6%, Asian 3.1%, Hispanic 2.6%, Black 1.4% | 0.0% to 0.5% | [Xie et al. 2014, Ophthalmology 121(7)](https://www.ebi.ac.uk/europepmc/webservices/rest/search?query=TITLE:%22color%20vision%20deficiency%20in%20preschool%20children%22&resultType=core&format=json) |
| Global, children and adolescents | 4.4% | 0.6% | [Jeong et al. 2025, Ophthalmology 132(12)](https://www.ebi.ac.uk/europepmc/webservices/rest/search?query=EXT_ID:40769301&resultType=core&format=json) |
| Nepal, medical students | 6.6% | 0.8% | [JIOM Nepal 2017](https://jiomnepal.edu.np/index.php/jiomnepal/article/download/725/671/1327) |
| Saudi Arabia, medical students | about 4.3% | 0% | [Alamoudi et al. 2021](https://pmc.ncbi.nlm.nih.gov/articles/PMC8496699) |
| Puebla, Mexico | 2.2% overall | | [Rev Med UAS 2025](https://www.medigraphic.com/pdfs/sinaloa/uas-2025/uas253d.pdf) |
| Haiti, Dominican Republic, Congo | no study located | | Congo figures of about 1.8% of men circulate second-hand; unconfirmed |

WCAG does not endorse a simulator; the related resources under [Understanding SC 1.4.1](https://www.w3.org/WAI/WCAG22/Understanding/use-of-color) list Vischeck, the AWARE Color Laboratory and the Edge DevTools emulation, with a note that listing is not endorsement.

**MUST**

- Pair every colored state (in, out, blocked, success, error) with its word on the same element.
- Separate any two state colors by luminance as well as hue when they can appear side by side.
- Put a sign and an arrow on every market delta, whichever up and down colors the market uses (section 11).

**SHOULD**

- Prefer a non-green hue for positive states when the market register does not require green.
- Run the simulation on the built screen, not the design file, because theming can remap tokens.

---

## 3. The market register

| Field | Content |
|---|---|
| **Rule** | Each register entry MUST name the color or pairing, what is ruled out, why, and a source, and MUST carry a rule level and an evidence grade. An entry with no source MUST be labeled unconfirmed and still be followed until research confirms or removes it. |
| **Why** | Folklore about color spreads fast and is hard to retire. Labeling it keeps the team honest about what is known, without shipping the risk while it is checked. Grading it tells a reviewer how hard a rule is to overturn. |
| **How to verify** | Every entry has a source link or the label "unconfirmed", a level from the table below, and a grade. A MUST NOT carries a grade of statute or enforcement case, or is a house rule under the grade rule below. |

**What counts as a pairing:** two colors as the dominant colors of one composition. A color on the other, a stripe or split of the two, a two-series chart in the pair, a logo or brand built on it. A small colored element on a neutral surface beside body text is not a pairing. In a dark theme, the near-black background counts as black. A band pattern counts too: two or three colors set as stripes in a flag's order read as that flag with no emblem, so check stripes, ribbons and edge strips, not only pairs.

**Entry format.** Every entry in a country section has the same parts, in this order:

1. A bold rule line: the level, the color, pairing, band order or symbol, and the surface it applies to.
2. The evidence: what happened, when, and with what consequence, ending in the source link.
3. `Counts:` what a designer would ship that triggers the rule.
4. `Does not count:` the nearest safe use, so the rule is not over-applied.
5. `Grade:` the evidence grade.

**Rule levels.**

| Level | When it applies | What it takes to ship anyway |
|---|---|---|
| MUST NOT | A statute, a regulator's order, or a documented enforcement case exists | Nothing. The surface changes. |
| SHOULD avoid | A documented partisan, sectarian or mourning reading exists, with no statute | A written exception signed by the register owner, with the reading named and the reason it does not apply |
| Caution | The reading is plausible and thinly sourced, or confined to one context such as an election window | A note in the review, no sign-off needed |
| No rule | The team checked a piece of folklore and found no source | Nothing. The line exists so the next team does not re-research it |

**Evidence grades.**

| Grade | Means | Example in this spec |
|---|---|---|
| Statute | The text of a law or regulation, on an official site or quoted by a legal publisher | Ley 210-19 on the Dominican flag |
| Enforcement case | A court, police or regulator acted on the color or symbol | The Santo Domingo pizzeria owner held for a month |
| Reputable press | A paper of record, wire service or public broadcaster reports the reading | AFP on the Brazil shirt |
| Academic | A peer-reviewed, museum or reference-registry source documents the meaning | The Tampa Museum of Art on drapo colors |
| Folklore | Widely repeated, or resting on an encyclopedia infobox only | "Red means blood in the DRC", recorded as No rule |

A MUST NOT rests on Statute or Enforcement case, or is a **house rule**: a MUST NOT the product adopts because Reputable press or Academic sources tie the color or symbol to a dictatorship, a genocide, sectarian or gang violence, or death. Any MUST NOT graded below Enforcement case is a house rule by definition, and its grade line states the real grade rather than inflating it. A SHOULD avoid needs at least Reputable press or Academic. Anything resting on Folklore is a Caution at most. Where a source is an encyclopedia page it is marked "last resort"; the entry keeps the grade of what the page reports and MUST get a primary source at its next check.

**Review cadence.** A register entry is a dated fact about a market, and markets move.

- Every register MUST carry a `reviewed` date and MUST be re-read before any release that is the first into that market in 12 months.
- Entries tied to a party, a movement or a mourning period MUST carry a `next check` date: the next election, the end of mourning, or 12 months, whichever is first.
- Retired entries stay in the register with a `retired` date and the reason, so the rule is not re-added from memory.

**Election window.** From 90 days before a scheduled national election to 30 days after it, every SHOULD avoid on a party color in that market is treated as a MUST NOT for marketing, splash screens, receipts and any surface with the brand as its dominant color. Product state colors (success, error, in, out) are not affected. Where a market has no election date because the vote is postponed, as in Haiti, the window is open now and closes 30 days after a published result. The 90 and 30 day figures are a house rule chosen to cover the campaign periods set by the electoral boards cited in the country sections; where a board sets a longer precampaign, as the Dominican JCE does, the entry gives that date instead. The dates in force are in the election calendar in section 11.

---

## 4. Every market

**MUST NOT use a party's logo, symbol, acronym, slogan or leader's image, in any market.** Every country below where party colors matter has them overlapping the national palette, so the colors alone cannot be ruled out, but the marks can, and they turn an ordinary palette into a political statement ([JCE warning on party colors and symbology, Diario Libre](https://www.diariolibre.com/politica/partidos/2025/12/01/jce-intima-a-la-fuerza-del-pueblo-por-propaganda-anticipada/3363880)).

- Counts: logos, flags, mascots, numbers on a ballot, rally photography, election symbols such as a lotus, a hand, a cricket bat, a boat or an umbrella.
- Does not count: a single color the party also uses.

Grade: enforcement case

**MUST NOT put a national flag or coat of arms on a commercial surface without checking that market's law.** Flag laws in the Dominican Republic, Mexico, Brazil, Cuba, Canada, Poland, China, India, Pakistan, Bangladesh, Indonesia, Malaysia, the Philippines, Singapore, Fiji, Kenya, Nigeria, South Africa, Ethiopia, Egypt and Saudi Arabia restrict commercial use, and most laws restrict flags and emblems, not colors ([Ley 210-19](https://mirex.gob.do/pdf/dcep/ley_no.210-19_de_los_simbolos_patrios_dominicanos.pdf), [LEBHN](https://www.diputados.gob.mx/LeyesBiblio/pdf/LEBHN.pdf), [Lei 5.700](https://www.planalto.gov.br/ccivil_03/leis/l5700.htm)). The country sections give each statute.

- Counts: the flag, a partial flag, the coat of arms, bands in the flag's order, a generated image of the flag with the wrong stripe count.
- Does not count: the flag's colors used separately.

Grade: statute

**MUST NOT print religious text (the shahada, Quranic verses, "Allah") on anything that is discarded.** Brands have withdrawn bottle caps and bunting printed with the Saudi flag because it carries the shahada ([The New Arab](https://www.newarab.com/news/riyadh-condemns-world-cup-saudi-beer-after-backlash)).

- Counts: receipts, packaging, disposables, flags of any country that carry the shahada, including the Taliban white flag.

Grade: reputable press

**MUST NOT use a retired regime's flag as retro styling.** The Zaire torch flag, the Rwandan 1962 tricolor, the apartheid flag, the Gaddafi green field, the Saddam-era stars, the Syrian two-star flag, the Francoist eagle, the Imperial German bands and the Confederate flag each appear below with their own sources. A retired flag reads as a position, not as nostalgia.

Grade: enforcement case for the apartheid, Francoist and Imperial German flags; house rule for the rest

**SHOULD avoid the six-stripe rainbow on surfaces that ship into a market listed in the rainbow register (section 11), and SHOULD use it only deliberately elsewhere.** The reading is the same everywhere; the consequence ranges from a boycott to a criminal charge against the licence.

Grade: enforcement case (see section 11)

**SHOULD avoid a skull in a straw hat in every market; MUST NOT in Indonesia.** The One Piece flag became the shared emblem of the 2025 Gen Z protests in Indonesia, Nepal and Madagascar, with raids and seizures in Indonesia (section 10).

- Does not count: a plain skull icon in a warning state.

Grade: enforcement case

---

## 5. Caribbean and Latin America

### Haiti

**MUST NOT pair red and black.** François Duvalier changed the flag's blue to black in 1964, and the black and red flag stood for the dictatorship until the blue and red flag returned on 17 February 1986 ([Britannica](https://www.britannica.com/topic/flag-of-Haiti), [FOTW Haiti](https://www.crwflags.com/fotw/flags/ht.html)). The Duvalierist PUN still uses black, red and white ([Wikipedia](https://en.wikipedia.org/wiki/National_Unity_Party_%28Haiti%29)). No Haitian law applies; this is a house rule.

- Red error text on a white surface beside black body copy is not the pairing.
- A red tag on a near-black dark-theme card is.

Grade: reputable press, academic

**Green carries no cultural restriction.** No reputable source records a Haitian dislike of green. The one political link is the green of the Inite campaign in the disputed 2010 election ([Laurent Dubois, Soccer Politics](https://soccerpolitics.org/2010/11/28/yellow-and-green-in-haiti-a-footnote-to-the-election-crisis/)). Green as a state color stays limited by section 2, for color blindness, not culture.

**Caution: green and yellow, or green and white, as the dominant pair of civic or campaign-style material.** Unconfirmed as a live reading: it echoes the 2010 Inite campaign ([Dubois](https://soccerpolitics.org/2010/11/28/yellow-and-green-in-haiti-a-footnote-to-the-election-crisis/)).

Grade: academic

**Caution: pink (PHTK), blue (Fanmi Lavalas) or red (Pitit Desalin) as the dominant color of civic or campaign-style material.** Pink was Martelly's campaign color ([Dubois](https://soccerpolitics.org/2010/11/28/yellow-and-green-in-haiti-a-footnote-to-the-election-crisis/)). The other assignments rest on party infoboxes only: PHTK pink, Fanmi Lavalas blue, Pitit Desalin red; EDE lists no color ([Wikipedia, PHTK](https://en.wikipedia.org/wiki/Haitian_T%C3%A8t_Kale_Party), [Wikipedia, Fanmi Lavalas](https://en.wikipedia.org/wiki/Fanmi_Lavalas), [Wikipedia, Pitit Desalin](https://en.wikipedia.org/wiki/Platf%C3%B2m_Pitit_Desalin), [fr.wikipedia, EDE](https://fr.wikipedia.org/wiki/Les_Engag%C3%A9s_pour_le_d%C3%A9veloppement)).

- Counts: a pink or blue hero band with a candidate-style portrait or slogan.
- Does not count: blue as the brand color of a screen, red as an error state.

Grade: academic for pink; folklore for the rest

**Election window: open, no date.** The CEP calendar of 27 July 2026 set the first round for 13 December 2026 and the second for 21 February 2027; on 6 October 2026 the CEP postponed the process without a date ([La Libre, 2026-07-28](https://www.lalibre.be/international/amerique/2026/07/28/haiti-les-autorites-annoncent-des-elections-en-fin-dannee-sous-condition-de-securite-Q5Q2RICDGBDCFLTHA224JFUHAQ/), [DH, 2026-10-06](https://www.dhnet.be/dernieres-depeches/2026/10/06/le-conseil-electoral-haitien-reporte-les-elections-R6SNCNXCF5GXFENSLH5DOCPFQY/)). The window is open now and closes 30 days after a published result.

Grade: reputable press

**Caution: compositions that copy Vodou drapo.** A lwa is identified by color plus motif, such as pink with a checkered heart for Ezili ([Tampa Museum of Art](https://tampamuseum.org/sequin-arts-the-flagmakers-of-haiti/)).

- Counts: sequin-flag look, vèvè motifs with their lwa's color.
- Does not count: the colors used plainly.

Grade: academic

**Denomination chips MUST match the BRH note colors and MUST carry the numeral.** Read from the central bank's own note images ([BRH, Billets: images et caractéristiques](https://www.brh.ht/moyens-de-paiements/billets-images-et-caracteristiques/)).

| Note | Dominant color | Portrait or scene |
|---|---|---|
| 10 G | purple | Sanite Bélair |
| 20 G | brown and gold (2001 commemorative) | Toussaint Louverture |
| 25 G | dark blue | Palais de Justice |
| 50 G | olive brown | François Capois |
| 100 G | slate blue gray | Henri Christophe |
| 250 G | yellow khaki | Jean-Jacques Dessalines |
| 500 G | olive green | Alexandre Pétion |
| 1000 G | violet with yellow | Florvil Hyppolite |

- Counts: a chip tinted with another note's color; 10 G and 1000 G are both purple, so the numeral carries the difference.
- Does not count: neutral chips with the figure in text.
- The 50, 100, 250 and 500 bicentennial notes carry the national flag at right. A chip that copies the note art copies the flag, which matters the moment the same component ships to the Dominican Republic.

Grade: statute (central bank)

**Red reads as error or warning,** never as a reward or a win.

- No rule: Haitian law on flag colors in advertising. No statute or decree beyond the constitutional flag definition was found.
- No rule: gang colors. The Al Jazeera explainer on G9, G-Pèp and Viv Ansanm lists leaders and territory and no colors or visual marks ([Al Jazeera, 2024](https://www.aljazeera.com/news/2024/3/13/who-are-haitis-gangs-and-what-do-they-want-all-you-need-to-know)).

### Dominican Republic

**MUST NOT use the flag, the coat of arms, or red, blue and white arranged to resemble the flag.** Ley 210-19 makes it a punishable irreverence to use the flag in whole or in part in commercial promotion, to use its colors so that together they resemble the flag in commercial or political advertising, or to use the coat of arms in for-profit promotion, with 15 to 30 days in prison plus a fine, and any person may file a complaint ([Ley 210-19, arts. 24.5, 24.6, 28.3, 38](https://mirex.gob.do/pdf/dcep/ley_no.210-19_de_los_simbolos_patrios_dominicanos.pdf)).

- Counts: a flag motif on a receipt, splash screen, promo or packaging; quartered red and blue blocks with a white cross; the coat of arms.
- Does not count: red and blue used separately, such as a red error tag on a blue-branded screen.

Grade: statute

**MUST NOT combine Dominican and Haitian national colors or symbols in one composition.** In 2019 a Santo Domingo pizzeria owner was held for a month and his boxes and stickers seized for a sign that put Dominican symbols with Haitian flag colors ([El Nuevo Diario](https://elnuevodiario.com.do/dictan-prision-preventiva-contra-hombre-usaba-simbolos-patrios-en-letrero-de-su-negocio/)).

- Counts: any surface shown in the Dominican Republic that carries both countries' flags or national color sets.
- Does not count: separate Haitian surfaces shipped only in Haiti.

Grade: enforcement case

**SHOULD avoid one party's color as the dominant color of a brand or campaign, most of all in the run-up to an election.** Party colors are an everyday political code (PLD purple with a yellow star, Fuerza del Pueblo green with a cayena flower, PRM blue and white, PRSC red, PRD white), and the electoral board treats a party's colors as evidence of campaigning ([Lony Fernández](https://www.lonyfernandez.com/post/uso-de-los-colores-en-la-pol%C3%ADtica-dominicana), [Diario Libre](https://www.diariolibre.com/politica/partidos/2025/12/01/jce-intima-a-la-fuerza-del-pueblo-por-propaganda-anticipada/3363880)). No law binds a business, and no brand has been penalized; the risk is being read as partisan.

- Counts: purple with yellow, dark green with a flower motif, either as the dominant pair of a composition; green against purple as the only two series of a chart or the two sides of a toggle.
- Does not count: green for cash coming in, purple as one series among several, red, blue or white as ordinary UI colors.

Grade: reputable press

**Election window: 20 February 2028 (municipal) and 21 May 2028 (presidential and congressional).** Article 209 of the Constitution fixes the third Sunday of May and the third Sunday of February every four years ([Wikipedia, last resort](https://en.wikipedia.org/wiki/Elections_in_the_Dominican_Republic)). The JCE has ruled that the precampaign cannot start before the first Sunday of July 2027, with fines of 1 to 200 minimum salaries for early rallies under Ley 20-23 art. 308 ([Acento, 2025-02-05](https://acento.com.do/politica/jce-advierte-periodo-de-precampana-y-campana-electoral-aun-no-han-iniciado-9452522.html)); Participación Ciudadana puts the hard line at 25 July 2027 ([Acento, 2026-05-24](https://acento.com.do/politica/participacion-ciudadana-alerta-la-campana-del-2028-ya-empezo-aunque-la-ley-lo-prohibe-9684916.html)). These rules bind parties, not brands. For this spec the window opens 25 July 2027 and closes 25 July 2028, 30 days after the 25 June runoff.

Grade: statute as reported by the electoral board

**Caution: baseball club colors on a sports or gaming surface.** Licey blue, Escogido red and Águilas yellow and black; the colors and sources are in section 11.4. Blue against red also overlaps the PRM and PRSC pair above.

Grade: folklore (club pages only)

**Denomination chips MUST match the BCRD note colors and MUST carry the numeral.** Read from the central bank's 2025-series images ([BCRD, Billetes en circulación](https://bancentral.gov.do/a/d/6064-billetes-en-circulacion)). The 2025-series 100 and 500 entered circulation on 2 June 2026 and older notes stay valid ([Revista Mercado, 2026-06-05](https://revistamercado.do/money-invest/daily-news/llegan-nuevos-billetes-en-rd-que-pasa-con-los-viejos-de-rd50-rd100-y-rd500-que-tienes-en-el-bolsillo/)).

| Note | Dominant color | Front |
|---|---|---|
| RD$50 | purple | Catedral Primada |
| RD$100 | orange red | Duarte, Sánchez, Mella |
| RD$200 | pink | Hermanas Mirabal |
| RD$500 | teal green | Salomé Ureña and Pedro Henríquez Ureña |
| RD$1,000 | red | Palacio Nacional |
| RD$2,000 | blue | Emilio Prud'Homme and José Reyes |

- Counts: 100 and 1,000 are both warm red and 200 pink sits beside both, so the numeral carries the difference.
- Does not count: neutral chips with the figure in text.

Grade: statute (central bank)

### Cuba

**MUST NOT use the flag or coat of arms in advertising, on merchandise, or crossed with another national flag.** Ley 128/2019 art. 44.1 prohibits the flag in communications with advertising or commercial ends and "cruzada junto a otra bandera nacional"; art. 62 prohibits the coat of arms in advertising, on articles of non-official use, and as part of other figures; the transitional provision sets a warning or a 200-peso fine where the act is not a crime ([Gaceta Oficial No. 71, 2019-09-19](https://instituciones.sld.cu/facultadfinlayalbarran/files/2020/01/ley-128-sobre-los-simbolos.pdf)).

- Counts: the flag or lone star on a splash screen, receipt, promo or packaging; the arms as a watermark; a Cuban and foreign flag side by side.
- Does not count: red, white and blue used separately.

Grade: statute

### Jamaica

**MUST NOT set orange and green as two opposed sides; SHOULD avoid either as the dominant color of civic or campaign-style material.** Orange is the PNP's color and green the JLP's. A JLP councillor said in 2008 she was shot "for no other reason than because I wear green"; a 2011 column warns that an orange shirt in a JLP area "could prove to be very detrimental to one's health"; in February 2024 a JLP councillor confronted a man over an orange shirt and armband and drew a firearm ([Gleaner, 2008-07-13](https://old.jamaica-gleaner.com/gleaner/20080713/cleisure/cleisure4.html), [Observer, 2011-09-12](https://www.jamaicaobserver.com/2011/09/12/colour-me-mad/), [Observer, 2024-02-06](https://www.jamaicaobserver.com/takesstyleout/2024/02/06/pnp-condemns-jlp-councillors-altercation-man-orange-citing-intimidation-assault-jlp-councillor-claims-self-defence/)). Garrison communities, each controlled by one party, account for most murders, so the color code is a street code, not only a ballot code.

- Counts: orange versus green in a two-option control, chart or map; an orange or green hero band on a civic message; agent uniforms or branded wristbands in either color in Kingston.
- Does not count: orange as a warning state, green as a success state, black, gold and green as the flag.

Grade: enforcement case, reputable press

**Red, gold and green bands read as Rastafari in Jamaica and its diaspora.** See the pan-African set in section 11; the reading is religious, not partisan, and carries no restriction.

### Puerto Rico

**Caution: a black and white rendering of the flag in neutral product, and the shade of blue in any flag rendering.** Since 4 July 2016 the all-black flag has been the anti-PROMESA protest symbol; light blue signals independence, dark blue statehood, medium blue the current status ([Wikipedia, Flag of Puerto Rico, last resort](https://en.wikipedia.org/wiki/Flag_of_Puerto_Rico)).

- Counts: a monochrome flag icon, a flag on a dark theme rendered in white and black.
- Does not count: red, white and blue as separate UI colors.

Grade: folklore

### Trinidad and Tobago

**MUST NOT use the flag as a trade mark or fasten advertising to it.** The National Guidelines on the Usage of National Emblems under the National Emblems (Regulation) Act Chap. 19:04 state the flag "should not be used as a commercial trade mark" and that nothing may be placed on it; the Trade Marks Act 2015 s. 60 bars registering a mark containing a state flag without authorization ([TTIPO, 2021-09-27](https://internationalipcooperation.eu/sites/default/files/caripi-docs/2021-09/TTIPO%20-%20FLAGS%20AND%20EMBLEMS%2027%2009%202021.pdf)).

Grade: statute

**Caution: red and yellow as two opposed sides.** PNM is red with the balisier flower, UNC yellow with a rising sun ([Wikipedia, PNM](https://en.wikipedia.org/wiki/People%27s_National_Movement), [Wikipedia, UNC](https://en.wikipedia.org/wiki/United_National_Congress), last resort).

- Does not count: red, white and black as plain UI colors.
- No rule: gang colors. Police painted over "Rasta City gang colours" on poles in Belmont in 2018, but the colors are not named in print ([Trinidad Express, 2018-06-15](https://trinidadexpress.com/news/local/laventille-bracing-for-crime-spike-after-ramadan/article_1625cf4a-70ff-11e8-bd4d-bf2865de959f.html)).

Grade: folklore

### Guyana

**Caution: any two-color opposition that maps onto the two main parties.** The PPP/C draws its base from Indo-Guyanese voters and the PNCR from Afro-Guyanese voters, and voting follows that line ([Conversation Tree](https://conversationtree.gy/?p=2731)). The party colors themselves (commonly given as PPP red and PNC green) could not be sourced: unconfirmed.

Grade: academic for the ethnic base; folklore for colors

### Bahamas

**Caution: red, gold or yellow, and green as dominant campaign-style colors.** The FNM is red and the PLP gold and blue; in 2012 the Prime Minister mocked the PLP's "Gold Rush" with "they ain't gold, they're yellow" and placed the DNA as green ([Tribune, 2012-03-28](http://www.tribune242.com/news/2012/mar/28/pm-plp-are-yellow-not-gold)).

- Does not count: aquamarine, gold and black as the flag palette in neutral use.

Grade: reputable press

### Barbados, Panama, Guatemala, Chile

No rule. Only party infoboxes exist (BLP red and gold; no color for the DLP), and no flag-use statute has been checked for any of the four. Next check: Chile's Ley 20.537 and Panama's Ley 34 de 1949.

### Costa Rica

**Caution: green and white as the dominant pair of civic material.** The PLN is nicknamed the "verdiblancos" ([Wikipedia, PLN, last resort](https://en.wikipedia.org/wiki/National_Liberation_Party_%28Costa_Rica%29)).

- Does not count: a green success state on a white screen.

Grade: folklore

### Nicaragua

**MUST NOT pair red and black.** It is the FSLN flag, flown by Ortega beside the national flag ([Diario las Américas via AP, 2019-08-28](https://www.diariolasamericas.com/america-latina/regimen-sandinista-y-oposicion-disputan-banderas-nicaragua-n4183513)).

Grade: reputable press; house rule

**SHOULD avoid blue and white as bands, ribbons or wristband motifs.** From 2018 police detained people for carrying the flag or blue-and-white bracelets; one businessman reports 39 detentions, and in August 2020 a shopkeeper was held for four hours and her flags seized ([VOA, 2020-06-24](https://www.vozdeamerica.com/a/centroamerica_criminalizado-el-uso-de-la-bandera-dicen-opositores-en-nicaragua/6064595.html), [Observador via Confidencial, 2020-09-14](https://observador.cr/gobierno-de-daniel-ortega-sigue-persiguiendo-a-quienes-venden-banderas-nacionales/)). The government then reclaimed the flag for its own displays, so the reading cuts both ways.

- Counts: blue-white-blue edge strips, ribbon or bracelet imagery, protest-style photography.
- Does not count: blue as a brand color on a white screen.

Grade: enforcement case

### Honduras

**SHOULD avoid red and black as the dominant pair, and red-white-red bands.** Libre's colors are red and black, the Liberal flag is red, white and red, and the National Party is blue; a Liberal candidate campaigned in 2013 on "el negro y rojo es traición" ([La Prensa, 2013-07-15](https://www.laprensa.hn/honduras/el-negro-y-rojo-es-traicion-mauricio-villeda-DDLP333451), [Wikipedia, Libre](https://en.wikipedia.org/wiki/Liberty_and_Refoundation), [Wikipedia, Partido Nacional](https://en.wikipedia.org/wiki/National_Party_of_Honduras)).

- Does not count: a red error tag on white, blue as a brand color.

Grade: reputable press

### El Salvador, Honduras and Guatemala: gang numbers

**MUST NOT feature the numbers 13 or 18 on tickets, tiers, promos or jersey-style graphics.** They are the MS-13 and Barrio 18 identity marks; of 66 clubs in El Salvador's top three leagues only 14 still assign shirt numbers 13 or 18, and players from gang areas have been beaten over them ([InSight Crime](https://insightcrime.org/news/analysis/how-gangs-have-disturbed-the-math-of-football-in-el-salvador), [Barrio 18 profile](https://insightcrime.org/el-salvador-organized-crime-news/barrio-18-profile/)). MS-13 "blue and white" and school color bans could not be sourced: unconfirmed.

- Counts: a "lucky 13" promo, a 13th or 18th loyalty tier shown as a badge, numbered tickets with the number as hero.
- Does not count: 13 or 18 in a running count or a date.

Grade: reputable press

### El Salvador

**No commercial restriction in the flag law.** The Ley de Símbolos Patrios permits personal use of the symbols with respect (art. 26) and penalizes only public officials (art. 24) ([Justia](http://el-salvador.justia.com/nacionales/leyes/ley-de-simbolos-patrios/gdoc/)).

**Caution: cyan and white as the dominant pair, or blue-white-red as ARENA.** Nuevas Ideas lists cyan and white, ARENA blue, white and red ([Wikipedia, Nuevas Ideas](https://en.wikipedia.org/wiki/Nuevas_Ideas), [Wikipedia, ARENA](https://en.wikipedia.org/wiki/Nationalist_Republican_Alliance), last resort).

- Counts: a cyan hero band with a slogan.
- Does not count: cyan as a link color.

Grade: folklore

### Brazil

**MUST NOT put the flag on product labels or packaging.** Lei 5.700 art. 31 IV lists it as disrespect to the flag, punished by fine ([Planalto](https://www.planalto.gov.br/ccivil_03/leis/l5700.htm)).

Grade: statute

**SHOULD avoid green and yellow as the dominant styling of civic material.** The green and yellow football shirt was claimed by bolsonaristas, many Brazilians avoid it for that reason, and red is the left's counter-color ([AFP, 2026-06-24](https://citizen.digital/article/red-or-green-for-brazil-the-politics-of-world-cup-kits-matter)).

- Counts: CBF-shirt look, flag-styled promos.
- Does not count: a green success state, a yellow warning state.

Grade: reputable press

**MUST NOT dress field staff in all black in Rio favelas; SHOULD avoid red and black blocks on Rio promos.** In Comando Vermelho areas all-black clothing is read as militia and a woman was killed for wearing it; the Flamengo shirt is read as CV ([A Tarde, 2025-04-17](https://atarde.com.br/brasil/sinais-de-faccao-confira-simbolos-que-podem-levar-a-morte-no-brasil-1314682)). Red and black is also Flamengo against Fluminense's maroon and green, and black and white against green and white is Corinthians against Palmeiras in São Paulo ([RSSSF Brazil](https://rsssf.org/colours/brazil.html)).

- Counts: black uniforms for agents, red-black blocks, black-white against green-white as two sides.
- Does not count: black text, a red error state.

Grade: reputable press

### Mexico

**MUST NOT use the flag or coat of arms to promote a product or service.** The law bars using the flag to promote "imagen, bienes o servicios" and requires authorization for the coat of arms, with fines up to 10,000 UMA plus daily fines ([LEBHN, arts. 6, 32 Bis, 56](https://www.diputados.gob.mx/LeyesBiblio/pdf/LEBHN.pdf)).

- Does not count: green, white and red as separate UI colors.

Grade: statute

**Caution: guinda (maroon) or pink as the dominant color of civic messaging.** Guinda is Morena's color and the INE investigated it on election walls; pink was the 2024 opposition's ([Excélsior](https://www.excelsior.com.mx/nacional/ine-indagatoria-bardas-guindas-morena-rechaza/1713154), [Expansión](https://politica.expansion.mx/elecciones/2024/05/16/morena-exige-que-ine-deje-de-usar-color-rosa-apropiado-por-campana-de-xochitl)).

Grade: reputable press

**Caution: yellow against red and white stripes on a sports surface.** América is yellow with blue edges and Chivas red and white stripes ([RSSSF Mexico](https://rsssf.org/colours/mexico.html)).

- No rule: cartel color codes. None found.

Grade: academic (reference registry)

### Venezuela

**SHOULD avoid saturated red as the dominant color of civic material.** "Rojo rojito" is the color of chavismo and the PSUV, though the government's own campaigns have softened it since 2006 ([VOA](https://www.vozdeamerica.com/a/la-campaña-de-nicolas-maduro-se-aleja-del-rojo-copia-a-la-oposicion-y-ofrece-mejorias-venezuela-/7654676.html)).

- Does not count: red error states.

Grade: reputable press

### Colombia

**Caution: red and blue set against each other as two sides.** They are the Liberal and Conservative colors, fought over in La Violencia ([El Universal](https://www.eluniversal.com.co/politica/los-colores-poderosos-aliados-para-ganar-la-presidencia-de-colombia-GA5929901)). In Medellín the same pair is Independiente Medellín against Atlético Nacional's green and white ([RSSSF Colombia](https://rsssf.org/colours/colombia.html)).

- Does not count: red or blue used alone.

Grade: reputable press

### Peru

**SHOULD avoid orange as the dominant color of civic material.** Orange "ha sido siempre el color del fujimorismo" and the Fuerza Popular mark is an orange K; red is read as the left ([El Comercio, 2016-04-07](https://elcomercio.pe/politica/elecciones/elecciones-2016-significan-logos-partidos-394676-noticia/)).

- Does not count: orange as a warning state.

**Caution: flag or coat of arms in advertising, logos or packaging.** A Defense Ministry draft regulation under public consultation in July 2025 would ban them in promotions, logos, packaging and labels; not in force when checked ([Diario Correo, 2025-07-17](https://diariocorreo.pe/economia/dirigente-de-gamarra-advierte-impacto-economico-por-restriccion-de-simbolos-patrios-en-productos-noticia/)).

Grade: reputable press

### Argentina

**SHOULD avoid violet as the dominant color of civic material.** Violet is La Libertad Avanza's color; after the 26 October 2025 midterms Milei said the map "se pintó de violeta" ([El Imparcial, 2025-10-28](https://www.elimparcial.com/columnas/2025/10/28/triunfo-violeta/)).

- Does not count: violet as a chart series.

**Caution: blue and yellow banding, or white with a red diagonal, on a gaming surface.** Boca Juniors is blue with a yellow band and River Plate white with a red sash ([RSSSF Argentina](https://rsssf.org/colours/argentina.html)). Never set the two as the two sides of a control.

- Does not count: the celeste y blanca in neutral use.

Grade: reputable press; academic (reference registry) for clubs

### Bolivia

**MUST NOT reproduce the wiphala as decoration, on garments or accessories, or in any propaganda.** DS 241 makes the seven-color 7 by 7 checker a state symbol with fixed Pantone values (art. 29), bars writing or painting on it or using it in political or personal propaganda (art. 42.1), bars its use as an accessory, rug, garment or uniform part (art. 42.2), and refers insults to art. 129 of the penal code ([Lexivox, DS 241 of 2009](https://www.lexivox.org/norms/BO-DS-N241.html)). It is a live flashpoint: it was burned in anti-MAS protests in November 2019 and the police held a national act of apology ([Los Tiempos, 2019-11-13](https://www.lostiempos.com/node/477925)).

- Counts: any rainbow checker grid or diagonal seven-color pattern; wiphala-style badges or loyalty tiers.
- Does not count: a Pride stripe (stripes, not a grid), the red-yellow-green tricolor in neutral use.

Grade: statute

**Caution: blue as the dominant color of civic material.** MAS-IPSP lists blue ([Wikipedia, last resort](https://en.wikipedia.org/wiki/Movement_for_Socialism_%28Bolivia%29)).

Grade: folklore

### Ecuador

**Caution: red and cyan together with a torch or "RC" mark.** The CNE approved that identity for Revolución Ciudadana on 17 September 2021 ([Expreso, 2021](https://www.expreso.ec/actualidad/fuerza-compromiso-social-desaparece-llama-revolucion-ciudadana-112055.html)).

- Does not count: red and cyan as separate UI colors.

Grade: reputable press

### Uruguay

**Caution: red versus white as two opposed sides.** The Colorado and Blanco (Partido Nacional) identities date from ribbons worn at the 1836 Battle of Carpintería. Unconfirmed: no reachable source yet.

Grade: folklore

### Paraguay

**SHOULD avoid red and blue as two opposed sides; Caution with either as a dominant civic color.** The Colorados are red and the Liberals are "los azules" in everyday press shorthand, with the Colorado president saying the country "se tiñó de rojo" after the 2021 municipals; the names Azules and Colorados date from 1869 ([La Nación, 2021-10-14](https://www.lanacion.com.py/politica/2021/10/14/el-comandante-rojas-pone-fin-a-hegemonia-liberal-en-mbuyapey/), [Country Studies, Paraguay](https://countrystudies.us/paraguay/12.htm)).

- Counts: red versus blue in a two-option control, chart or map.
- Does not count: red, white and blue as the flag, red as an error state.

Grade: reputable press

---

## 6. North America

### United States

**SHOULD avoid the Stars and Stripes in advertising or on disposables.** 4 U.S.C. 8(i) says the flag "should never be used for advertising purposes in any manner whatsoever" and should not be printed on napkins or boxes, but the section carries no penalty ([Cornell LII, 4 U.S.C. 8](https://www.law.cornell.edu/uscode/text/4/8)). In Halter v. Nebraska (1907) the Supreme Court upheld a $50 fine for a beer bottle bearing the flag for advertising ([Cornell LII, 205 U.S. 34](https://www.law.cornell.edu/supremecourt/text/205/34)). Later flag-speech cases make a modern prosecution unlikely, so this is reputational, not criminal.

- Counts: the flag or a flag-field on a receipt, promo banner, packaging.
- Does not count: red, white and blue as separate UI colors.

Grade: statute (no penalty), enforcement case (1907)

**SHOULD avoid red and blue as two opposed sides in civic or financial charts.** Networks fixed red for Republicans and blue for Democrats during the 2000 recount, and the code has held since ([NPR](https://www.npr.org/2014/11/13/363762677/the-color-of-politics-how-did-red-and-blue-states-come-to-be)). Unconfirmed: search excerpt.

- Counts: a two-series chart in saturated red and blue, a red-versus-blue map or toggle.
- Does not count: red error and blue link color on one screen.

Grade: reputable press

**SHOULD avoid a red cap with white block lettering.** Washington Post critic Robin Givhan told NPR the MAGA hat was "weaponized by Charlottesville and by white supremacists" and now carries "dark connotations" regardless of the wearer's intent ([NHPR/NPR, 2019](https://www.nhpr.org/2019-01-27/the-symbol-of-the-maga-hat)).

- Counts: red baseball cap with white capitals in photography, illustration or merchandise.
- Does not count: red as a brand color.

Grade: reputable press

**MUST NOT use the Confederate battle flag.** Walmart, Sears, Kmart and eBay stopped selling it on 22 and 23 June 2015, and eBay called it "a contemporary symbol of divisiveness and racism" ([Engadget](https://www.engadget.com/2015-06-23-online-retailers-stop-selling-confederate-flag.html)).

- Counts: the saltire with stars in any color treatment, "Dixie" styling.

Grade: reputable press

**Caution: solid red or solid royal blue in school-facing or youth material; red-black against blue-black in Chicago.** Bloods wear red and Crips blue; Chicago's Folk Nation gangs wear blue and black and People Nation red and black ([Police Magazine](https://www.policemag.com/articles/nations-at-war-within-windy-city-limits)). California Ed Code 32282 lets districts ban gang-related apparel: Kennedy High School in Fremont prohibits "RED OR ROYAL BLUE shirts, hats, shoelaces, backpacks" ([Fremont Unified](https://fremontunified.org/kennedy/about/policies/dress-code/)), and Shandon JUSD dress-coded a Dodgers jersey and a red Christmas sweater in 2023 ([CalCoastNews](https://calcoastnews.com/2023/09/shandon-schools-ban-red-and-blue-clothing-parents-outraged)). Policy is local and varies.

- Counts: branded apparel or swag in solid red or royal blue shipped to schools; red versus blue as two sides in youth-facing creative.
- Does not count: UI colors.

Grade: enforcement case (school policy), reputable press

**Caution: the rainbow as a brand accent.** Target's comparable sales fell 5.4 percent in Q2 2023, and executives named "the strong reaction to this year's Pride assortment" as a headwind alongside threats to staff ([CBS News](https://www.cbsnews.com/news/targets-pride-backlash-sales-down/)). It reads as a position to both sides; use it deliberately or not at all.

Grade: reputable press

**Red, black and green bands read as Black nationalist (UNIA, 1920).** See the pan-African set in section 11; the reading carries no restriction.

### Canada

**MUST NOT adopt the national or a provincial flag, arms or crest as a mark in connection with a business.** Trademarks Act s.9(1) bars adopting "in connection with a business, as a trademark or otherwise" the Royal Arms, any arms, crest or flag adopted by Canada or a province, and any national flag of a Paris Union country; s.9(2) allows it with consent ([Justice Laws, s.9](https://laws-lois.justice.gc.ca/eng/acts/t-13/section-9-20250401.html)).

- Counts: a maple-leaf flag or provincial flag in a logo, app icon or campaign mark.
- Does not count: red and white as colors, a plain maple leaf not in flag form.

Grade: statute

**Caution: Liberal red, Conservative blue, NDP orange as the dominant color of civic material in election periods.** The Globe and Mail describes federal power as alternating "between Conservative blue and Liberal red" ([Globe and Mail](https://arc-dev.theglobeandmail.com/opinion/editorials/article-a-look-back-at-a-decade-when-canada-shifted-from-blue-to-red)); the NDP's color is orange ([Wikipedia, last resort](https://en.wikipedia.org/wiki/New_Democratic_Party)).

- Does not count: any of them as an ordinary UI color.
- No rule: Quebec's fleurdelisé as a sovereignty marker. No commercial restriction was found ([Wikipedia, last resort](https://en.wikipedia.org/wiki/Flag_of_Quebec)).

Grade: reputable press

---

## 7. Sub-Saharan Africa

### Democratic Republic of the Congo

**MUST NOT use party marks or political figures.** The ruling UDPS uses red, yellow and blue and the opposition PPRD uses yellow and blue, both from the national flag, and the conflict between them is live: the PPRD headquarters in Kinshasa was set on fire during a UDPS march on 4 May 2026 ([Radio Okapi](https://www.radiookapi.net/2026/05/05/actualite/politique/le-siege-du-pprd-incendie-lors-dune-marche-de-ludps-kinshasa), [fr.wikipedia UDPS](https://fr.wikipedia.org/wiki/Union_pour_la_d%C3%A9mocratie_et_le_progr%C3%A8s_social)).

- Counts: party logos, acronyms, leaders' portraits, yellow and blue composed to echo the PPRD logo, AFC/M23 and FRN marks.
- Does not count: the national palette in neutral use.

Grade: reputable press

**MUST NOT use the Zaire flag or its torch emblem.** The light green flag with a yellow disc and an arm holding a red torch was Mobutu's from 1971 until 17 May 1997, and it was flown again in the May 2024 coup attempt ([Britannica](https://britannica.com/EBchecked/topic/1355145), [Wikipedia, Flag of Zaire, last resort](https://en.wikipedia.org/wiki/Flag_of_Zaire)).

- Counts: the torch-and-arm emblem; a green field with a centered yellow disc (SHOULD avoid).
- Does not count: green as a state color.

Grade: reputable press; house rule

**Caution: crowds or leaders dressed in white in civic or campaign-style photography.** UDPS militants camped "tout en blanc" at the Limete headquarters for Étienne Tshisekedi's funeral on 30 May 2019, and at the 22 September 2026 pro-Tshisekedi march the UDPS and Union sacrée leaders were "tous vêtus de blanc" ([Actualite.cd 2019](https://actualite.cd/2019/05/30/obseques-de-tshisekedi-certains-militants-ont-passe-nuit-au-siege-de-ludps), [Actualite.cd 2026](https://actualite.cd/2026/09/22/kinshasa-ludps-et-ses-allies-marchent-sans-coup-ferir)).

- Counts: a white-clad crowd as hero imagery, white uniforms on a march or rally scene.
- Does not count: white backgrounds, a single person in white.

Grade: reputable press

**Caution: black-dominant layouts with condolence cues.** Black is generally the mourning color in francophone Central Africa ([Mount Royal University](https://mrujs.mtroyal.ca/index.php/cf/article/download/746/598)). The one Kinshasa-specific source names "traditional clothing and uniforms" and no color ([Mail and Guardian / AFP](https://mg.co.za/article/2020-04-02-drc-in-mourning-as-funeral-parties-banned)), so the Kinshasa reading stays unconfirmed.

- Does not count: black text.
- No rule: "red means blood in the DRC" has no source.
- No rule: no AFC/M23 or FRN color could be sourced. AFC/M23 held Goma from 27 January 2025 and joined the Kabila-led Front for the Refoundation of the Nation on 12 October 2026 ([Wikipedia, last resort](https://en.wikipedia.org/wiki/Alliance_Fleuve_Congo)).

Grade: academic

**MUST NOT use green and black, or green and white, as the dominant pair of a lottery or betting surface in Kinshasa, and MUST NOT set green against black-and-white stripes.** AS Vita Club is green with black edges, DC Motema Pembe green with white edges, both of Kinshasa; TP Mazembe of Lubumbashi is black and white stripes, so the last pairing reads as Lubumbashi against the capital ([RSSSF Congo-Kinshasa](https://rsssf.org/colours/zaire.html)).

- Counts: green-black or green-white blocks, a green option against a striped one.
- Does not count: green as a success state on a neutral ground.

Grade: academic (reference registry); house rule

**Denomination chips SHOULD match the BCC note colors and MUST carry the numeral.** The BCC lists eight circulating notes, 50 to 20,000 FC ([BCC](https://www.bcc.cd/la-banque/billets-et-monnaie/reconnaitre-les-billets)). Dominant colors: 50 lilac brown, 100 slate blue, 200 lilac olive, 500 blue, 1,000 green, 5,000 orange, 10,000 violet, 20,000 yellow brown ([Wikipedia, last resort](https://en.wikipedia.org/wiki/Congolese_franc); 20,000 confirmed yellow and brown at [Realbanknotes](https://realbanknotes.com/banknote/52833-Congo-Democratic-Republic-p104b-20000-Francs-from-2013); 10,000 confirmed violet at [World Banknotes](https://www.worldbanknotescoins.com/2017/04/congo-democratic-republic-10000-congolese-francs-banknote-2006.html)). The BCC page confirms the denominations; the colors rest on catalogs and should be read off the BCC images before a chip ships.

- Counts: a green "5,000 FC" chip, an orange "1,000 FC" chip, cash-count tiles tinted by amount.
- Does not count: neutral chips with the figure in text.

Grade: statute (central bank) for denominations; folklore for colors

**Election window: December 2028.** The CENI roadmap sets the presidential campaign for November to December 2028 and the vote for December 2028 ([Actualite.cd](https://actualite.cd/2025/04/04/pour-denis-kadima-la-publication-de-la-feuille-de-route-2025-2029-est-la-preuve-que)). For this spec the window opens 1 September 2028.

Grade: reputable press

### Republic of the Congo

**Caution: red as the dominant color of civic material.** Red is the ruling PCT's color ([Wikipedia, last resort](https://en.wikipedia.org/wiki/Congolese_Party_of_Labour)). The March 2026 election returned Sassou Nguesso with 94.9 percent under a nationwide phone and internet blackout, with opposition leaders imprisoned, so a partisan reading is a live risk ([ICIR](https://www.icirnigeria.org/congo-brazzaville-election-boycotts-blackouts-growing-dissent-but-denis-sassou-nguesso-returns-for-fifth-consecutive-term/)).

- Does not count: red error states.

Grade: reputable press for the election; folklore for the color

### Rwanda

**MUST NOT use the 1962 red, yellow and green vertical tricolor.** It was replaced by the 25 October 2001 amendment because red "is associated with bloodshed that has characterized the country since independence", culminating in the 1994 genocide ([FOTW Rwanda](https://www.crwflags.com/fotw/flags/rw.html), [Britannica](https://www.britannica.com/topic/flag-of-Rwanda)).

- Counts: that tricolor in that order, any "R" device on it, retro "old Rwanda" graphics.
- Does not count: red, yellow and green as separate state colors, or the pan-African palette in other markets.

Grade: reputable press, academic

**SHOULD avoid gray or purple remembrance styling in commercial material around Kwibuka, 7 to 13 April, and SHOULD mute festive promos that week.** Gray is the official commemoration color ([The New Times, 2013](https://www.newtimes.co.rw/article/90664/National/public-warned-against-trivialisng-genocide/amp), [AllAfrica, 2026-04-07](https://allafrica.com/stories/202604070077.html)), and Law 59/2018 punishes visual acts that trivialize the genocide with 5 to 7 years ([The New Times](https://www.newtimes.co.rw/article/90517/National/genocide-memorial-change-in-colour-for-mourning), [Law 59/2018](https://www.minijust.gov.rw/fileadmin/user_upload/Minijust/Publications/Laws/Law.Crime_of_Genocide_Ideology_2018.pdf)).

- Counts: gray ribbons, gray "we remember" campaigns.
- Does not count: neutral gray UI.

Grade: statute

### Ghana

**SHOULD avoid red and black as the two dominant colors; MUST NOT on celebratory, promotional or win surfaces.** In southern Ghana funeral dress and decoration are red and black ([Calvin University](https://sites.calvin.edu/mkh2/ghza2016/red), [Cooper Hewitt](https://www.cooperhewitt.org/2018/09/07/adinkra-message-and-medium/)).

- Counts: red and black color blocks, brick red with black on promos, receipts or win screens.
- Does not count: black text on white with a red error state.

Grade: academic; the MUST NOT is a house rule

**Red, gold and green bands with a black star are the flag, not a party color.** The CPP used green, white and red; no source shows the flag set as a party color ([FOTW Ghana](https://www.crwflags.com/fotw/flags/gh.html)). See the pan-African set in section 11.

### Kenya

**MUST NOT use the flag, emblems, or their colors and adaptations in branding without written permission.** The National Flag, Emblems and Names Act covers commercial use, with a fine or up to six months ([Kenya Law](https://new.kenyalaw.org/akn/ke/act/1963/44)).

- Counts: the flag, black-red-green-white bands with the shield.
- Does not count: one of those colors alone.

Grade: statute

**SHOULD avoid ODM orange or UDA yellow as the dominant brand color in campaign periods.** Color is the first marker of party in Kenya ([Nation](https://nation.africa/kenya/news/politics-influencing-fashion-trends-as-campaigns-hot-up-3761908)).

- Does not count: orange as a warning accent.

Grade: reputable press

**Caution: black-dominant civic creative with the flag as a motif, around 25 June.** On 25 June 2024 protesters wearing black and with the flag tied round hands or heads stormed Parliament; about 60 people were killed across the protests ([Citizen Digital](http://citizen.digital/news/june-25-2024-the-day-kenyan-gen-zs-shocked-the-world-n365202)).

- Does not count: black text, a dark theme.
- No rule: no single color is owned by the Gen Z movement.

Grade: reputable press

**Caution: Gor Mahia green against AFC Leopards blue and white on a Nairobi sports surface.** The fan bases are mainly Luo and Luhya, so the pairing reads as ethnic; colors and sources are in section 11.4.

Grade: folklore

### Nigeria

**MUST NOT use the flag or coat of arms without a license.** Unauthorized use in connection with any body is an offense under the Flags and Coat of Arms Act ([PLAC](https://www.placng.org/lawsofnigeria/print.php?sn=188)).

- Does not count: green and white as plain UI colors.

Grade: statute

### South Africa

**MUST NOT display the pre-1994 orange, white and blue flag.** The Equality Court ruled on 21 August 2019 that gratuitous display is hate speech ([Nelson Mandela Foundation](https://www.nelsonmandela.org/news/entry/media-statement-hate-speech-and-displays-of-the-apartheid-flag)); the Supreme Court of Appeal dismissed AfriForum's appeal in April 2023, with the only exceptions artistic, academic or journalistic use in the public interest ([The Star](https://pretorianews.co.za/the-star/news/2023-04-25-eff-welcomes-sca-ruling-against-afriforum-apartheid-flag)).

- Counts: the flag, orange-white-blue horizontal bands with the small central flags, "retro" South African styling.
- Does not count: orange, white and blue as separate colors.

Grade: enforcement case

**MUST NOT use the current flag in trade without ministerial permission.** Section 15 of the Merchandise Marks Act lets the Minister prohibit use of the national flag or any former national flag in connection with any trade, business, profession, occupation or event, and breach is an offense ([Merchandise Marks Act s15](http://www.acts.co.za/merchandise-marks-act-1941/15__use_of_certain_marks_may_b)).

Grade: statute

**SHOULD avoid black, green and gold horizontal bands, saturated red as a dominant civic color, and green with black as a pair.** The ANC flag is three equal horizontal stripes of black, green and gold ([Wikipedia, last resort](https://en.wikipedia.org/wiki/African_National_Congress)); red is the EFF's color and blue the DA's, and the political palette is openly read as "blue or red" ([The African](https://theafrican.co.za/politics/2023-08-17-the-colour-of-our-politics-blue--or-red)); MK party uses green and black ([MK Party](https://www.mkparty.org.za/)).

- Counts: a black-green-gold ribbon or edge strip, red berets in photography, a red-versus-blue two-option control.
- Does not count: a red error state, a blue brand, green as one chart series.

Grade: reputable press

### Ethiopia

**MUST NOT show the plain green, yellow and red tricolor without the blue emblem, and MUST NOT use the flag in any commercial advertisement.** Proclamation 654/2009 art. 23(1) prohibits using "the Flag without its Emblem", punishable by a fine up to 5,000 birr or imprisonment up to one year and six months; art. 23(10) prohibits use "in any form of commercial advertisement", with a legal person paying at least double the fine ([Proclamation 654/2009](http://mesfinbelachew.net/proclamations/654_2009.pdf)). The plain tricolor remains in use by the diaspora and some opposition groups, so it also reads as a political statement.

- Counts: three horizontal bands green over yellow over red, a tricolor edge strip, the full flag on a promo.
- Does not count: green, yellow and red used apart.
- No rule: Tigray's red and yellow could not be sourced to a restriction or enforcement case.

Grade: statute

### Eritrea, South Sudan, Benin, Guinea

No rule. Nothing beyond flag-use conventions or a single-party page is on record.

### Uganda

**MUST NOT show red berets or military-style clothing.** The UPDF gazette of 18 September 2019 made the red beret and tunic official military clothing and banned sale or wearing of resembling attire ([Al Jazeera](https://www.aljazeera.com/news/2019/9/30/uganda-bans-red-beret-bobi-wines-signature-headgear), [Monitor](https://www.monitor.co.ug/uganda/news/national/why-updf-banned-wearing-of-red-beret-1850684)). Bobi Wine said in January 2022 that over 100 NUP supporters were jailed on red-beret charges ([The East African](https://www.theeastafrican.co.ke/tea/news/east-africa/uganda-bobi-wine-dares-police-army-on-red-beret-3680872)).

- Counts: red berets, camouflage, tunic-style uniforms in imagery.

Grade: statute, enforcement case

**Caution: red, white and navy blue as a set; MUST NOT use the umbrella motif (section 4).** These are NUP's colors and symbol ([Wikipedia, last resort](https://en.wikipedia.org/wiki/National_Unity_Platform)); the 15 January 2026 election followed mass arrests of NUP supporters ([Wikipedia, last resort](https://en.wikipedia.org/wiki/2026_Ugandan_general_election)). NRM yellow: unconfirmed.

Grade: folklore

**MUST NOT use rainbow stripes or pride cues.** The Anti-Homosexuality Act 2023 makes "promotion of homosexuality", including advertising and publishing, punishable by 20 years, and a company faces a fine and a 10-year licence suspension or cancellation ([Monitor](https://www.monitor.co.ug/uganda/news/national/the-12-offences-penalties-in-new-anti-gay-legislation-4169476), [HRW](https://www.hrw.org/news/2023/05/30/ugandas-president-signs-repressive-anti-lgbt-law)). The Act does not name the rainbow; the risk is a promotion charge against the licence.

- Counts: rainbow gradients, six-stripe bands, pride-month creative.
- Does not count: a multi-hue chart palette.

Grade: statute

### Tanzania

**Caution: green and yellow as the dominant pair; MUST NOT use the hoe-and-hammer motif (section 4).** They are CCM's colors and symbol ([Wikipedia, last resort](https://en.wikipedia.org/wiki/Chama_Cha_Mapinduzi)). Chadema was barred in April 2025 and its leader charged with treason; the 29 October 2025 vote brought a curfew, an internet shutdown and deaths estimated from over 100 to 700 ([Citizen Digital / AFP](http://citizen.digital/news/hundreds-dead-in-tanzania-post-election-violence-says-opposition-n372270)). Chadema's red, blue and white: unconfirmed.

- Counts: green and yellow blocks, a green-and-yellow ribbon.
- Does not count: green success beside an amber warning.

Grade: reputable press for the crackdown; folklore for colors

### Senegal

**Caution: red and green as the dominant pair of civic material.** PASTEF's colors ([Wikipedia, last resort](https://en.wikipedia.org/wiki/African_Patriots_of_Senegal_for_Work,_Ethics_and_Fraternity)).

Grade: folklore

### Côte d'Ivoire

**SHOULD avoid orange as the dominant color of civic material; Caution: orange set against blue.** Orange is the RHDP's color; the pro-government daily hailed the 27 December 2025 legislative win as "La Côte d'Ivoire en orange" ([La Libre / AFP](https://www.lalibre.be/dernieres-depeches/2025/12/29/legislatives-en-cote-divoire-ecrasante-victoire-du-parti-au-pouvoir-SE4WEZSHMFH4JFN6XHLI5N2TYA/)). The FPI's colors are blue, white and red ([Wikipedia, last resort](https://en.wikipedia.org/wiki/Ivorian_Popular_Front)).

- Counts: an orange brand splash, an orange-versus-blue chart.
- Does not count: orange as a warning accent.

Grade: reputable press

### Cameroon

**Caution: blue and white horizontal multi-stripes.** The Ambazonia flag is nine alternating blue and white stripes with a dove and 13 stars ([Wikipedia, last resort](https://en.wikipedia.org/wiki/Flag_of_Ambazonia)); raising it in 2017 drew live fire and arrests ([The New Humanitarian](https://www.thenewhumanitarian.org/2016/12/15/non-merci-english-speaking-cameroon-rises-wants-republic-ambazonia)). Unconfirmed: search excerpt for the enforcement.

- Counts: blue-white-blue striping, a striped ribbon with a dove.
- Does not count: blue text on white.

Grade: folklore

### Angola

**SHOULD avoid red and green, or red and black, as a dominant pair in civic material.** UNITA supporters rally in "red and green, UNITA's colours" ([IBTimes / AFP, 2022](https://www.ibtimes.com/angolan-parties-wrap-campaigning-tense-election-nears-3604851)); the MPLA's color is red ([Wikipedia, last resort](https://en.wikipedia.org/wiki/MPLA)).

- Does not count: red error beside green success on a neutral surface.

Grade: reputable press

### Mozambique

**Caution: red as the dominant color of civic material.** Red is Frelimo's color ([Wikipedia, last resort](https://en.wikipedia.org/wiki/FRELIMO)). Protests after the 9 October 2024 election ran to 25 January 2025 with 315 deaths counted by Plataforma DECIDE and over 4,000 arrests ([AP](https://www.clickondetroit.com/news/world/2025/04/15/mozambique-carried-out-a-brutal-crackdown-on-post-election-protests-amnesty-says/)).

Grade: reputable press

### Zimbabwe

**SHOULD avoid yellow as the dominant civic color; Caution: red, and the green-yellow-red-black set.** The CCC launched on 24 January 2022 in yellow to break from the MDC's red ([BizNews](https://www.biznews.com/africa/yellow-zimbabwe-new-red)); ZANU-PF officials claimed yellow as theirs on 30 January 2022 and called the CCC's finger symbol satanic ([Nehanda Radio](https://nehandaradio.com/?p=283531)). ZANU-PF's colors are green, yellow, red and black ([Wikipedia, last resort](https://en.wikipedia.org/wiki/ZANU%E2%80%93PF)).

- Counts: a yellow-washed campaign look, a yellow pointed-finger motif.
- Does not count: yellow as a warning state.

Grade: reputable press

### Zambia

**Caution: green or red as the dominant color of civic material.** PF supporters wore green shirts with Lungu's face in 2021 ([Daily Maverick](https://www.dailymaverick.co.za/article/2021-08-11-main-contenders-lungu-and-hichilema-trade-insults-while-zambians-brace-themselves-for-polling-day/)); UPND's colors are red and yellow ([Wikipedia, last resort](https://en.wikipedia.org/wiki/United_Party_for_National_Development)).

Grade: reputable press

### Malawi

**Caution: black, red and green as a set with a cockerel, and blue as a dominant civic color.** MCP's colors and symbol, and the DPP's blue ([Wikipedia MCP](https://en.wikipedia.org/wiki/Malawi_Congress_Party), [Wikipedia DPP](https://en.wikipedia.org/wiki/Democratic_Progressive_Party_%28Malawi%29), last resort).

Grade: folklore

### Namibia

**Caution: red with blue and green in one composition.** SWAPO's colors ([Wikipedia, last resort](https://en.wikipedia.org/wiki/SWAPO)), which overlap the national flag.

Grade: folklore

### Sudan

**Caution: blue-dominant solidarity-style creative.** Blue became the memorial color after Mohamed Mattar was shot on 3 June 2019 in the crackdown blamed on the RSF, and #BlueForSudan came to stand for all the uprising's dead ([Al Jazeera](https://www.aljazeera.com/news/2019/6/13/blueforsudan-why-is-social-media-turning-blue-for-sudan)). Not a restriction; a blue "we stand with" campaign reads as the 2019 memorial.

- Does not count: a blue brand or UI.
- No rule: no RSF color could be sourced.

Grade: reputable press

### Burundi

**Caution: red, green and white as a set, and an eagle-with-machete motif.** CNDD-FDD's colors and symbol ([Wikipedia, last resort](https://en.wikipedia.org/wiki/CNDD%E2%80%93FDD)).

Grade: folklore

### Mali, Burkina Faso, Niger

**SHOULD avoid a plain green field with a centered sun or baobab emblem.** The AES confederation flag, launched in Bamako on 22 February 2025, is a green field with the bloc's logo centered ([Hespress](https://en.hespress.com/104303-sahel-states-alliance-unveils-official-flag-amid-regional-realignment.html)).

- Counts: a green splash screen with a central orange sun, a baobab-on-green promo.
- Does not count: green as a success state.

Grade: reputable press

**Red, gold and green vertical tricolors are the flags of Guinea, Senegal and Mali, not party colors.** See the pan-African set in section 11.

### Togo

**Caution: blue as the dominant civic color.** UNIR's color ([Wikipedia, last resort](https://en.wikipedia.org/wiki/Union_for_the_Republic_%28Togo%29)).

Grade: folklore

### Sierra Leone

**Caution: red set against green as two sides.** APC is red, SLPP is green with a palm tree ([Wikipedia APC](https://en.wikipedia.org/wiki/All_People%27s_Congress), [Wikipedia SLPP](https://en.wikipedia.org/wiki/Sierra_Leone_People%27s_Party), last resort).

- Does not count: red error beside green success on a neutral surface.

Grade: folklore

### Liberia

**Caution: blue, or green with maroon, as the dominant civic color.** CDC blue; Unity Party green and maroon ([Wikipedia CDC](https://en.wikipedia.org/wiki/Coalition_for_Democratic_Change), [Wikipedia UP](https://en.wikipedia.org/wiki/Unity_Party_%28Liberia%29), last resort).

Grade: folklore

### Madagascar

**SHOULD avoid a pirate skull-and-crossbones, above all one wearing a hat.** Gen Z Madagascar's emblem is the One Piece skull with the straw hat replaced by a Betsileo satroka; protests from 25 September 2025 left at least 22 dead by the UN count, and Colonel Randrianirina took power on 14 October 2025 ([AP](https://www.aol.com/articles/gen-z-protesters-united-anime-112159566.html), [Al Jazeera](https://www.aljazeera.com/news/2025/10/14/who-is-in-charge-of-madagascar-after-president-rajoelina-flees)).

- Counts: skull motifs in playful or gaming creative, a straw-hat skull sticker.
- Does not count: a plain warning icon.

Grade: reputable press

---

## 8. Europe

### Russia

**MUST NOT pair blue and yellow, or use white-blue-white bands or rainbow stripes.** Courts have fined and detained people for dyed hair, bracelets, fences and earrings in these colors, with no flag present ([RFE/RL](https://www.rferl.org/a/netyosov-fined--hair-dyed-ukrainian-national-flag/32955201.html), [OVD-Info](https://ovd.info/en/express-news/2026/09/22/student-justice-ministry-academy-has-been-fined-wearing-blue-and-yellow), [HRW](https://www.hrw.org/news/2024/02/15/russia-first-convictions-under-lgbt-extremist-ruling)).

- Counts: two-band layouts, ribbons, prominent paired blocks, rainbow bands or gradients.
- Does not count: blue and yellow far apart in a multi-hue palette. Unconfirmed threshold; enforcement is arbitrary.

Grade: enforcement case

### Belarus

**MUST NOT use white-red-white bands or pair blue and yellow; SHOULD avoid red and white as the dominant pair.** Prosecutions have reached red-white bracelets, curtains and food, and yellow-blue flowers and balloons, with arrests of 7 to 15 days and criminal terms up to 1.5 years ([PEN Belarus](https://penbelarus.org/en/2023/06/27/persecution-for-symbols-belarus-2022.html)).

Grade: enforcement case

### Ukraine, Lithuania, Latvia, Estonia and Moldova

**MUST NOT use orange and black stripes or a military Z or V.** The St George ribbon and Z and V are banned by statute, and the European Court of Human Rights upheld Ukraine's ban ([European Pravda](https://www.eurointegration.com.ua/eng/news/2024/12/12/7200529/), [ERR](https://news.err.ee/1609929956/over-1-000-violations-of-banned-symbols-law-logged-in-4-years)). Russia promotes the same ribbon as official, so it reads as pro-war everywhere else.

- Does not count: orange and black used apart, a Z or V in ordinary text.

Grade: statute

**Caution: red over black as two horizontal bands inside Ukraine; SHOULD avoid it in Poland.** The UPA red-black flag "continues to be a symbol of the Ukrainian nationalist movement" and is widely flown ([Wikipedia, last resort](https://en.wikipedia.org/wiki/Ukrainian_Insurgent_Army)); in Poland it reads as Volhynia, and on 14 August 2025 President Nawrocki urged the Sejm to add it to the banned-symbols catalog ([LIGA.net](https://news.liga.net/en/politics/news/navrotskyi-urged-the-sejm-to-adopt-a-ban-on-the-upa-flag-and-will-discuss-this-with-zelenskyy)).

- Counts: red upper and black lower band, ribbons, two-tone cards in that order.
- Does not count: red text on a dark theme.

Grade: reputable press

### Germany and Austria

**SHOULD avoid black, white and red as three horizontal bands; MUST NOT combine them with an Iron Cross, eagle or war ensign.** The Imperial flags are the far right's stand-in for the banned swastika flag ([Jüdische Allgemeine](https://www.juedische-allgemeine.de/politik/schwarz-weiss-rot-legal/)). Only the swastika version is banned by criminal law; Bremen's decree of 21 September 2020 lets police confiscate the Iron Cross versions and fine up to EUR 1,000, Niedersachsen followed on 1 October 2020, and the NRW Landtag voted on 8 October 2020 to ban the war ensign by decree ([evangelisch.de](https://www.evangelisch.de/inhalte/176471/02-10-2020/weitere-bundeslaender-fuer-verbot-von-reichskriegsflaggen), [LTO](https://www.lto.de/recht/nachrichten/n/nrw-landtag-abstimmung-verbot-reichskriegsflagge-rechtsextremismus-reichsbuerger)).

- Counts: any flag with an Iron Cross on black-white-red, retro "Kaiserreich" styling.
- Does not count: black text, white ground and a red accent.

Grade: enforcement case (state decrees)

**MUST NOT use a red and white checkerboard that starts with a white field (Austria, Croatia).** It is the Ustasha arms, banned in Austria since 2019 ([Balkan Insight](https://balkaninsight.com/2019/02/13/austria-bans-two-croatian-ustasa-symbols/bi/)).

- Does not count: Croatia's current checkerboard, which starts with red.

Grade: statute

### Croatia

**MUST NOT use "Za dom spremni" or the "U" device.** The white-first checkerboard is under Germany and Austria. The Constitutional Court upheld public-order convictions for the salute in 2016 and the High Misdemeanour Court found it breached art. 39 of the constitution in August 2019 ([Wikipedia, last resort](https://en.wikipedia.org/wiki/Za_dom_spremni)); at the 5 July 2025 Zagreb concert police said they would file misdemeanor charges from footage ([tportal](https://www.tportal.hr/vijesti/clanak/pogledajte-delirij-na-bojni-cavoglave-thompson-poveo-i-pozdrav-zds-foto-20250705)).

Grade: enforcement case

### Bosnia and Herzegovina, Kosovo, Serbia

**SHOULD avoid red-blue-white horizontal bands and red-black compositions in Kosovo; Caution on both, and on red-white checkerboards, in Bosnia.** The Pristina Basic Court annulled Gračanica's decision permitting Serbian flags for Vidovdan in June 2025 ([KoSSev](https://kossev.info/court-bans-display-of-serbian-flag-for-vidovdan-in-gracanica-outrage-from-serbian-representatives/)); Kosovo's state flag was designed to avoid "solely red and black or red, blue and white" ([Wikipedia, last resort](https://en.wikipedia.org/wiki/Flag_of_Kosovo)). In Bosnia the Republika Srpska flag is the Serbian tricolor and each color set reads as one constituent people ([Wikipedia, last resort](https://en.wikipedia.org/wiki/Flag_of_Republika_Srpska)). In Belgrade black-and-white stripes against red-and-white is Partizan against Red Star ([RSSSF Serbia](https://rsssf.org/colours/serbia.html)).

- Does not count: blue and yellow, Kosovo's own palette.
- No rule (Serbia): nothing beyond flag display law is on record.

Grade: enforcement case for Kosovo; folklore for Bosnia

### Hungary

**SHOULD avoid red and white horizontal multi-stripes.** The Árpád stripes were the Arrow Cross banner in 1944 and Jobbik's flag from 2006 ([JTA](https://www.jta.org/2006/10/31/lifestyle/nazi-linked-flag-surfaces-in-hungary)).

Grade: reputable press

**MUST NOT show same-sex families, gender transition or the rainbow as Pride on products or surfaces accessible to minors without the required handling.** The June 2021 act bans "depicting or promoting" homosexuality to under-18s; a Budapest office fined bookseller Líra Könyv for not labeling a book with same-sex parents ([Global News / AP](https://globalnews.ca/news/8033058/hungary-book-ban-lgbtq-content/)), and the implementing decree of 6 August 2021 requires closed packaging and bars sale within 200 meters of schools and churches ([Daily News Hungary](https://dailynewshungary.com/homosexual-content-is-officially-banned-in-hungary/)).

- Counts: rainbow-family illustration in onboarding, kids' or family promos, printed inserts.
- Does not count: a spectrum gradient with no Pride reference.

Grade: statute, enforcement case

### Poland

**MUST NOT put the official emblem, flag or national colors on goods for sale; stylized versions are allowed.** Art. 16 of the act on the emblem, colors and anthem bars them on objects intended for commercial trade unless "w formie stylizowanej lub artystycznie przetworzonej"; insulting the flag is up to a year under art. 137 k.k., and a Warsaw court upheld a PLN 471,000 broadcaster fine for a show that stuck flags in dog droppings ([Bankier](https://www.bankier.pl/wiadomosc/Jak-mozna-uzywac-symboli-narodowych-2556429.html), [Rzeczpospolita](https://www.rp.pl/prawo-karne/art13644031-godlo-barwy-i-hymn-rp-flaga-juz-nie-taka-swieta)).

- Counts: the exact white-red flag or crowned eagle on packaging, cards, merch.
- Does not count: white and red as plain colors, a clearly stylized band.

Grade: statute, enforcement case

**SHOULD avoid the rainbow on or near religious imagery; Caution on the rainbow generally.** Three activists were tried for rainbow halos on the Black Madonna of Częstochowa and acquitted on 2 March 2021 ([Crux](https://cruxnow.com/church-in-europe/2021/03/polish-court-acquits-activists-who-put-lgbt-rainbow-on-icon)); almost 100 local governments adopted "LGBT ideology-free" resolutions, which courts began annulling in July 2020 ([Notes from Poland](https://notesfrompoland.com/2020/07/15/polish-courts-annul-lgbt-ideology-free-zones-finding-they-violate-constitution/)).

Grade: enforcement case

### Spain

**MUST NOT use Francoist flag elements.** The Democratic Memory Law fines exaltation of Francoist symbols from EUR 200 to EUR 150,000 ([Democratic Memory Law](https://en.wikipedia.org/wiki/Democratic_Memory_Law)).

- Counts: the eagle of Saint John, the yoke and arrows.
- Does not count: red and yellow, or the current flag.

Grade: statute (via reference page)

**Caution: blue and red vertical stripes against white, or red and white stripes, on a sports surface.** Barcelona, Real Madrid and Atlético; Real against Barça also carries Catalan against unionist politics ([RSSSF Spain](https://rsssf.org/colours/spain.html)).

Grade: academic (reference registry)

### France

**MUST NOT put the tricolor, or blue, white and red juxtaposed so as to resemble it, on anything with an electoral purpose.** Code électoral art. R27 bans the national emblem and "la juxtaposition des trois couleurs : bleu, blanc et rouge" on electoral posters and circulars, except to reproduce a party emblem; the Conseil constitutionnel found a breach in January 2025 for a candidate pictured in a tricolor sash ([Weka](https://www.weka.fr/actualite/elus/article_juridique/professions-de-foi-gare-a-l-utilisation-des-symboles-tricolores-207871/)).

- Counts: any surface a candidate or party could reuse: co-branded civic campaigns, voter-information material.
- Does not count: ordinary commercial surfaces.

Grade: statute, enforcement case

**SHOULD avoid a blue-white-red flame motif.** The Rassemblement National kept the flame on renaming in June 2018; Public Sénat calls it a copy of the Italian MSI logo ([Public Sénat](https://www.publicsenat.fr/actualites/politique/le-parti-de-marine-le-pen-change-de-nom-mais-garde-la-flamme-identitaire-86551)).

- Counts: a tricolor flame as an icon, loader or badge.

Grade: reputable press

**Caution: a yellow high-visibility vest as a motif.** It has been the gilets jaunes' symbol since 17 November 2018 ([Wikipedia, last resort](https://en.wikipedia.org/wiki/Yellow_vests_protests)).

- Does not count: amber warning states.
- No rule: party colors (LR blue, PS pink, LFI red) as a commercial reading. Not sourced.

Grade: folklore

### Italy

**MUST NOT depict the tricolor as something degraded.** Art. 292 c.p. punishes insult to the flag with EUR 1,000 to 5,000 and intentional public damage with up to two years, and extends to any flag in the national colors ([Money.it](https://www.money.it/sapete-che-rovinare-bandiera-e-reato-ecco-cosa-rischia)). No commercial-use restriction was found.

- Counts: a tricolor torn, trampled, in a bin, as a doormat, in a joke.
- Does not count: the flag used respectfully, the colors apart.

Grade: statute

**Caution: a green-white-red flame motif.** The tricolor flame is Fratelli d'Italia's symbol, inherited from AN and the MSI ([Wikipedia, last resort](https://en.wikipedia.org/wiki/Brothers_of_Italy)).

Grade: folklore

### United Kingdom (Northern Ireland)

**SHOULD avoid green-white-orange or red-white-blue as alternating stripes or blocks.** These are sectarian territorial markers painted on kerbs ([CAIN, Ulster University](https://cain.ulster.ac.uk/images/symbols/unionloyal.htm), [Irish News](https://www.irishnews.com/news/northernirelandnews/2018/08/09/news/why-are-kerbs-painted-green-white-and-orange-a-hate-crime--1403237/)).

- Counts: flag-like bands, alternating edge strips on a receipt, bunting patterns.
- Does not count: green or orange used apart.

Grade: reputable press, academic

**Caution: green and orange as two opposed sides in a chart or two-option control.**

Grade: reputable press

### United Kingdom (Scotland)

**Caution: green-and-white hoops and royal blue as two opposed sides, and an orange sash motif.** Section 11.4 makes the two sides a MUST NOT on a betting surface. Celtic's support is largely Irish Catholic and Rangers' Protestant and unionist, and assaults rise on Old Firm weekends ([RSSSF Scotland](https://rsssf.org/colours/scotland.html), [Wikipedia, Old Firm, last resort](https://en.wikipedia.org/wiki/Old_Firm)). No rule binds a business.

- Does not count: green or blue used alone.

Grade: folklore

### Greece, Cyprus and North Macedonia

**MUST NOT use the Golden Dawn meander on black or red.** The Athens Court of Appeals convicted the leadership of running a criminal organization on 7 October 2020, upheld on 4 March 2026; the emblem is a meander in a circle in a Nazi-flag layout ([Wikipedia, last resort](https://en.wikipedia.org/wiki/Golden_Dawn_%28Greece%29)).

- Does not count: a Greek key as a plain border.

Grade: enforcement case (via reference page)

**SHOULD avoid the 16-ray Vergina sun in North Macedonia; Caution in Greece.** The Prespa agreement requires its removal from public use in North Macedonia, carried out from July 2019 ([Greek City Times](https://greekcitytimes.com/2019/08/18/authorities-removing-vergina-sun-public-areas/)).

Grade: reputable press

**Caution (Cyprus): blue-and-white or red-with-crescent styling.** The constitution requires a flag of neutral color, read as excluding Greek blue and Turkish red ([Wikipedia, last resort](https://en.wikipedia.org/wiki/Flag_of_Cyprus)). In Athens, red-and-white stripes against green is Olympiacos against Panathinaikos ([RSSSF Greece](https://rsssf.org/colours/greece.html)).

Grade: folklore

### Belgium

**Caution: an all-black lion on yellow.** The official Flemish lion has red claws and tongue; the version with black claws was promoted by the Flemish SS and "has come to stand for the separatist or otherwise radical sections" ([Wikipedia, last resort](https://en.wikipedia.org/wiki/Flag_of_Flanders)).

Grade: folklore

### Czech Republic

**MUST NOT overprint the flag.** Anyone may use the state flag in a suitable and dignified way, but section 9 bars any text, image or badge on it; breaches are fined up to CZK 10,000, misuse or disparagement up to CZK 30,000 ([Zákony pro lidi, 352/2001](https://www.zakonyprolidi.cz/cs/2001-352)).

Grade: statute

### Romania

**MUST NOT add inscriptions or symbols to the flag.** A June 2023 amendment to Law 75/1994 bars it, with fines of RON 10,000 to 20,000 ([Wikipedia, last resort](https://en.wikipedia.org/wiki/Flag_of_Romania)).

Grade: statute (via reference page)

### Georgia

**Caution: blue and amber as a dominant civic pair.** Georgian Dream's colors ([Wikipedia, last resort](https://en.wikipedia.org/wiki/Georgian_Dream)).

Grade: folklore

### Netherlands, Sweden, Norway, Portugal, Republic of Ireland, Bulgaria, Armenia, Azerbaijan

No rule. Flag acts in these markets set design and official use only, or bar adding marks to the flag ([Riksdagen](https://www.riksdagen.se/sv/dokument-och-lagar/dokument/svensk-forfattningssamling/lag-1982269-om-sveriges-flagga_sfs-1982-269/), [Lovdata](https://lovdata.no/dokument/NL/lov/1898-12-10-1)); Irish flag guidance is advisory and asks that the flag never carry slogans or logos. Orange in the Netherlands is the royal house's livery with no restriction on private use. Party colors were not sourced.

---

## 9. Middle East, North Africa and South Asia

### India

**MUST NOT use the tricolor, the Ashoka Chakra or the State Emblem in commerce without central government permission.** The Emblems and Names Act 1950 and the Flag Code 2002 restrict commercial use ([iPleaders](https://blog.ipleaders.in/indian-national-flag-laws-and-case-laws/)).

- Does not count: saffron, white and green used apart.

Grade: statute

**MUST NOT use a lotus or an open hand as a mark.** Section 4 applies; the BJP lotus and Congress hand are registered election symbols.

Grade: enforcement case (section 4)

**SHOULD avoid saffron and green as two opposed sides; Caution with saffron as a "national" brand color.** Saffron reads as patriotic to some and as BJP-aligned to others, as the 2026 row over the hockey kit showed ([Onmanorama](https://www.onmanorama.com/sports/other-sports/2026/07/31/blue-for-india-is-like-yellow-for-brazil-criticism-mounts-against-saffronisation-of-hockey.amp.html)).

Grade: reputable press

**SHOULD avoid yellow flags, yellow triangular pennants and yellow-and-blue paired flags in Sikh-diaspora or Punjab-facing creative.** Yellow and blue Khalistan flags fly at the Surrey gurdwara where Hardeep Singh Nijjar was shot in June 2023, and Khalistan-flag and Indian-flag crowds clashed at a Brampton temple on 4 November 2024 ([SBS, 2023-09-23](https://www.sbs.com.au/news/article/the-death-of-a-canadian-man-has-brought-attention-to-the-khalistan-movement-what-is-it/iu4aa9g2w), [The Tribune, 2024-11-04](https://www.tribuneindia.com/news/punjab/kids-women-men-being-attacked-khalistani-flags-fly-as-violence-erupts-at-brampton-hindu-temple)). This applies in Canada and the UK as much as in India.

- Counts: a saffron-yellow triangular pennant, yellow and blue as a flag pair.
- Does not count: yellow as a warning state.

Grade: reputable press

**Caution: white as the dominant color of festive or wedding creative.** White is the color of widowhood in Hindu tradition ([Narratively](https://narratively.com/how-widows-vrindavan-got-their-color-back)).

- No rule: Dalit blue as a restricted color could not be sourced.

Grade: reputable press

### Pakistan

**MUST NOT use the flag, a partial flag, or a colorable imitation of it in a trademark, design or for any trade or business without written federal permission.** The Names and Emblems (Prevention of Unauthorised Use) Act lists the flag in its schedule, covers pictorial representations and colorable imitations, and bars their use "for the purposes of any trade, business, calling or profession" ([WIPO Lex, s.2(c), s.3, Schedule item 2](https://www.wipo.int/wipolex/en/text/497221)).

- Counts: the flag or its crescent-and-star on a receipt, splash screen or promo; a green field with a white hoist bar.
- Does not count: green and white as separate UI colors.

Grade: statute

**SHOULD avoid green over red as two horizontal bands with a white crescent and star, and a red, black, green vertical tricolor; MUST NOT use a cricket bat as a mark.** PTI's flag is green over red with a white crescent and star and the PPP flag is a red, black, green vertical tricolor ([Wikipedia PTI](https://en.wikipedia.org/wiki/Pakistan_Tehreek-e-Insaf), [Wikipedia PPP](https://en.wikipedia.org/wiki/Pakistan_Peoples_Party), last resort). Since the 9 May 2023 riots the state has treated PTI material as a target, and the ECP stripped PTI of its cricket bat symbol on 22 December 2023 ([ARY News](https://arynews.tv/ecp-allots-election-symbols-to-145-political-parties/)).

- Counts: a cricket bat as a mark, a green-over-red split with a crescent, a red-black-green stripe set.
- Does not count: green as a success state, red as an error state.

Grade: reputable press for the crackdown; folklore for the flag designs

### Bangladesh

**MUST NOT use the flag in a trademark, design or for trade without written permission** ([Bangladesh Flag Rules 1972](https://en.wikipedia.org/wiki/Flag_of_Bangladesh)).

Grade: statute (via reference page)

**SHOULD avoid Awami League imagery, including black mourning styling around 15 August, and solid red squares or red blindfold imagery in civic creative.** The party has been banned since May 2025 ([PTI via The Week](https://www.theweek.in/wire-updates/international/2025/05/12/fgn52-bangla-awami-ban.html)). On 30 July 2024 tens of thousands turned their Facebook profiles solid red to reject the government's black-badge day of mourning ([TBS News](https://www.tbsnews.net/features/panorama/30-july-2024-day-social-media-turned-red-1501681)). The Awami League flag is green with four red stars and its symbol is a boat ([Wikipedia, last resort](https://en.wikipedia.org/wiki/Awami_League)).

- Counts: a solid red avatar frame, a red cloth over eyes, a boat mark, green with red stars.
- Does not count: red and green as plain UI colors.

Grade: reputable press

### Sri Lanka

**MUST NOT put the lion flag or the Buddhist flag on low-dignity items.** The government has asked retailers to remove such products and ordered action against disrespect of the Buddhist flag ([Daily FT](https://www.ft.lk/News/Sri-Lanka-asks-Amazon-to-remove-bikinis-and-doormats-featuring-its-flag/56-714755), [Tamil Guardian](https://www.tamilguardian.com/node/22748)).

- Counts: apparel, doormats, swimwear, the Buddhist flag's color stripe as decoration.

Grade: enforcement case

**SHOULD avoid red as the dominant color of civic or campaign-style material.** Red is the color of the JVP and its NPP alliance, and the 2022 Gotagogama protesters turned red back on the Rajapaksas with red ribbons and signs ([Counterpoint, 2022-11-16](https://counterpoint.lk/politics-colors-colors-politics/)).

- Counts: a red-dominant civic poster, a bell as a mark.
- Does not count: red as an error state.

Grade: reputable press

### Nepal

**SHOULD avoid the One Piece straw-hat skull on civic or youth marketing.** It was the defining image of the September 2025 Gen Z protests that burned Singha Durbar and toppled the Oli government ([Fortune, 2025-09-24](https://fortune.com/2025/09/24/gen-z-revolution-protest-one-piece-pirate-flag-jolly-roger)).

- Counts: a skull in a straw hat, pirate-flag framing on youth campaigns.
- Does not count: a plain skull icon in a warning state.

Grade: reputable press

### Afghanistan

**MUST NOT show the black, red, green tricolor inside Afghanistan; MUST NOT print the Taliban white flag on anything disposable.** On 21 August 2025 the Taliban arrested 16 young men in Kandahar for raising the tricolor at a private Independence Day gathering ([Afghanistan International, 2025-08-22](https://www.afintl.com/en/202508225386)). The white flag carries the shahada, so section 4 applies to receipts and packaging.

- Counts: black-red-green bands in that order, the tricolor emoji in Afghanistan-facing UI, the white shahada flag on any discarded surface.
- Does not count: black, red or green used apart.

Grade: enforcement case

### Saudi Arabia

**MUST NOT use any national flag, religious symbol or sectarian symbol in commercial material, and MUST NOT print the Saudi flag on any product anywhere.** A 2024 commerce ministry rule bans them from products and promotions, and the flag carries the shahada ([Gulf News](https://gulfnews.com/world/gulf/saudi/saudi-arabia-bans-commercial-use-of-national-religious-and-sectarian-symbols-1.1731838256178)).

- Does not count: green alone.

Grade: statute

### United Arab Emirates

**MUST NOT drop, damage, invert or insult the UAE flag, an emirate flag, a GCC flag or another country's flag in a public place.** Federal Law 2 of 1971 as amended sets 10 to 25 years and a fine of Dh500,000, and Article 176 of the Penal Code covers insulting the state's flag, emblem or symbols ([Gulf News](https://gulfnews.com/uae/government/jail-term-of-10-25-years-and-dh500000-fine-for-insulting-uae-flag-1.75169320)).

- Counts: a flag cropped, inverted, on a doormat, or printed where it will be thrown away.
- Does not count: red, green, white and black as separate colors.

Grade: statute (via reputable press)

### Qatar

**SHOULD avoid rainbow stripes and gradients.** On 21 November 2022 stadium security confiscated rainbow bucket hats and made a journalist change a rainbow shirt, and FIFA said on 30 November that permitted rainbow items were being blocked despite Qatari assurances ([PinkNews](https://thepinknews.com/2022/11/22/fifa-qatar-rainbow-hats-world-cup), [ESPN](https://africa.espn.com/football/story/_/id/37634403/fifa-says-rainbow-items-allowed-stadiums)).

- Counts: six-band rainbow stripes, rainbow gradients, Pride-month creative.
- Does not count: a multi-hue chart palette that is not in spectrum order.
- No rule: maroon is the national color and carries no sourced sensitivity.

Grade: enforcement case

### Bahrain

**SHOULD avoid the Pearl Roundabout monument and six-sail-and-pearl motifs.** The government demolished the monument on 18 March 2011 to erase "bad memories" of the uprising, and the 500 fils coin carrying it was withdrawn ([Al Jazeera, 2011-03-18](https://www.aljazeera.com/news/2011/3/18/bahrain-tears-down-protest-symbol)).

- Does not count: red and white, which are the national colors and carry no sourced protest reading.

Grade: reputable press

### Yemen

**MUST NOT use red barbed-wire lettering with white and green text in a banner layout.** The Houthi sarkha lines streets in Houthi areas with the enemies' names in a red font drawn as barbed wire ([The Conversation, 2024-02-11](https://theconversation.com/america-is-the-mother-of-terrorism-why-the-houthis-new-slogan-is-important-for-understanding-the-middle-east-222865)).

- Does not count: red or green used apart.

Grade: reputable press

### Jordan, Kuwait, Oman, Tunisia, Bhutan, Maldives

No rule. Nothing beyond general flag-use law is on record.

### Israel and Palestine

**SHOULD avoid red, green, black and white composed as the Palestinian flag or a watermelon, and blue and white composed as the Israeli flag, in neutral products.** Either reads as a political statement, and Israel has restricted the Palestinian flag ([CSM](https://csmonitor.com/World/Middle-East/2024/0117/Seeds-of-resistance-Why-watermelon-symbolizes-Palestinian-solidarity), [Times of Israel](https://www.timesofisrael.com/knesset-advances-bill-banning-palestinian-flags-on-university-campuses/)).

- Does not count: those colors as separate UI colors.

Grade: reputable press

**Caution: orange as the dominant color of civic material in Israel.** Orange marked opposition to the 2005 Gaza disengagement and blue marked support, in a street "color war" of ribbons ([CSM, 2005-08-08](https://www.csmonitor.com/2005/0808/p09s01-coop.html)).

Grade: reputable press

**Caution: a full-black page with one line of white text.** Four Israeli dailies ran black front pages reading "A black day for Israeli democracy" on 25 July 2023 after the first judicial overhaul law passed ([CSM, 2023-07-25](https://www.csmonitor.com/World/Middle-East/2023/0725/Israel-s-black-ink-day-Unprecedented-protest-against-judicial-reform)).

- Does not count: dark theme UI.

Grade: reputable press

### Iran

**MUST NOT use the lion and sun emblem or the 1907 to 1979 flag inside Iran; SHOULD avoid it everywhere as a neutral "Iran" mark.** Displaying it is illegal in Iran, it is read as monarchist, and fans carrying it were barred from a 2022 World Cup match ([National Geographic, 2022-11-29](https://www.nationalgeographic.com/history/article/iran-flag-symbolism-history-meaning-controversy)).

- Counts: a lion holding a sword under a sun, a tricolor with the emblem removed.
- Does not count: green, white and red as separate colors.

Grade: reputable press

**SHOULD avoid green as a movement or solidarity signal.** Green was the color of the 2009 opposition movement ([V&A](https://collections.vam.ac.uk/item/O1814476)), and the emblem-free tricolor was its defiance flag ([National Geographic](https://www.nationalgeographic.com/history/article/iran-flag-symbolism-history-meaning-controversy)).

- Does not count: green as a success state.

Grade: academic, reputable press

### Iraq

**MUST NOT use the pre-2008 flag with three green stars or Saddam's handwritten takbir.** Parliament removed the three stars, the Baath Party motto, in January 2008 because the Kurdistan Regional Government refused to fly the Saddam-era flag ([CSM, 2008-01-23](https://www.csmonitor.com/World/terrorism-security/2008/0123/p99s01-duts.html), [Rudaw, 2013-12-18](https://www.rudaw.net/english/kurdistan/18122013)).

- Counts: three green stars on a white band, the old calligraphy, retro "Iraq 1991" styling.
- Does not count: red, white and black as plain UI colors.

Grade: reputable press

**Caution: the current flag and the Kurdistan sun flag as a pair or as sides.** Kurdish parties still object to the 2008 flag as temporary ([Rudaw](https://www.rudaw.net/english/kurdistan/18122013)).

Grade: reputable press

### Syria

**MUST NOT use the red, white, black two-star flag; SHOULD avoid red over white over black bands.** The green, white, black three-star flag replaced it within a day of Assad's fall on 8 December 2024, and the Constitutional Declaration of 13 March 2025 made it official; the two-star flag is tied to the Baathist state of 1963 to 2024 ([Morocco World News, 2024-12-09](https://www.moroccoworldnews.com/2024/12/167431/will-syrias-independence-flag-become-its-new-national-symbol/), [Wikipedia, Flag of Syria, last resort](https://en.wikipedia.org/wiki/Flag_of_Syria)).

- Counts: the old flag emoji or asset in any Syria-facing surface, two green stars on white, red-white-black band order.
- Does not count: green, white and black used apart.

Grade: reputable press

### Lebanon

**MUST NOT use party flags or emblems; SHOULD avoid one party's color as the dominant color of Lebanon-only campaigns.** Party flags are sectarian markers, and the 2019 protests flew only the national flag ([NUS Middle East Institute](https://mei.nus.edu.sg/wp-content/uploads/2020/12/Insight-251-Sectarianism-and-the-Failure-of-Lebanon%E2%80%99s-2019-Uprising.pdf)). Assignments from party pages only: Hezbollah yellow with a green rifle logo, Amal green and red, Free Patriotic Movement orange, Future Movement blue, Lebanese Forces red, white and green, Kataeb green, white and brown, PSP white, blue and red ([Wikipedia, Flag of Hezbollah](https://en.wikipedia.org/wiki/Flag_of_Hezbollah), [Amal](https://en.wikipedia.org/wiki/Amal_Movement), [FPM](https://en.wikipedia.org/wiki/Free_Patriotic_Movement), [Future](https://en.wikipedia.org/wiki/Future_Movement), [LF](https://en.wikipedia.org/wiki/Lebanese_Forces), [Kataeb](https://en.wikipedia.org/wiki/Kataeb_Party), [PSP](https://en.wikipedia.org/wiki/Progressive_Socialist_Party), all last resort).

- Counts: a yellow field with green calligraphy, orange as a campaign color, a cedar in a red circle.
- Does not count: any one of these as a state color.

Grade: academic for the sectarian reading; folklore for the assignments

### Egypt

**MUST NOT use the flag as a commercial symbol, add any slogan, picture or design to it, or print it where it will be worn or discarded.** Law 41 of 2014 sets up to one year or LE30,000 for disrespecting the flag and bars using it "as a commercial symbol"; a department store owner was referred to court in December 2014 for printing the flag on shoe soles ([Egypt Independent via Reuters, 2014-06-01](https://www.egyptindependent.com/egypt-makes-disrespecting-flag-crime-state-media/), [Egypt Independent, 2014-12-25](https://www.egyptindependent.com/?p=2441867)).

- Counts: the flag or the golden eagle on a receipt, packaging, shoe, costume or promo; a flag with a logo overlaid.
- Does not count: red, white and black as separate colors.

Grade: statute, enforcement case

**MUST NOT use the black four-finger hand on yellow (Rabaa).** Displaying it has led to detention ([VOA](https://www.voanews.com/content/egyptians-defiant-over-rabaa-symbol/1800249.html)).

- Does not count: yellow alone.

Grade: enforcement case

**Caution: all red against white with two red bands on a Cairo sports surface.** Al Ahly is all red and Zamalek white with two red bands ([RSSSF Egypt](https://rsssf.org/colours/egypt.html)).

Grade: academic (reference registry)

### Libya

**MUST NOT use a plain green field as a brand or screen background without a mark on it.** The symbol-free green flag was Gaddafi's from 1977 to 2011 and remains in use by loyalists ([Al Jazeera, 2011-02-24](https://www.aljazeera.com/news/2011/2/24/whats-in-a-flag)).

- Counts: a full-bleed unmarked green surface, green armband imagery, "Green Book" styling.
- Does not count: green with content on it, green as a success state.

Grade: reputable press

### Morocco

**MUST NOT alter, deface or disrespect the flag, the motto, the arms or state decorations.** Law 17-05 sets 6 months to 3 years and 10,000 to 100,000 dirhams; on 4 August 2025 a Tiznit court gave six months for burning Throne Day flags ([Le360](https://fr.le360.ma/politique/outrage-aux-emblemes-et-symboles-de-la-nation-voici-ce-que-dit-la-loi-201230/), [Hespress, 2025-08-04](https://en.hespress.com/117515-man-sentenced-to-six-months-in-prison-for-burning-moroccan-flag-in-tiznit.html)).

- Counts: a cropped or recolored flag, the pentagram on a disposable.
- Does not count: red and green as separate UI colors.

Grade: statute, enforcement case

**Caution: the Amazigh flag (blue, green, yellow bands with a red yaz) and the Rif Republic flag.** Le360 cites a 2019 Paris rally by Rif separatists as the aggravated case of outrage to the flag ([Le360](https://fr.le360.ma/politique/outrage-aux-emblemes-et-symboles-de-la-nation-voici-ce-que-dit-la-loi-201230/)). In Casablanca green-and-white against red-and-white is Raja against Wydad, and Wydad's red and white is also read as the monarchy's colors ([RSSSF Morocco](https://rsssf.org/colours/morocco.html)).

Grade: reputable press

### Algeria

**MUST NOT use the Amazigh flag or its blue, green, yellow bands with a red yaz.** The army chief banned any flag but the national flag in June 2019; 18 people were arrested in Algiers on 23 June 2019 and 41 in July, and in August 2019 a court gave one demonstrator ten years ([North Africa Post](https://north-africa.com/algeria-regime-of-general-gaid-salah-arrests-18-for-carrying-berber-flag-increases-repression-of-peaceful-protesters/), [Fanack](https://fanack.com/human-rights-en/amazigh-algeria~123242/)).

- Counts: three horizontal bands of blue, green and yellow in that order, the yaz glyph.
- Does not count: those colors apart.

Grade: enforcement case

### Turkey

**MUST NOT use the gray wolf sign or the MHP's three crescents.** Both are party marks under section 4 ([Wikipedia, Wolf salute, last resort](https://en.wikipedia.org/wiki/Wolf_salute)).

Grade: enforcement case (section 4)

**Caution: orange as the dominant color of civic material.** Orange is the AKP's color ([Wikipedia, last resort](https://en.wikipedia.org/wiki/Justice_and_Development_Party_%28Turkey%29)).

Grade: folklore

**Caution: yellow and navy, red and yellow, or black and white as the dominant pair of a gaming surface in Istanbul.** Fenerbahçe, Galatasaray and Beşiktaş; red and yellow is also the flag ([RSSSF Turkey](https://rsssf.org/colours/turkey.html)).

Grade: folklore

---

## 10. East Asia, Southeast Asia and Oceania

### China

**MUST NOT use the flag or its design as a trademark, a patented design or in commercial advertising, nor in private funerals.** National Flag Law art. 20 ([Chinese text, Wikisource, last resort](https://zh.wikisource.org/wiki/中华人民共和国国旗法_%282020年%29)); the 2020 amendments took effect 1 January 2021 and add inverted display and discarding as offenses ([AFP via The Peninsula](https://s.thepeninsula.qa/article/17/10/2020/China-passes-amendments-outlawing-insulting-national-flag)).

- Does not count: red and yellow as colors.

Grade: statute

**Market data:** rises in red, falls in green (section 11.1).

**MUST NOT render a living person's name in red.** Names of the condemned were written in red, so a red name reads as a death wish ([USC Folklore Archives](https://folklore.usc.edu/?p=43613)).

- Does not count: red seals, red backgrounds, red text that is not a name.

Grade: academic (folklore archive)

**SHOULD avoid white as the dominant color of gifts, envelopes or festive packaging, and red in condolence contexts.** White is the mourning color ([Dignity Memorial](https://www.dignitymemorial.com/en-ca/memorial-services/funeral-traditions/chinese-funeral-etiquette-and-superstitions)).

- Does not count: white UI backgrounds.

Grade: reputable press

**SHOULD avoid a green hat on a man in imagery or merchandise.** "Wearing a green hat" means being a cuckold ([USC Folklore Archives](https://folklore.usc.edu/green-hats-in-chinese-culture/)).

Grade: academic (folklore archive)

**Caution: Winnie the Pooh imagery in China-facing material.** Pooh images were removed from Chinese social media in mid-2017 after memes compared Xi Jinping to the bear, and the 2018 film Christopher Robin got no release ([Wikipedia, last resort](https://en.wikipedia.org/wiki/Winnie-the-Pooh)).

- Counts: a yellow bear in a red shirt beside a leader.
- Does not count: generic bear mascots.

Grade: folklore

### Hong Kong

**MUST NOT use yellow and blue as a two-state legend for merchants or users.** "Yellow" and "blue" shops were the 2019 political boycott lists, and businesses dropped the labels after the National Security Law ([AP](https://www.mvariety.com/?p=43866)).

Grade: reputable press

**SHOULD avoid yellow umbrellas, yellow and black protest-gear pairings, and black or candle campaigns near 4 June.** Police have arrested people for commemorating 4 June ([VOA](https://www.voanews.com/a/6603517.html)).

- Does not count: yellow or black alone.

Grade: enforcement case

**MUST NOT broadcast, perform, print, publish, sell or reproduce "Glory to Hong Kong".** Court of Appeal injunction of 8 May 2024, with carve-outs for academic and news activity ([AFP via Taipei Times](https://taipeitimes.com/News/world/archives/2024/05/09/2003817617)).

Grade: enforcement case

**SHOULD avoid the black bauhinia flag and the "Liberate Hong Kong" flag.** Unconfirmed: no source located yet; followed until one confirms or removes it.

Grade: unconfirmed

**Market data:** rises in green, falls in red, the opposite of the mainland (section 11.1).

### Taiwan

**Caution: green and blue as two opposed sides, above all in election periods.** Green is the DPP camp and blue the KMT camp ([Wikipedia, Pan-Green Coalition, last resort](https://en.wikipedia.org/wiki/Pan-Green_Coalition)).

Grade: folklore

**Caution: the ROC flag itself as a side.** Its canton is the KMT party emblem, independence supporters reject it, and it is never seen at DPP rallies ([Wikipedia, last resort](https://en.wikipedia.org/wiki/Flag_of_the_Republic_of_China)).

- Does not count: the flag on a neutral country selector.

Grade: folklore

**Market data:** red up and green down on Chinese-language surfaces, green up and red down on English ones (section 11.1).

### Japan

**MUST NOT use black and white stripes in celebratory, retail or promotional contexts.** Black and white curtains hang at funerals; red and white is the celebratory pair ([nippon.com](https://www.nippon.com/en/guide-to-japan/gu020007/funeral-etiquette-in-japan.html), [Kōhaku maku](https://en.wikipedia.org/wiki/K%C5%8Dhaku_maku), [ja.wikipedia, kujiramaku, last resort](https://ja.wikipedia.org/wiki/鯨幕)). The black and white curtain became the funeral curtain only from the early Showa era.

- Does not count: black text on white.

Grade: reputable press; house rule

**Caution: a living person's name in red.** Only a folklore page supports it: red ink "suggests the person's life will be cut short", from gravestones where a living spouse's name is painted red ([Tofugu](https://www.tofugu.com/japan/japanese-superstitions/)).

Grade: folklore

**Market data:** rises in red, falls in blue or green by host site, with a sign on every delta (section 11.1).

### South Korea

**MUST NOT render a living person's name in red.** Names of the dead were written in red ([Korea Herald](https://www.koreaherald.com/article/3323892)).

- Does not count: red seals.

Grade: reputable press

**Market data:** rises in red, falls in blue (section 11.1).

**SHOULD avoid red and blue as two opposed sides, and solid red or solid blue as the dominant color of civic material in election periods.** Red has been the conservative color since the Saenuri rebrand in 2012 and blue the Democratic Party's since 2015; K-pop stars avoid both colors at election time ([Korea JoongAng Daily via Daum, 2025-05-25](https://v.daum.net/v/20250525104533083), [Semafor, 2024-04-09](https://www.semafor.com/article/04/09/2024/south-korea-legislative-elections-k-pop-stars-shun-bright-colors)).

- Counts: a red versus blue toggle, chart or map in Korea.
- Does not count: red up and blue down on a stock board.

Grade: reputable press

**Caution: light-stick and candle crowds as civic imagery.** Fans brought group light sticks of every color to the 7 December 2024 impeachment rally, organized by Candlelight Action ([Korea Times, 2024-12-08](https://www.koreatimes.co.kr/southkorea/society/20241208/k-pop-light-sticks-become-new-candle-lights-for-korean-democracy)).

Grade: reputable press

### Thailand

**MUST NOT pair royal yellow with royal imagery in commercial or humorous material.** Article 112 punishes insulting the monarchy with up to 15 years per count, and satirical calendars with yellow ducks drew two years ([CNN](https://amp.cnn.com/cnn/2023/03/08/asia/rubber-duck-jail-scli-intl)).

- Does not count: yellow as a plain UI or brand color.

Grade: enforcement case

**SHOULD avoid red and yellow as two opposed sides.** They were the rival street movements of 2006 to 2014 ([CSM](https://csmonitor.com/World/2010/0421/Thailand-reds-shirts-yellow-shirts-duel-over-victim-compensation)).

Grade: reputable press

**SHOULD avoid bright festive palettes during official royal mourning.** Mourning for Queen Sirikit began 25 October 2025; the one-year mourning attire for civil servants lapses around 25 October 2026, public dark dress was 90 days, and no order suspended entertainment or business ([TAT Newsroom, 2025-10-26](https://www.tatnews.org/2025/10/official-announcement-mourning-practices-following-the-passing-of-her-majesty-queen-sirikit-the-queen-mother/)). Check current guidance before a launch: as of 20 October 2026 no formal end notice was on record.

Grade: statute (government notice)

**Caution: weekday colors on royal dates.** Yellow is Monday and the birthday color of Rama IX and Rama X; light blue is Friday and Queen Sirikit's; purple is Saturday and Queen Suthida's ([Queen Sirikit Museum of Textiles](https://qsmtthailand.org/research/dress-and-color-at-the-thai-court-ca-1850-present/)).

- Counts: royal yellow or light blue in humorous material around 28 July or 12 August.
- Does not count: respectful use; yellow as a warning state.

Grade: academic

### Myanmar

**MUST NOT use red with NLD imagery or the three-finger salute inside Myanmar.** These were the 2021 anti-coup symbols, and the NLD was dissolved in 2023 ([Al Jazeera](https://www.aljazeera.com/news/2023/3/30/us-uk-japan-australia-denounce-dissolution-of-myanmars-nld)). The junta-run election of December 2025 to January 2026 returned the military-backed USDP, with the NLD still dissolved ([Asialink, University of Melbourne](https://asialink.unimelb.edu.au/diplomacy/insights/myanmars-election-reveals-hairline-cracks-military-rule/)).

- Does not count: red as a plain accent.

Grade: reputable press, academic

### Vietnam

**Market data:** the five-color board in section 11.1: green up, red down, yellow reference, purple ceiling, cyan floor.

### Cambodia

**MUST NOT use party marks; Caution: light blue as the dominant color of civic material.** The ruling CPP flag is light blue with the party emblem ([FOTW](https://crwflags.com/FOTW/FLAGS/kh-polit.html)); the only opposition, the Candlelight Party, was barred from the July 2023 election ([LICADHO](https://licadho-cambodia.org/flashnews.php?perm=333)).

- Counts: a candle logo, a rising sun on dark blue (the dissolved CNRP), the CPP angel-and-rice emblem.
- Does not count: light blue as a UI color on its own.

Grade: enforcement case for the party bans; folklore for the color

### Indonesia

**MUST NOT use the national flag in advertising or commercial promotion.** UU 24/2009 art. 24(b) bars using the flag "untuk reklame atau iklan komersial", art. 67 punishes it with up to one year or a Rp100 million fine, and art. 66 punishes insulting the flag with up to five years ([Hukumonline](https://www.hukumonline.com/berita/a/penghinaan-terhadap-bendera-merah-putih--begini-hukumnya-lt64dc5b7ab22a1?page=2)).

- Counts: the red-over-white flag on a receipt, promo, splash screen or packaging.
- Does not count: red and white as separate UI colors.

Grade: statute

**MUST NOT use the One Piece straw-hat skull flag; SHOULD avoid any skull on a black field.** The flag became a national anti-government symbol in July and August 2025; the chief security minister warned of "criminal consequences" and police raided a Central Java printer on 6 August 2025 ([AFP via Fortune, 2025-08-08](https://fortune.com/asia/2025/08/08/indonesia-one-piece-anime-jolly-roger-protest), [Al Jazeera, 2025-08-16](https://www.aljazeera.com/news/2025/8/16/indonesians-raise-anime-pirate-flag-in-protest-as-nation-marks-independence)).

- Counts: the straw-hat Jolly Roger, any skull-and-crossbones mascot or banner, anything beside the national flag or around 17 August.
- Does not count: black as a plain UI color.

Grade: enforcement case

**Caution: solid red or solid yellow as the dominant color of civic-style material.** Red is PDI-P's color; yellow is Golkar's, the New Order's ruling organization from 1971 to 1999 ([PDI-P](https://en.wikipedia.org/wiki/Indonesian_Democratic_Party_of_Struggle), [Golkar](https://en.wikipedia.org/wiki/Golkar), Wikipedia, last resort).

- Counts: a red poster with a bull, a yellow poster with a banyan tree.
- Does not count: red error states, yellow warning states.

Grade: folklore

**SHOULD avoid six-stripe rainbow bands.** No statute names the rainbow, but the broadcasting commission banned LGBT-related broadcasts on 12 February 2016 ([HRW, 2016](https://www.hrw.org/report/2016/08/10/these-political-games-ruin-our-lives/indonesias-lgbt-community-under-threat)).

Grade: reputable press (NGO report)

### Malaysia

**MUST NOT use the Jalur Gemilang, its name or a colorable imitation in trade or business without the Minister's written permission.** Emblems and Names (Prevention of Improper Use) Act 1963 s3(1)(a) ([DNH](https://dnh.com.my/can-the-jalur-gemilang-be-used-in-promotional-activities/)). On 5 September 2026 the National Unity Minister restated the penalty, up to RM20,000 or three years, and warned that AI-generated flag images with the wrong stripe count must be checked before posting ([Bernama, 2026-09-05](https://bernama.com/en/news.php?id=2603268)).

- Counts: the flag or an altered flag in ads, packaging, logos or social promos; generated imagery of the flag.
- Does not count: red, white, blue and yellow as plain colors.

Grade: statute

**SHOULD avoid solid yellow as the dominant color of civic-style material; MUST NOT pair yellow with "Bersih".** On 29 June 2011 the Home Minister declared the yellow Bersih 2.0 T-shirt illegal; HRW counted some 270 people arrested for wearing or selling the shirts ([Lawyers for Liberty](https://www.lawyersforliberty.org/?p=1505), [HRW, 2011-07-13](https://hrw.org/news/2011/07/13/malaysia-investigate-crackdown-pro-democracy-march)).

- Counts: yellow T-shirt imagery, yellow with "clean" or reform slogans.
- Does not count: yellow as a warning state; royal yellow in ceremonial contexts.

Grade: enforcement case

**MUST NOT use rainbow Pride styling on products sold in Malaysia.** Home Ministry officers seized 164 Pride Collection watches from Swatch stores on 13 and 14 May 2023 ([NBC/AP](https://www.nbcnews.com/nbc-out/out-news/malaysia-raids-swatch-stores-seizes-rainbow-pride-watches-rcna86195)); a prohibition order followed in August with up to three years' jail for possession ([Malay Mail, 2023-09-23](https://www.malaymail.com/amp/news/malaysia/2023/09/23/pm-anwar-says-home-ministry-seizure-on-rainbow-swatches-excessive-but-defends-malaysias-anti-lgbt-stance/92465)).

- Counts: six-stripe bands, "Pride" labels, rainbow product lines.
- Does not count: multi-hue chart palettes that do not read as the Pride flag.

Grade: enforcement case

**Caution: green as the dominant color of civic material.** PAS is green and white and its 2022 and 2023 gains were dubbed the "green wave"; UMNO is red and white ([PAS](https://en.wikipedia.org/wiki/Malaysian_Islamic_Party), [UMNO](https://en.wikipedia.org/wiki/United_Malays_National_Organisation), Wikipedia, last resort).

Grade: folklore

### Philippines

**MUST NOT use the flag as a trademark, on commercial labels or designs, on merchandise, or in any advertisement.** RA 8491 s34(c)(6), (g) and (i); s50 sets P5,000 to P20,000 and up to one year, with a company's President or CEO liable ([LawPhil, RA 8491](https://lawphil.net/statutes/repacts/ra1998/ra_8491_1998.html)).

- Counts: the sun and stars, the blue-red-white triangle layout, flag elements on products.
- Does not count: blue, red, yellow and white apart.

Grade: statute

**SHOULD avoid yellow, pink or red as the dominant color of civic-style material; MUST NOT use the yellow ribbon.** Yellow has stood for the opposition since Corazon Aquino and is read as the Liberal Party, red is associated with the Marcoses, and Robredo's 2022 campaign chose pink on 7 October 2021 to escape the yellow label ([GMA, 2021-10-08](https://www.gmanetwork.com/news/balitambayan/balita/806286/robredo-ipinaliwanag-kung-bakit-pink-ang-campaign-color-sa-halip-na-dilaw/story/), [Pacific Island Times, 2021-10-08](https://www.pacificislandtimes.com/post/pink-yellow-and-the-colorful-philippine-presidential-race)).

- Counts: a yellow ribbon, pink with a "kakampink" look, red with Marcos-era imagery, yellow against red or pink as two sides.
- Does not count: yellow warning, red error, pink as one chart series.

Grade: reputable press

### Singapore

**MUST NOT use the flag or its image for commercial purposes outside 1 July to 30 September without approval.** National Symbols Act 2022, in force 1 August 2023: respectful commercial use needs no approval in the National Day period; altered flag designs cannot be produced; offenses carry up to S$30,000 and six months ([MCCY, 2023-07-31](https://www.mccy.gov.sg/about-us/news-and-resources/rules-governing-usage-of-national-symbols-eased-with-clearer-guidelines-on-respectful-use/)).

- Counts: the crescent and five stars, a red-over-white flag motif, a recolored flag, outside the window.
- Does not count: red and white apart.

Grade: statute

**Caution: all-white crowds or uniforms, and light blue, as civic signals.** PAP members wear white; Workers' Party campaigners wear light blue ([PAP](https://en.wikipedia.org/wiki/People%27s_Action_Party), [WP](https://en.wikipedia.org/wiki/Workers%27_Party_%28Singapore%29), Wikipedia, last resort).

Grade: folklore

### Laos, Mongolia, North Korea

No rule. No statute or enforcement on commercial use of these flags or emblems could be sourced.

### Australia

**MAY use the Aboriginal flag commercially without permission or fee; MUST reproduce it whole and present it respectfully.** The Commonwealth bought the copyright and announced free public use on 25 January 2022, including apparel, websites and digital media; Carroll and Richardson Flagworld remains the exclusive licensed maker of physical flags, and Harold Thomas keeps moral rights ([NIAA, 2022-01-25](https://www.indigenous.gov.au/news-and-media/announcements/free-use-aboriginal-flag-secured-all-australians), [HopgoodGanim](https://www.hopgoodganim.com.au/news-insights/aboriginal-flag-copyright-australian-government/)).

- Counts as a breach: a cropped or recolored flag, text or objects over it, manufactured flags or bunting from another maker.
- Does not count: black over red with a yellow disc, shown whole, on a screen or receipt.

Grade: statute

**MUST NOT reproduce the Torres Strait Islander flag without written permission from the Torres Strait Island Regional Council.** The council owns the copyright, requires the original PMS colors and credit to Bernard Namok ([TSIRC](https://tsirc.qld.gov.au/our-work/torres-strait-islander-flag)).

Grade: statute (copyright owner's terms)

**MUST NOT register the national flag as a trade mark (Trade Marks Act 1995 s39) and MUST get PM&C permission to import products carrying it** ([HopgoodGanim](https://www.hopgoodganim.com.au/news-insights/aboriginal-flag-copyright-australian-government/)).

Grade: statute (via law-firm summary)

### New Zealand

**MUST NOT alter the New Zealand flag by adding any letter, emblem or representation; MUST NOT use the Coat of Arms, or "Royal" or "Government" words, in trade so as to suggest official sanction.** Flags, Emblems, and Names Protection Act 1981 ss11, 13, 14; fines to NZ$5,000 for a person and NZ$50,000 for a company ([WIPO Lex](https://www.wipo.int/wipolex/en/text/497108)). There is no ban on commercial use of the plain flag.

- Counts: a logo placed on the flag, "Royal" in a product name, the coat of arms.
- Does not count: the unaltered flag; red, white and blue apart.

Grade: statute

**Caution: black, red and white with a koru composed as the tino rangatiratanga flag in neutral commercial material.** It was chosen as the national Māori flag after a 2009 consultation, has no statutory status, and rose in prominence during the 2025 Treaty Principles Bill debate ([Wikipedia, last resort](https://en.wikipedia.org/wiki/Tino_Rangatiratanga_flag)).

- Does not count: black, red and white used apart.

Grade: folklore

### Fiji

**MUST NOT use the flag or any part of it in a trademark, logo, advertising or for commercial purposes without the minister's prior approval.** National Flag Protection Act 2015, s10 "Commercial use of the Flag" ([Fiji Times](https://www.fijitimes.com.fj/?p=86450), [PacLII](https://paclii.org/fj/legis/num_act/nfpa2015246)). Unconfirmed: commencement by Gazette notice not confirmed.

Grade: statute

### Papua New Guinea

**MUST NOT use the National Emblem in connection with any business or trade without authorization; MUST NOT use the flag or a lookalike so as to suggest authorization.** National Identity Act ss6 and 10 ([consolidated text](https://www.pngbuai.com/300socialsciences/340-laws-legislation/PNG-National-Identity-Act-1971a.html)).

Grade: statute (older consolidation)

### Timor-Leste

**MUST NOT reproduce the flag on product labels or packaging; MUST NOT put the national emblem on private documents; MUST reproduce any symbol exactly to the law's design and colors.** Law 2/2007 arts 1(3), 1(5), 21(3), 23(1)(d); fines USD 100 to 500, doubled on repeat ([WIPO Lex, Portuguese text](https://www.wipo.int/wipolex/en/legislation/details/11060)).

- Counts: flag on packaging, emblem on a receipt or statement, an off-proportion flag.

Grade: statute

### Brunei

**MUST NOT use the Brunei Coat of Arms, the State Seal, or royal standards and seals for trade or business without the Sultan's written permission.** Emblems and Names (Prevention of Improper Use) Act Cap 94 s3; the Schedule lists the crest but not the national flag ([WIPO Lex](https://www.wipo.int/wipolex/en/text/207330)).

- Counts: the red crest, the Sultan's name on a product.
- Does not count: yellow, white and black bands without the crest (Caution only).

Grade: statute

---

## 11. Cross-market registers

| Field | Content |
|---|---|
| **Rule** | The six registers below apply across markets and MUST be checked in the sweep alongside the country entry: market data colors, mourning colors, rainbow restrictions, club colors, gang codes and the pan-African set, plus the election calendar that drives the window rule. |
| **Why** | These readings cut across borders. A green-up chart that is right in New York is wrong in Shanghai, a black and white stripe that is neutral in Paris is a funeral in Tokyo, and a rainbow loader that is a brand flourish in Montreal is extremist material in Moscow. |
| **How to verify** | Each register has a date and a source per row; every row marked unconfirmed is treated at the stricter reading until closed. |

### 11.1 Market data: up and down colors

Every row was read from the exchange's or a major local broker's own stylesheet or help page on 2026-10-20 unless marked otherwise. Hex values are the site's own.

| Market | Rise | Fall | Reference | Source |
|---|---|---|---|---|
| United States | green | red | none | Secondary only: [W3C i18n thread](https://lists.w3.org/Archives/Public/www-international/2005JulSep/0189.html) |
| Canada | green `#0d0` | red | none | [TSX](https://www.tsx.com/) |
| United Kingdom | green `#458B00` | red `#C00` | none | [FT Markets](https://markets.ft.com/data/indices/tearsheet/summary?s=FTSE:FSI); Hargreaves Lansdown uses blue for positive ([HL](https://www.hl.co.uk/shares/stock-market-summary/ftse-100)) |
| Eurozone | green `#108653` | red `#f11c3a` | none | [Boursorama](https://www.boursorama.com/bourse/indices/cours/1rPCAC/) |
| Brazil | green | red | none | [InfoMoney](https://www.infomoney.com.br/cotacoes/b3/indice/ibovespa/) |
| Mexico | green `#2fab07` | red | none | [BMV](https://www.bmv.com.mx/) |
| Argentina | green `#15803d` | red `#b91c1c` | none | [Rava](https://www.rava.com/perfil/MERVAL) |
| Dominican Republic | none | none | none | BVRD publishes a PDF and Excel bulletin, no live board or color legend ([BVRD](https://bvrd.com.do/)) |
| Haiti | none | none | none | BRH rate page lists rates with unsigned variation, no color or arrow ([BRH](https://www.brh.ht/taux-du-jour/)) |
| India | green `#0e9687` | red `#d51131` | none | [Economic Times](https://economictimes.indiatimes.com/markets) |
| China | red `#e02727` | green `#1ac843` | none | [SSE](https://www.sse.com.cn/); [Zhang and Han 2014](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0089193) |
| Hong Kong | green `#4acb70` | red `#c65665` | none | [HKEX](https://www.hkex.com.hk/?sc_lang=en), same on English and Traditional Chinese pages; [AAStocks](https://www.aastocks.com/en/stocks/market/index/hk-index.aspx); [Futu](https://support.futunn.com/en/topic40). Chinese-language broker app defaults: unconfirmed |
| Taiwan | red in Chinese, green in English | green in Chinese, red in English | none | TWSE stylesheet swaps by `:lang(en)` ([TWSE](https://www.twse.com.tw/en/)) |
| Japan | red `#f30` | blue `#06f` or green, by site | none | [Kabutan](https://kabutan.jp/) red and blue; [Oricon](https://life.oricon.co.jp/rank_certificate/news/2053436/) red and green; brokers let users switch ([RetireJapan](https://retirejapan.com/forum/viewtopic.php?p=38912)). JPX itself: unconfirmed |
| South Korea | red `#ff2a2a` | blue `#0096ff` | none | [KRX data portal](https://data.krx.co.kr/contents/MDC/MAIN/main/index.cmd) |
| Vietnam | green | red | yellow reference, purple ceiling, cyan floor | [PHS](https://phs.vn/en/knowledge/what-is-the-reference-price/80); [DSC](https://www.dsc.com.vn/kien-thuc/gia-tran-gia-san-la-gi); [CafeF](https://cafef.vn/du-lieu.chn) |
| Thailand | unconfirmed | unconfirmed | unconfirmed | SET boards are script-rendered ([SET](https://www.set.or.th/en/market/product/stock/quote/COLOUR/price)) |
| Indonesia | unconfirmed | unconfirmed | unconfirmed | no board reachable for a check |
| Philippines | green `#21A690` | red `#FF3729` | none | [Investagrams](https://www.investagrams.com/Stock/PSE:PSEI) |
| Malaysia | green `#218838` | red `#c63948` | none | [KLSE Screener](https://www.klsescreener.com/v2/) |
| Singapore | green `#74ad00` | magenta red `#b90256` | none | [SGX](https://www.sgx.com/securities/securities-prices) |
| Saudi Arabia | green `#23b533` | red | none | [Argaam](https://www.argaam.com/en) |
| UAE | green `#458d37` | red `#dc0a0a` | none | [Mubasher DFM](https://english.mubasher.info/markets/DFM) |
| South Africa | green `#67bc45` | red `#ee2b31` | none | [Sharenet](https://www.sharenet.co.za/v3/index.php) |
| Nigeria | unconfirmed | unconfirmed | unconfirmed | NGX price list is script-driven ([NGX](https://ngxgroup.com/exchange/data/equities-price-list/)) |
| Kenya | green `#8DC442` | red | none | [NSE Kenya](https://www.nse.co.ke/) |
| Egypt | green `#458d37` | red `#dc0a0a` | none | [Mubasher EGX](https://english.mubasher.info/markets/EGX) |
| Turkey | green `#00ba39` | red `#e74c3c` | none | [Borsa Istanbul](http://www.borsaistanbul.com/en) |

**MUST show market rises in red and falls in green in mainland China and on Chinese-language Taiwan surfaces.**

- Counts: tickers, P&L, deltas, candle bodies, up and down arrows.
- Does not count: a receipt total or a balance, which carry no market direction.

**MUST set the pair per interface language, not per territory, in Taiwan, and MUST follow the exchange (green up, red down) in Hong Kong, not the mainland's pair.**

**MUST show rises in red in South Korea and Japan, falls in blue in Korea, and falls in blue or green in Japan according to the host site.** Japanese brokers vary and let users switch, which is why the sign and arrow are not optional.

**MUST use the five-color board in Vietnam:** green up, red down, yellow reference, purple ceiling, cyan floor.

**SHOULD default to green up and red down everywhere else, and MUST pair every delta with a sign and an arrow.** Thailand, Indonesia and Nigeria are unconfirmed. Haiti and the Dominican Republic have no price-board convention, so the product's own pair applies under section 2, which argues against green for the positive state.

Grade: reputable press (exchange and broker documentation); academic for China

### 11.2 Mourning and funeral colors

| Market | Mourning color | What it means for a product | Source |
|---|---|---|---|
| China | White for immediate family, dark for guests; red avoided except for a death over 80 | Keep white off gift envelopes, festive packaging and reward surfaces; keep red off condolence surfaces | [Dignity Memorial](https://www.dignitymemorial.com/en-ca/memorial-services/funeral-traditions/chinese-funeral-etiquette-and-superstitions) |
| Japan | Black; black and white striped curtain at wakes, red and white at celebrations | No black and white stripes or bunting on retail, celebratory or win surfaces | [nippon.com](https://www.nippon.com/en/guide-to-japan/gu020007/funeral-etiquette-in-japan.html) |
| South Korea | Traditionally white hemp; today black suits, white hanbok for some women | Black with white reads as a funeral; avoid white-dominant festive creative aimed at older users | [Korea Times](https://www.koreatimes.co.kr/southkorea/20090527/tips-for-korean-funeral-custom) |
| Vietnam | White robes, sashes and headbands for close family | White sash or headband motifs and white-dominant gift creative read as mourning | [Local Vietnam](https://localvietnam.com/culture/people/vietnamese-funeral-traditions/) |
| India (Hindu) | White; black not worn and may read as disrespectful | Condolence surfaces white-based, not black; avoid white-dominant wedding or festive creative | [Funeral Partners](https://branchstage2.funeralpartners.co.uk/wokingfuneralservice/?p=4008) |
| Thailand | Black or white; during royal mourning the government asks for black or white | Mute festive palettes and promos during royal mourning | [TTG Asia](https://www.ttgasia.com/2016/10/21/thailand-sets-record-straight-for-mourning-period/) |
| Cambodia | White; white "crocodile" flags outside a house of death | White flag or pennant motifs read as a death notice | [Frazer Consultants](https://web.frazerconsultants.com/cultural-spotlight-cambodian-funeral-traditions), [Kiva](https://www-1.kiva.org/blog/cambodia-a-nation-says-goodbye-to-its-former-king) |
| Iran | Black; black cloth on doors and walls in Muharram and Safar | Black-draped layouts and banners read as Muharram mourning | [WikiShia](https://en.wikishia.net/view/Black_Clothing) |
| Egypt | Yellow in antiquity only; modern convention unconfirmed | No product rule; do not cite "Egypt mourns in yellow" as current | [Davey, via Project Gutenberg](https://www.gutenberg.org/files/44379/44379-h/44379-h.htm) |
| Ghana | Red (kobene), brown (kuntunkuni) and blue-black (brisi) adinkra; red for chief mourners | Red and black as the dominant pair of a promo, receipt or win surface reads as a funeral | [Cooper Hewitt](https://www.cooperhewitt.org/2018/09/07/adinkra-message-and-medium/), [Horniman Museum](https://www.horniman.ac.uk/object/HC.1999.368/json) |
| South Africa | All-black dress, cape and doek for a widow | Black-dominant creative with a woman in a head covering reads as widowhood | [Sowetan](https://www.sowetan.co.za/news/south-africa/2020-01-14-mourning-attire-a-culture-or-a-norm/) |
| Ethiopia | Black; black scarf for women | Black scarves and all-black figures read as mourning | [Frazer Consultants](https://web.frazerconsultants.com/cultural-spotlight-ethiopian-funeral-traditions/) |
| Brazil | Purple with black among Catholics | Avoid purple and black as the dominant pair on festive, reward or gift surfaces | [Woodlawn](https://www.woodlawn.org/blog/funeral-rites-across-different-cultures-the-significance-of-color/) |
| Haiti | Gede colors are black, purple and white; Fèt Gede is 1 and 2 November with festivities through the month. Everyday Catholic funeral dress: unconfirmed | Purple and black together in late October or November reads as Gede | [Visit Haiti](https://visithaiti.com/art-culture/photo-journal-fet-gede-day-of-the-dead/), [Wikipedia, Gede, last resort](https://en.wikipedia.org/wiki/Gede_%28Haitian_Vodou%29) |
| Dominican Republic | Black, with white, gray and lilac for older women; in the Cibao, white T-shirts printed with the deceased's face during the nine days | A plain white T-shirt with a portrait reads as a novena; black ribbons read as bereavement | [Acento](https://acento.com.do/cultura/la-muerte-el-duelo-el-luto-los-ritos-y-su-transformacion-social-9344721.html) |
| DRC | Black generally in francophone Central Africa | Black-dominant layouts with condolence cues read as mourning; black text does not count | [Bouchedi-Nzouanga, Convergences francophones 8.1](https://mrujs.mtroyal.ca/index.php/cf/article/download/746/598) |
| Rwanda | Gray, "synonymous with ash", replaced purple by cabinet decision in 2013; mourning week 7 to 13 April | Gray remembrance styling in April reads as official commemoration; mute festive promos that week | [The New Times, 2013-04-04](https://www.newtimes.co.rw/article/90664/National/public-warned-against-trivialisng-genocide/amp), [AllAfrica, 2026-04-07](https://allafrica.com/stories/202604070077.html) |

**MUST NOT use black and white as the two dominant colors, in stripes, bunting or split layouts, on celebratory, retail or win surfaces in Japan, Cambodia or Korea.**

- Counts: alternating stripes, a black panel beside a white panel, black and white ribbon motifs.
- Does not count: black text on a white screen.

**SHOULD avoid white as the dominant color of gift, envelope, festive or reward surfaces in China, Vietnam, Korea, Cambodia and India.**

- Counts: white envelope imagery, white-dominant win screens, white flags or pennants.
- Does not count: a white UI background, white body copy on dark.

**SHOULD avoid black on a condolence or memorial surface for Hindu users, and red on one for Chinese users.**

- Counts: account-closure-on-death flows, beneficiary notices, "in memory" messaging.

**SHOULD avoid purple and black as the dominant pair of festive or reward surfaces in Brazil, and in Haiti from late October through November.**

- Does not count: purple as one chart series, a purple accent on white.

**SHOULD mute festive palettes and promos during a declared mourning period:** Thailand during royal mourning, Rwanda 7 to 13 April.

Unconfirmed: modern Egyptian mourning color, Thai widow lilac, Haitian everyday Catholic funeral dress, Kinshasa-specific practice.

Grade: reputable press and academic; folklore where marked

### 11.3 Rainbow and Pride color restrictions

| Country | What happened | Date | Consequence | Source |
|---|---|---|---|---|
| Russia | Supreme Court declared the "international LGBT movement" extremist and the rainbow flag a forbidden symbol; first convictions were a fine for posting a flag and five days' detention for rainbow earrings | 30 Nov 2023; convictions early 2024 | Any rainbow stripe, gradient or icon reads as extremist material; up to 15 days' detention, up to four years on repeat | [HRW](https://www.hrw.org/news/2024/02/15/russia-first-convictions-under-lgbt-extremist-ruling) |
| Hungary | 2021 law bans portraying homosexuality to minors; Act III of 2025 bans assemblies breaching it; constitutional amendment 14 Apr 2025 | 2021; 2025 | Rainbow creative reachable by minors risks the 2021 law; Pride attendees fined, organizers up to one year | [Amnesty Canada](https://amnesty.ca/urgent-actions/hungary-protect-the-right-to-march-for-pride/) |
| Poland | "LGBT-free zones" from 2019, all withdrawn by Apr 2025; three activists tried and acquitted in 2021 over Black Madonna posters with a rainbow halo | 2019 to 2025 | No live legal bar on rainbow colors; a rainbow on a religious image is prosecutable | [Crux](https://cruxnow.com/church-in-europe/2021/03/polish-court-acquits-activists-who-put-lgbt-rainbow-on-icon) |
| Saudi Arabia | Commerce ministry seized rainbow-colored bows, skirts, hats and pencil cases from Riyadh shops as "promoting homosexuality" | 14 to 15 Jun 2022 | Rainbow merchandise, packaging or children's creative can be seized at retail | [Al-Monitor / AFP](https://www.al-monitor.com/originals/2022/06/saudi-seizes-rainbow-toys-homosexuality-crackdown) |
| Qatar | Stadium security seized rainbow items from fans; captains dropped the OneLove armband under FIFA sanction threat | Nov 2022 | Rainbow items confiscated at public venues even when nominally permitted | [ESPN](https://africa.espn.com/football/story/_/id/37634403/fifa-says-rainbow-items-allowed-stadiums) |
| UAE | Amazon blocked about 150 search terms including "pride" on its UAE site under threat of penalty | 2022 to 2023 | Pride-themed listings are blocked; a rainbow element is a takedown risk | [Wikipedia, last resort](https://en.wikipedia.org/wiki/LGBTQ_rights_in_the_United_Arab_Emirates) |
| Malaysia | Home ministry seized more than 160 Swatch Pride watches, then gazetted a ban on all Swatch LGBTQ items including boxes and wrappers | May 2023; ban 10 Aug 2023 | Possession: up to three years or MYR 20,000; packaging counts | [AP](https://www.click2houston.com/news/world/2023/08/10/malaysia-makes-owning-an-lgbtq-swatch-punishable-by-up-to-3-years-in-jail/) |
| Indonesia | Broadcast regulator banned content normalizing LGBTQ (2016); presidential decree names LGBTQ culture a "non-military national threat" | 2016; Oct 2025 | Rainbow-coded marketing can be read as banned promotion | [HRW, 2016](https://www.hrw.org/report/2016/08/10/these-political-games-ruin-our-lives/indonesias-lgbt-community-under-threat), [Wikipedia, last resort](https://en.wikipedia.org/wiki/LGBTQ_rights_in_Indonesia) |
| Turkey | Istanbul Pride banned every year since 2015; 2025 march banned, at least 30 detained | 29 Jun 2025 | Rainbow banners in public draw detention; a rainbow on a screen is not documented as prosecuted | [PinkNews](https://www.thepinknews.com/2025/06/30/dozens-detained-in-turkey-during-banned-istanbul-pride-march) |
| Uganda | Anti-Homosexuality Act: "promotion of homosexuality", up to 20 years | 30 May 2023 | Rainbow creative shipped into Uganda can be charged as promotion | [HRW](https://www.hrw.org/news/2023/05/30/ugandas-president-signs-repressive-anti-lgbt-law) |
| Ghana | Family Values bill passed Feb 2024 and lapsed unsigned; reintroduced and passed again May 2026 with three to five years for promoting LGBTQ activity; assent not recorded | 2024; 2026 | Treat as live: rainbow promotion would carry three to five years | [Wikipedia, last resort](https://en.wikipedia.org/wiki/LGBTQ_rights_in_Ghana) |
| Kenya | Family Protection Bill (2023) stalled in committee | 2023 | No rainbow restriction today | [Wikipedia, last resort](https://en.wikipedia.org/wiki/LGBTQ_rights_in_Kenya) |
| Nigeria | Same Sex Marriage (Prohibition) Act bars a "public show of same sex amorous relationship directly or indirectly" | Jan 2014 | Ten years for a public show, which a rainbow campaign could be argued to be | [Wikipedia, last resort](https://en.wikipedia.org/wiki/LGBTQ_rights_in_Nigeria) |
| Egypt | Rainbow flags waved at a Mashrou' Leila concert in Cairo; at least eleven arrested for "debauchery", one sentenced to six years | 22 Sep 2017 | A rainbow flag in public has led to multi-year sentences without a specific statute | [HRW](https://www.hrw.org/news/2017/09/30/egypt-stop-anti-lgbt-crackdown-intimidation) |
| Lebanon | Interior minister ordered security forces to prevent any LGBT gathering; suspended by the Shura Council 1 Nov 2022 | 2022 | No standing ban on rainbow display | [Wikipedia, last resort](https://en.wikipedia.org/wiki/LGBTQ_rights_in_Lebanon) |
| Iraq | Amendment to the 1988 anti-prostitution law: "promoting homosexuality", undefined, seven years | 27 Apr 2024 | Any rainbow creative can be prosecuted as promotion | [HRW](https://www.hrw.org/news/2024/05/20/iraq-repeal-anti-lgbt-law) |
| Georgia | "Family Values" package passed 84 to 0; restricts media and advertising promoting non-heterosexual relationships | Sep to Oct 2024 | Rainbow in advertising restricted by statute; penalties unconfirmed | [PinkNews](https://www.thepinknews.com/2024/09/18/georgia-lgbt-propaganda-law/) |
| Belarus | Bill banning "propaganda of homosexual relations" signed | 15 Apr 2026 | Rainbow creative is propaganda by statute; penalty amounts unconfirmed | [Wikipedia, last resort](https://en.wikipedia.org/wiki/LGBTQ_rights_in_Belarus) |
| Jamaica | Montego Bay mayor blocked a Pride venue | Sep 2019 | No legal restriction on rainbow display | [Wikipedia, last resort](https://en.wikipedia.org/wiki/LGBTQ_rights_in_Jamaica) |
| Haiti | 2016 Massimadi festival canceled after threats, not by order; 2017 Senate bill never became law | 2016; 2017 | No legal restriction on rainbow display | [Wikipedia, last resort](https://en.wikipedia.org/wiki/LGBTQ_rights_in_Haiti) |
| Dominican Republic | Police broke up the 2012 Santo Domingo Pride parade, citing improper use of the Dominican flag | 6 Jun 2012 | No rainbow restriction; a rainbow composed with the Dominican flag is a flag-law exposure (section 5) | [Wikipedia, last resort](https://en.wikipedia.org/wiki/LGBTQ_rights_in_the_Dominican_Republic) |

**MUST NOT ship a six-color rainbow stripe, gradient, ribbon or icon into Russia, Iraq, Uganda, Belarus, Georgia, Malaysia or Saudi Arabia.**

- Counts: progress bars, loaders, chart series and onboarding art that run red-orange-yellow-green-blue-purple in order; rainbow packaging and wrappers; a rainbow on a receipt or splash screen.
- Does not count: a multi-hue categorical palette whose hues are not in spectral order and never sit as adjacent bands.

**SHOULD avoid the rainbow stripe in Hungary, Indonesia, Nigeria, Ghana, Turkey, Qatar, UAE and Egypt.**

- Counts: Pride-themed campaigns, limited editions, app icons swapped for June.

**MUST NOT run a Pride-month theme, icon swap or campaign in any market on this register without a named owner's sign-off, and MUST keep it off surfaces reachable by minors in Hungary.**

**MUST NOT compose a rainbow with a national flag or a religious image.**

**MAY use the rainbow in Haiti, Jamaica, Kenya and Lebanon, and in Poland away from religious imagery.** No standing legal bar; social risk only, and in the United States it reads as a position to both sides (section 6).

Grade: statute and enforcement case for the MUST NOT rows; folklore where a row rests on an encyclopedia page

### 11.4 Club colors on sports, lottery and betting surfaces

Club colors are from the RSSSF club colors registry, an established reference whose pages are dated; several are old, and "W" marks a Wikipedia-only confirmation. A product with a betting, lottery or sports surface MUST NOT set a rivalry's two color sets as the two sides of a control, chart or promo in that club's market, and SHOULD avoid either set as the dominant pair of a surface there.

| Market | Rivalry | Colors | Source |
|---|---|---|---|
| Argentina, Buenos Aires | Boca Juniors and River Plate | Boca blue with a yellow band; River white with a red diagonal sash | [RSSSF Argentina, 2026](https://rsssf.org/colours/argentina.html) |
| Brazil, Rio de Janeiro | Flamengo and Fluminense | Flamengo black, red, white; Fluminense maroon, green, white | [RSSSF Brazil](https://rsssf.org/colours/brazil.html) |
| Brazil, São Paulo | Corinthians and Palmeiras | black and white; green and white | [RSSSF Brazil](https://rsssf.org/colours/brazil.html); [W](https://en.wikipedia.org/wiki/Derby_Paulista) |
| Scotland, Glasgow | Celtic and Rangers | green and white hoops; blue. Sectarian, not only sporting | [RSSSF Scotland](https://rsssf.org/colours/scotland.html); [W](https://en.wikipedia.org/wiki/Old_Firm) |
| Egypt, Cairo | Al Ahly and Zamalek | all red; white with two red bands | [RSSSF Egypt](https://rsssf.org/colours/egypt.html) |
| Turkey, Istanbul | Fenerbahçe, Galatasaray, Beşiktaş | yellow and navy; red and yellow; black and white | [RSSSF Turkey](https://rsssf.org/colours/turkey.html) |
| Spain | Real Madrid, Barcelona, Atlético | white; blue and red stripes; red and white stripes | [RSSSF Spain](https://rsssf.org/colours/spain.html) |
| Greece | Olympiacos and Panathinaikos | red and white stripes; green | [RSSSF Greece](https://rsssf.org/colours/greece.html) |
| Serbia, Belgrade | Partizan and Red Star | white with black stripes; red with white stripes | [RSSSF Serbia](https://rsssf.org/colours/serbia.html) |
| Morocco, Casablanca | Raja and Wydad | green and white; red with white edges, also read as the monarchy's colors | [RSSSF Morocco](https://rsssf.org/colours/morocco.html) |
| DRC, Kinshasa and Lubumbashi | TP Mazembe, AS Vita Club, DC Motema Pembe | Mazembe black and white stripes; Vita Club green with black edges; Motema Pembe green with white edges | [RSSSF Congo-Kinshasa](https://rsssf.org/colours/zaire.html) |
| Haiti | Racing Club Haïtien, Violette, Don Bosco; national team | Racing yellow and blue; Violette green and white (2001 listing); Don Bosco yellow and black; Les Grenadiers blue shirt with red shorts | [Haïti Tempo](https://haititempo.com/foot-d1-le-vieux-lion-pret-pour-le-combat); [RSSSF Haiti, 2001](https://rsssf.org/colours/haiti.html); [W](https://en.wikipedia.org/wiki/Haiti_national_football_team). Don Bosco "jaune et noir": unconfirmed |
| Dominican Republic | Tigres del Licey, Leones del Escogido, Águilas Cibaeñas | Licey blue; Escogido red, white, black; Águilas yellow, orange, black. Licey against Águilas is the capital against the Cibao | [W Licey](https://es.wikipedia.org/wiki/Tigres_del_Licey); [W Escogido](https://es.wikipedia.org/wiki/Leones_del_Escogido); [W Águilas](https://es.wikipedia.org/wiki/%C3%81guilas_Cibae%C3%B1as) |
| Mexico | América and Chivas | yellow with blue edges; red and white stripes | [RSSSF Mexico](https://rsssf.org/colours/mexico.html) |
| Colombia, Medellín | Atlético Nacional and Independiente Medellín | green and white stripes; red and blue | [RSSSF Colombia](https://rsssf.org/colours/colombia.html) |
| Kenya, Nairobi | Gor Mahia and AFC Leopards | green with white edges; blue and white (unconfirmed). Fan bases mainly Luo and Luhya | [RSSSF Kenya](https://rsssf.org/colours/kenya.html); [W](https://en.wikipedia.org/wiki/Mashemeji_Derby) |

- Counts: a two-option bet control in the two sets, a derby promo in one set, a jackpot tier palette that walks through one club's colors.
- Does not count: the brand palette when it happens to share one hue with one club; club crests used under licence with both clubs treated alike.
- Yellow and black is Don Bosco in Haiti and Águilas in the Dominican Republic, so a yellow-and-black jackpot look reads as a club on both sides of the island.

Grade: academic (reference registry); folklore where marked

### 11.5 Gang and cartel color codes

The evidence sits in each country entry; this table is the index the sweep reads.

| Market | Code | Rule | Entry |
|---|---|---|---|
| El Salvador, Honduras, Guatemala | the numbers 13 (MS-13) and 18 (Barrio 18) | MUST NOT feature either number | section 5 |
| United States | Bloods red, Crips blue; Chicago red and black against blue and black | Caution on solid red or royal blue in school-facing material | section 6 |
| Jamaica | JLP green, PNP orange | MUST NOT set the two as sides | section 5 |
| Brazil, Rio | all black read as militia; red and black read as Comando Vermelho | MUST NOT dress field staff in all black | section 5 |
| Haiti | none documented | No rule | section 5 |
| Trinidad and Tobago | colors exist but are not named in print | No rule | section 5 |
| Mexico | none found | No rule | none |

**MUST NOT dress field staff, agents or couriers in a color that a documented gang code claims in the area they work.** Uniform color is a safety decision, not a brand decision, in Kingston, Rio and the Northern Triangle.

Grade: reputable press; house rule

### 11.6 The pan-African and Rastafari sets

Two sets, often confused. **Red, black and green** was unveiled by Garvey's UNIA on 13 August 1920 at its New York convention: red for blood, black for the race, green for the land ([FOTW, US Afro-American flags](https://www.crwflags.com/fotw/flags/us-afro.html)). **Red, gold and green** is Ethiopia's tricolor (flown since 6 October 1897, [FOTW Ethiopia](https://www.crwflags.com/fotw/flags/et.html)), taken up by Jamaican Rastafari as the mark of Ethiopianism, passed through Garvey's London circle to Nkrumah, and adopted as Ghana's flag on 6 March 1957 with the black star from the Black Star Line ([Crampton, FIAV](https://fiav.org/wp-content/uploads/2021/04/13-12-Crampton-MarcusGarveyAndTheRastaColours.pdf), [FOTW Ghana](https://www.crwflags.com/fotw/flags/gh.html)). Guinea (1958), Senegal (1960) and Mali (1961) took the same set as vertical tricolors ([Guinea](https://www.crwflags.com/fotw/flags/gn.html), [Senegal](https://www.crwflags.com/fotw/flags/sn.html), [Mali](https://www.crwflags.com/fotw/flags/ml.html)).

**Readings by market.**

- Red-gold-green bands read as Rastafari in Jamaica and the Jamaican diaspora (US, UK, Canada); as Ethiopia with green on top, where the plain tricolor is a Proclamation 654/2009 offense (section 7); as Ghana with red on top; and as the retired 1962 flag in Rwanda, where the set is a MUST NOT.
- Red-black-green reads as Black nationalist in the US and as the UNIA; Kenya's flag adds white fimbriation and falls under the Kenya law entry.
- In Guinea, Senegal and Mali the set is national, not partisan; no source shows it as a party color there.

**MUST NOT use red, gold and green bands in the 1962 order in Rwanda or as a plain tricolor in Ethiopia (section 7), and SHOULD use them only deliberately in Jamaica, where they read as a religion.**

- Does not count: the three colors as separate state colors, or Ghana's and Senegal's own flags where their flag law allows.

Grade: academic

### 11.7 Election calendar, 2026-10-20 to 2028-10-31

Drives the window rule in section 3. Where the status is "announced", "expected" or "no date set", the date MUST be rechecked every 30 days. Haiti moved its date twice in 2026 and then withdrew it.

| Country | Next election | Status | Window for this spec | Source |
|---|---|---|---|---|
| Haiti | First round was set for 13 Dec 2026 and the runoff for 21 Feb 2027; the CEP postponed the process without a date on 6 Oct 2026 | No date set | Open now, until 30 days after a published result | [La Libre, 2026-07-28](https://www.lalibre.be/international/amerique/2026/07/28/haiti-les-autorites-annoncent-des-elections-en-fin-dannee-sous-condition-de-securite-Q5Q2RICDGBDCFLTHA224JFUHAQ/), [DH, 2026-10-06](https://www.dhnet.be/dernieres-depeches/2026/10/06/le-conseil-electoral-haitien-reporte-les-elections-R6SNCNXCF5GXFENSLH5DOCPFQY/) |
| Dominican Republic | Municipal 20 Feb 2028; presidential and congressional 21 May 2028; runoff 25 Jun 2028 | Scheduled, constitution art. 209 | 25 Jul 2027 (JCE precampaign line) to 25 Jul 2028 | [Constitute, DR 2015](https://www.constituteproject.org/constitution/Dominican_Republic_2015), [Acento, 2026-05-24](https://acento.com.do/politica/participacion-ciudadana-alerta-la-campana-del-2028-ya-empezo-aunque-la-ley-lo-prohibe-9684916.html) |
| DRC | Presidential, legislative and provincial, December 2028 per the CENI roadmap, unfunded as of 24 Sep 2026 | No date set | 1 Sep 2028 until 30 days after results | [Actualite.cd, 2025-04-04](https://actualite.cd/2025/04/04/pour-denis-kadima-la-publication-de-la-feuille-de-route-2025-2029-est-la-preuve-que), [Actualite.cd, 2026-09-25](https://actualite.cd/index.php/2026/09/25/rdc-aupres-de-muzito-la-ceni-presse-pour-le-financement-des-elections-de-2028) |
| United States | House and Senate 3 Nov 2026; presidential 7 Nov 2028 | Scheduled | 5 Aug 2026 to 3 Dec 2026; 9 Aug 2028 to 7 Dec 2028 | [ElectionGuide](https://electionguide.org/countries/id/226/), [3 U.S.C. 21](https://www.law.cornell.edu/uscode/text/3/21) |
| Canada | Fixed date 15 Oct 2029; earlier dissolution possible | Scheduled, after window | none in range | [Elections Canada](https://www.elections.ca/content.aspx?section=vot&dir=faq&document=faqelec&lang=e) |
| France | Presidential 18 Apr 2027, runoff 2 May 2027 | Scheduled | 18 Jan 2027 to 1 Jun 2027 | [Service Public](https://www.service-public.gouv.fr/particuliers/actualites/A15053?lang=fr) |
| Brazil | Presidential runoff 25 Oct 2026; next general Oct 2030 | Runoff scheduled | now to 24 Nov 2026 | [ElectionGuide](https://electionguide.org/countries/id/31/) |
| Mexico | Federal deputies 6 Jun 2027 | Scheduled | 8 Mar 2027 to 6 Jul 2027 | [INE](https://www.ine.mx/voto-y-elecciones/elecciones-2027/) |
| Colombia | Presidential held May and June 2026; next 2030 | After window | none in range | [ElectionGuide](https://electionguide.org/countries/id/48/) |
| Kenya | General 10 Aug 2027 | Scheduled, constitution art. 101 | 12 May 2027 to 9 Sep 2027 | [Constitute, Kenya 2010](https://www.constituteproject.org/constitution/Kenya_2010) |
| Nigeria | Presidential and National Assembly 16 Jan 2027 | Scheduled | 18 Oct 2026 to 15 Feb 2027 | [INEC](https://www.inecnigeria.org/), [ElectionGuide](https://electionguide.org/elections/id/5204/) |
| Ghana | Presidential and parliamentary, 7 Dec 2028 by convention | Expected | 8 Sep 2028 onward | [EC Ghana](https://ec.gov.gh/) |
| Uganda, Tanzania, Rwanda, India, Bangladesh, Pakistan, Indonesia, Thailand, Hungary, Germany, Colombia | Held 2024 to 2026; next 2029 to 2031 | After window | none in range | [ElectionGuide](https://electionguide.org/) |
| Philippines | Presidential, Senate, House and local 8 May 2028 | Scheduled by statute | 8 Feb 2028 to 7 Jun 2028 | [RA 7166 s.2](https://lawphil.net/statutes/repacts/ra1991/ra_7166_1991.html) |
| Taiwan | Presidential and legislative, Jan 2028 expected | Expected, no decree | Oct 2027 onward, confirm | [Election and Recall Act art. 35](https://law.moj.gov.tw/ENG/LawClass/LawAll.aspx?pcode=D0020053) |
| South Korea | National Assembly, Apr 2028 expected | Expected, day unconfirmed | Jan 2028 onward, confirm | [ElectionGuide](https://electionguide.org/countries/id/114/) |
| Japan | House of Councillors, Jul 2028 expected | Expected, no decree | Apr 2028 onward, confirm | [MIC](https://www.soumu.go.jp/senkyo/senkyo_s/naruhodo/naruhodo03.html) |

**MUST treat every SHOULD avoid on a party color in the country sections as MUST NOT inside that market's window, including any runoff, for marketing, splash, receipt and brand-dominant surfaces.**

- Does not count: state colors on an ordinary screen, a party's color as one chart series.

**SHOULD freeze marketing palettes and launch creative 120 days before election day,** so the window never catches receipts or packaging already in a print run.

**MUST NOT ship election-adjacent surfaces (civic reminders, "go vote" banners, results widgets) in any market without the section 4 party-mark check and this calendar's window check.**

Grade: statute (constitutions and electoral statutes); reputable press for announced dates

---

## 12. The release sweep

| Field | Content |
|---|---|
| **Rule** | Before a release ships into a market, one named person MUST run the sweep below against that market's register and record the result with the release. A sweep that finds a MUST NOT blocks the release until the surface changes. |
| **Why** | The register is only read if a step forces someone to read it. Every incident cited in this spec involved a surface that someone designed in good faith and nobody checked against the market it was going into. |
| **How to verify** | The release record names the sweeper, the register version, the date, and lists each surface checked with pass, fail or exception. |

**Step 1, collect the surfaces.** Every screen, printed receipt or ticket, chart, email, push notification, store listing, ad, deck and piece of packaging in the release. Include the dark theme of every screen as its own surface. Include the app icon and splash screen.

**Step 2, extract the palette.** From design tokens where they exist, otherwise from the built screens. Record every color that covers more than about 5 percent of a surface or forms an edge strip, ribbon, badge or series fill. Text colors on a neutral ground are out of scope here; they are covered by the WCAG specs.

**Step 3, run the pair test.** For every two colors that are both dominant on one surface, look the pair up in the market's register. Dominant means: a block or band of each, a split background, two series in one chart, a color on a color. One small element on a neutral ground is not a pair.

**Step 4, run the band test.** For every stripe, ribbon, edge strip, progress bar with segments, or stacked bar, write down the colors in order from top to bottom or left to right. Compare the sequence with every flag and party banner in the register. Two or three bands in a flag's order read as the flag with no emblem.

**Step 5, run the symbol test.** Search the release for every mark the register lists: flags, coats of arms, party logos, salutes, animals, flowers, numbers, slogans, leader images, and any emblem printed on a national flag. Check photography and illustration, not only icons. Check generated imagery twice: a generated flag with the wrong stripe count is still the flag to the law and is a defaced flag to the reader.

**Step 6, run the calendar test.** Check the market's election window and mourning periods (section 11) against the release date and the campaign's run. If the release lands inside a window, apply the window rule from section 3.

**Step 7, run the dark-theme test.** Repeat steps 3 and 4 with the dark theme's background counted as black. A red tag that passes on white becomes a red-on-black pairing on the dark card.

**Step 8, run the market data test.** If the release shows any gain, loss, rise, fall or delta, check it against the market data register in section 11. Every delta carries a sign and an arrow as well as a color.

**Step 9, run the cash test.** If the release shows a banknote, a denomination chip or a cash-count tile, check it against the market's note table (sections 5 and 7). The chip matches the current series and carries the numeral.

**Step 10, record.** One line per surface: surface, market, pass or fail, the entry that applied, and the exception reference if one was granted.

**MUST**

- Treat the dark theme as a separate surface in every step.
- Check printed material at print size; a 2 mm edge strip is still a band.
- Check vendor and partner material the product displays, such as a telco's top-up promo inside the app.
- Sweep a shared component once per market it ships into, not once overall. A denomination chip that passes in Haiti can fail in the Dominican Republic because the note art carries the flag.

**SHOULD**

- Automate steps 2 to 4 against the token file in CI using the schema in Appendix A, and keep steps 5 to 9 manual.
- Run the sweep on the staging build, not the design file, because build-time color mapping and theming can change what ships.

**MAY**

- Sample instead of sweeping every surface in a release that only changes copy, provided every changed surface is included.

---

## 13. When the register and the brand collide

| Field | Content |
|---|---|
| **Rule** | When a brand color or a product state color hits a register entry in one market, the product MUST change for that market, through a market theme, and MUST NOT ship the global palette with a note. |
| **Why** | A note in a design file does not reach the user. The Haitian red and black rule exists because a brand built on red with a dark theme ships a Duvalierist pairing to every Haitian user who turns the dark theme on, and no note fixes that. |
| **How to verify** | The market theme exists as tokens, is selected by market and not by language, and the sweep passes on it. |

**MUST**

- Key the theme on the market the user is in, not on the interface language. A French-speaking user in Kinshasa and one in Paris are in different registers.
- Keep the semantic token names stable and change only their values, so the override is one file and not a fork.
- Keep every market theme passing the WCAG specs and the color-blindness check in section 2; a market override is not an exception to either.

**SHOULD**

- Pick a replacement from the same part of the palette, so a market theme reads as the same product in different clothes.
- Record the collision in the register as a `resolved` line, with the token that changed and the date.

**MUST NOT**

- Resolve a collision by removing the state's word or icon so that only the color changes. Section 2 still applies.
- Resolve a collision by making the color less saturated. A dark red and black pairing is still red and black.
- Resolve a collision by shipping the surface only in the light theme. The user picks the theme, not the product.

---

## 14. Worked examples

**A receipt for Haiti and the Dominican Republic, one template.** A printed receipt with a brand-blue header strip, a red "payé" or "pagado" stamp, black body text on white, and a thin red strip at the foot.

- Band test: blue strip at the top, white body, red strip at the foot is the Haitian flag's order, blue over red, when the body is read as the white panel. In Haiti this is a flag reading, which no Haitian entry forbids. In the Dominican Republic a blue, white and red arrangement that resembles the flag is a Ley 210-19 risk, and the same template shipped to Santo Domingo fails the sweep.
- Fix: one strip, not two. Keep the header strip in brand blue, drop the foot strip, keep the red stamp as a single element on neutral ground. The pair test now sees red on white beside black text, which the Haiti entry explicitly allows.
- Dark theme does not apply to paper. Record the Dominican surface as pass after the change, and the Haitian one as pass unchanged.

**A two-series chart for the Dominican Republic.** Cash in and cash out plotted as two series, cash in green and cash out purple.

- Pair test: green against purple as the only two series of one chart is a pairing. Fuerza del Pueblo is green and the PLD is purple with yellow, so the chart is two party colors facing each other, which the Dominican entry lists as SHOULD avoid. From 25 July 2027 to 25 July 2028 the window rule makes it a MUST NOT on a marketing chart; an in-product chart stays SHOULD avoid.
- Fix: cash out in the brand's neutral dark, cash in in green, with the series labeled in words and the delta signed. Section 2 is satisfied by the label and the luminance gap.

**A win screen for Ghana.** A lottery product's win state with a dark background, red confetti and a red "You won" banner.

- Pair test: red on near-black is red and black. The Ghana entry makes that a MUST NOT on a win surface.
- Fix: gold or the brand's celebratory color on a dark ground, or red on white. The word "won" and an icon stay on the element.

**A denomination chip for Haiti, reused in Kinshasa.** A cash-out screen shows the notes the agent will hand over, one chip per denomination, colored like the note.

- Cash test: the Haitian table gives 10 G and 1000 G as both purple, so the chip carries the numeral and the word; the chip art does not copy the note face, because four of the notes carry the flag and the component also ships to Santo Domingo. In Kinshasa the same component takes the BCC colors, and the 1,000 FC chip is green while the 5,000 FC chip is orange; a chip that keeps the Haitian green for 500 would mislead a Congolese user who does not read the numeral.

**A betting slip for Kinshasa.** A two-option control for a derby, option A in green and option B in black and white stripes.

- Pair test and symbol test: green against black-and-white stripes is Vita Club or Motema Pembe against Mazembe, Kinshasa against Lubumbashi. The DRC entry makes that a MUST NOT on a betting surface.
- Fix: both options in the brand's neutral with the club names in words and the club crests only where the rights allow; the selected state carries a check mark, not a color.

**A solidarity post for the diaspora.** A marketing team wants a "we stand with Haiti" graphic in blue and red bands for the Dominican, US and Canadian app stores.

- Band test: blue over red is the Haitian flag. In the Dominican store that is a Ley 210-19 surface and, beside any Dominican symbol, the combination the pizzeria owner was held for. In the US and Canadian stores it is permitted.
- Fix: one graphic per store. The Dominican store gets the message in words on the brand palette with no bands.

---

## 15. Conformance checklist

- [ ] Every market in the release has a dated color register with an owner and a `reviewed` date within 12 months.
- [ ] Every register entry has a source or is labeled unconfirmed, a rule level, and an evidence grade; every MUST NOT is graded statute or enforcement case or marked a house rule.
- [ ] A named person ran the release sweep (section 12) and the record lists every surface with pass, fail or exception.
- [ ] No surface shipped into Haiti pairs red and black, in light or dark theme.
- [ ] No surface shipped into Nicaragua pairs red and black; none shipped into Ghana pairs them on a win or promotional surface.
- [ ] Every colored state carries a word, icon, or sign on the same element.
- [ ] Every state color pair passes a deuteranopia, protanopia, and grayscale check on the built screen.
- [ ] No surface shipped into the Dominican Republic uses the flag, the coat of arms, or a flag-like red, blue and white arrangement.
- [ ] No surface combines Dominican and Haitian national colors or symbols.
- [ ] No surface in any market carries a party mark, an election symbol, or a leader's image.
- [ ] No surface in any market carries a retired regime's flag, a national flag on a disposable, or religious text on a disposable.
- [ ] No release lands inside an election window with a party color as the dominant color of marketing, splash or receipt surfaces; Haiti's window is treated as open.
- [ ] Market data uses that market's up and down colors, with a sign and an arrow on every delta.
- [ ] Every denomination chip or banknote graphic matches the central bank's current series and carries the numeral.
- [ ] No living person's name renders in red in China or Korea; Japan is a Caution.
- [ ] No lottery, betting or sports surface sets two rival club color sets against each other in that club's market.
- [ ] No rainbow stripe ships into a market in the rainbow register without a signed exception.
- [ ] No skull in a straw hat on any surface shipped into Indonesia, and none elsewhere without a signed exception.
- [ ] Every market theme passes the WCAG specs and the section 2 check as well as the register.

---

## Appendix A: machine-readable register

A register MAY be kept as JSON so that steps 2 to 4 of the sweep run in CI. The schema has one object per entry and mirrors the entry format in section 3.

```json
{
  "market": "DO",
  "reviewed": "2026-10-20",
  "owner": "design",
  "entries": [
    {
      "id": "do-flag-arrangement",
      "level": "MUST_NOT",
      "kind": "band_order",
      "colors": [["blue", "white", "red"], ["red", "white", "blue"]],
      "surfaces": ["all"],
      "window": null,
      "grade": "statute",
      "source": "https://mirex.gob.do/pdf/dcep/ley_no.210-19_de_los_simbolos_patrios_dominicanos.pdf",
      "counts": "flag motif on a receipt, splash, promo or packaging; quartered red and blue with a white cross",
      "does_not_count": "red and blue used separately",
      "next_check": "2027-10-20",
      "retired": null
    },
    {
      "id": "do-pld-purple-yellow",
      "level": "SHOULD_AVOID",
      "kind": "pair",
      "colors": [["purple", "yellow"]],
      "surfaces": ["marketing", "splash", "receipt"],
      "window": {"opens": "2027-07-25", "closes": "2028-07-25"},
      "grade": "reputable_press",
      "source": "https://www.lonyfernandez.com/post/uso-de-los-colores-en-la-pol%C3%ADtica-dominicana",
      "counts": "purple with a yellow star or yellow accent as the dominant pair",
      "does_not_count": "purple as one series among several",
      "next_check": "2027-07-25",
      "retired": null
    },
    {
      "id": "ht-red-black",
      "level": "MUST_NOT",
      "kind": "pair",
      "colors": [["red", "black"]],
      "surfaces": ["all"],
      "window": null,
      "grade": "reputable_press",
      "house_rule": true,
      "source": "https://www.crwflags.com/fotw/flags/ht.html",
      "counts": "a red tag on a near-black dark-theme card",
      "does_not_count": "red error text on white beside black body copy",
      "next_check": "2027-10-20",
      "retired": null
    }
  ]
}
```

**Fields.**

| Field | Values | Notes |
|---|---|---|
| `level` | `MUST_NOT`, `SHOULD_AVOID`, `CAUTION`, `NO_RULE` | Mirrors the rule levels in section 3 |
| `kind` | `color`, `pair`, `band_order`, `symbol`, `name_color`, `market_data`, `banknote` | `band_order` compares ordered sequences; `pair` compares unordered sets |
| `colors` | Named hues, not hex | A checker maps the token's hex to a hue band; the register stays readable |
| `surfaces` | `all`, `marketing`, `splash`, `receipt`, `chart`, `win`, `betting`, `packaging`, `icon`, `uniform` | The sweep's step 1 inventory uses the same names |
| `window` | null, or `opens` and `closes` dates | When set, a `SHOULD_AVOID` is enforced as `MUST_NOT` inside the window; `closes: null` means open until further notice |
| `grade` | `statute`, `enforcement_case`, `reputable_press`, `academic`, `folklore` | A `MUST_NOT` with a grade below `enforcement_case` fails register validation unless `house_rule` is true |
| `house_rule` | boolean | True for any `MUST_NOT` graded below `enforcement_case`, such as Haiti's red and black; it still needs a reputable press or academic source |

**Hue bands for the checker.** A token counts as a named hue when its hue angle in HSL falls in the band and its saturation is above 25 percent; below that it is `neutral`. Black is lightness under 15 percent, white is lightness over 92 percent, regardless of hue.

| Hue | Degrees |
|---|---|
| red | 345 to 15 |
| orange | 15 to 45 |
| yellow | 45 to 70 |
| green | 70 to 170 |
| cyan | 170 to 200 |
| blue | 200 to 260 |
| purple | 260 to 300 |
| pink | 300 to 345 |

Maroon and guinda are `red` with lightness under 35 percent. Saffron is `orange`. Gold is `yellow` with saturation over 60 percent. Gray is `neutral` and only matters in the Rwanda entry, which a checker flags by lightness between 40 and 70 percent with saturation under 10 percent. The bands are a checker's approximation; the human sweep decides the edge cases.
