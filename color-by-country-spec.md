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
| **Rule** | Each market the product ships into MUST have a dated color register (§3 and the country sections). Where the register and the product's own color semantics disagree, the register wins and the product semantics change. |
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

- Prefer a non-green hue for positive states when the market register (§3 and the country sections) does not require green.

---

## 3. The market register

| Field | Content |
|---|---|
| **Rule** | Each register entry MUST name the color or pairing, what is ruled out, why, and a source. An entry with no source MUST be labeled unconfirmed and still be followed until research confirms or removes it. |
| **Why** | Folklore about color spreads fast and is hard to retire. Labeling it keeps the team honest about what is known, without shipping the risk while it is checked. |
| **How to verify** | Every entry has a source link or the label "unconfirmed". |

**What counts as a pairing:** two colors as the dominant colors of one composition. A color on the other, a stripe or split of the two, a two-series chart in the pair, a logo or brand built on it. A small colored element on a neutral surface beside body text is not a pairing. In a dark theme, the near-black background counts as black. A band pattern counts too: two or three colors set as stripes in a flag's order read as that flag with no emblem, so check stripes, ribbons and edge strips, not only pairs.

---

## 4. Every market

**MUST NOT use a party's logo, symbol, acronym, slogan or leader's image, in any market.** Every country below where party colors matter has them overlapping the national palette, so the colors alone cannot be ruled out, but the marks can, and they turn an ordinary palette into a political statement ([JCE warning on party colors and symbology, Diario Libre](https://www.diariolibre.com/politica/partidos/2025/12/01/jce-intima-a-la-fuerza-del-pueblo-por-propaganda-anticipada/3363880)).

- Counts: logos, flags, mascots, numbers on a ballot, rally photography.
- Does not count: a single color the party also uses.

**MUST NOT put a national flag or coat of arms on a commercial surface without checking that market's law.** Flag laws in the Dominican Republic, Mexico, Brazil, China, India, Bangladesh, Kenya, Nigeria and Saudi Arabia restrict commercial use, and most laws restrict flags and emblems, not colors ([Ley 210-19](https://mirex.gob.do/pdf/dcep/ley_no.210-19_de_los_simbolos_patrios_dominicanos.pdf), [LEBHN](https://www.diputados.gob.mx/LeyesBiblio/pdf/LEBHN.pdf), [Lei 5.700](https://www.planalto.gov.br/ccivil_03/leis/l5700.htm)).

- Counts: the flag, a partial flag, the coat of arms, bands in the flag's order.
- Does not count: the flag's colors used separately.

**MUST NOT print religious text (the shahada, Quranic verses, "Allah") on anything that is discarded.** Brands have withdrawn bottle caps and bunting printed with the Saudi flag because it carries the shahada ([The New Arab](https://www.newarab.com/news/riyadh-condemns-world-cup-saudi-beer-after-backlash)).

- Counts: receipts, packaging, disposables, flags of any country that carry the shahada.

---

## 5. Caribbean and Latin America

### Dominican Republic

**MUST NOT use the flag, the coat of arms, or red, blue and white arranged to resemble the flag.** Ley 210-19 makes it a punishable irreverence to use the flag in whole or in part in commercial promotion, to use its colors so that together they resemble the flag in commercial or political advertising, or to use the coat of arms in for-profit promotion, with 15 to 30 days in prison plus a fine, and any person may file a complaint ([Ley 210-19, arts. 24.5, 24.6, 28.3, 38](https://mirex.gob.do/pdf/dcep/ley_no.210-19_de_los_simbolos_patrios_dominicanos.pdf)).

- Counts: a flag motif on a receipt, splash screen, promo or packaging; quartered red and blue blocks with a white cross; the coat of arms.
- Does not count: red and blue used separately, such as a red error tag on a blue-branded screen.

**MUST NOT combine Dominican and Haitian national colors or symbols in one composition.** In 2019 a Santo Domingo pizzeria owner was held for a month and his boxes and stickers seized for a sign that put Dominican symbols with Haitian flag colors ([El Nuevo Diario](https://elnuevodiario.com.do/dictan-prision-preventiva-contra-hombre-usaba-simbolos-patrios-en-letrero-de-su-negocio/)).

- Counts: any surface shown in the Dominican Republic that carries both countries' flags or national color sets.
- Does not count: separate Haitian surfaces shipped only in Haiti.

**SHOULD avoid one party's color as the dominant color of a brand or campaign, most of all in the run-up to an election.** Party colors are an everyday political code (PLD purple with a yellow star, Fuerza del Pueblo green with a cayena flower, PRM blue and white, PRSC red, PRD white), and the electoral board treats a party's colors as evidence of campaigning ([Lony Fernández](https://www.lonyfernandez.com/post/uso-de-los-colores-en-la-pol%C3%ADtica-dominicana), [Diario Libre](https://www.diariolibre.com/politica/partidos/2025/12/01/jce-intima-a-la-fuerza-del-pueblo-por-propaganda-anticipada/3363880)). No law binds a business, and no brand has been penalized; the risk is being read as partisan.

- Counts: purple with yellow, dark green with a flower motif, either as the dominant pair of a composition.
- Does not count: green for cash coming in, purple as one chart series, red, blue or white as ordinary UI colors.

### Haiti

**MUST NOT pair red and black.** François Duvalier changed the flag's blue to black in 1964, and the black and red flag stood for the dictatorship until the blue and red flag returned in 1986 ([Britannica](https://www.britannica.com/topic/flag-of-Haiti), [Flag of Haiti](https://en.wikipedia.org/wiki/Flag_of_Haiti)). The Duvalierist PUN still uses black, red and white ([Wikipedia](https://en.wikipedia.org/wiki/National_Unity_Party_(Haiti))). No Haitian law applies; this is a house rule.

- Red error text on a white surface beside black body copy is not the pairing.
- A red tag on a near-black dark-theme card is.

**Green carries no cultural restriction.** No reputable source records a Haitian dislike of green. The one political link is the green of the Inite campaign in the disputed 2010 election ([Laurent Dubois, Soccer Politics](https://soccerpolitics.org/2010/11/28/yellow-and-green-in-haiti-a-footnote-to-the-election-crisis/)). Green as a state color stays limited by §2, for color blindness, not culture.

**Caution: green and yellow, or green and white, as the dominant pair of civic or campaign-style material.** Unconfirmed as a live reading: it echoes the 2010 Inite campaign ([Dubois](https://soccerpolitics.org/2010/11/28/yellow-and-green-in-haiti-a-footnote-to-the-election-crisis/)).

**Caution: pink as the dominant color in civic contexts.** Pink was Martelly's campaign color ([Dubois](https://soccerpolitics.org/2010/11/28/yellow-and-green-in-haiti-a-footnote-to-the-election-crisis/)).

**Caution: compositions that copy Vodou drapo.** A lwa is identified by color plus motif, such as pink with a checkered heart for Ezili ([Tampa Museum of Art](https://tampamuseum.org/sequin-arts-the-flagmakers-of-haiti/)).

- Counts: sequin-flag look, vèvè motifs with their lwa's color.
- Does not count: the colors used plainly.

**Red reads as error or warning,** never as a reward or a win.

### Brazil

**MUST NOT put the flag on product labels or packaging.** Lei 5.700 art. 31 IV lists it as disrespect to the flag, punished by fine ([Planalto](https://www.planalto.gov.br/ccivil_03/leis/l5700.htm)).

**SHOULD avoid green and yellow as the dominant styling of civic material.** The green and yellow football shirt was claimed by bolsonaristas, many Brazilians avoid it for that reason, and red is the left's counter-color ([AFP, 2026-06-24](https://citizen.digital/article/red-or-green-for-brazil-the-politics-of-world-cup-kits-matter)).

- Counts: CBF-shirt look, flag-styled promos.
- Does not count: a green success state, a yellow warning state.

### Mexico

**MUST NOT use the flag or coat of arms to promote a product or service.** The law bars using the flag to promote "imagen, bienes o servicios" and requires authorization for the coat of arms, with fines up to 10,000 UMA plus daily fines ([LEBHN, arts. 6, 32 Bis, 56](https://www.diputados.gob.mx/LeyesBiblio/pdf/LEBHN.pdf)).

- Does not count: green, white and red as separate UI colors.

**Caution: guinda (maroon) or pink as the dominant color of civic messaging.** Guinda is Morena's color and the INE investigated it on election walls; pink was the 2024 opposition's ([Excélsior](https://www.excelsior.com.mx/nacional/ine-indagatoria-bardas-guindas-morena-rechaza/1713154), [Expansión](https://politica.expansion.mx/elecciones/2024/05/16/morena-exige-que-ine-deje-de-usar-color-rosa-apropiado-por-campana-de-xochitl)).

### Venezuela

**SHOULD avoid saturated red as the dominant color of civic material.** "Rojo rojito" is the color of chavismo and the PSUV, though the government's own campaigns have softened it since 2006 ([VOA](https://www.vozdeamerica.com/a/la-campaña-de-nicolas-maduro-se-aleja-del-rojo-copia-a-la-oposicion-y-ofrece-mejorias-venezuela-/7654676.html)).

- Does not count: red error states.

### Colombia

**Caution: red and blue set against each other as two sides.** They are the Liberal and Conservative colors, fought over in La Violencia ([El Universal](https://www.eluniversal.com.co/politica/los-colores-poderosos-aliados-para-ganar-la-presidencia-de-colombia-GA5929901)).

- Does not count: red or blue used alone.

---

## 6. Sub-Saharan Africa

### Democratic Republic of the Congo

**MUST NOT use party marks or political figures.** The ruling UDPS uses red, yellow and blue and the opposition PPRD uses yellow and blue, both from the national flag, and the conflict between them is live: the PPRD headquarters in Kinshasa was set on fire during a UDPS march on 4 May 2026 ([Radio Okapi](https://www.radiookapi.net/2026/05/05/actualite/politique/le-siege-du-pprd-incendie-lors-dune-marche-de-ludps-kinshasa), [fr.wikipedia UDPS](https://fr.wikipedia.org/wiki/Union_pour_la_d%C3%A9mocratie_et_le_progr%C3%A8s_social)).

- Counts: party logos, acronyms, leaders' portraits, yellow and blue composed to echo the PPRD logo, AFC/M23 marks.
- Does not count: the national palette in neutral use.

**MUST NOT use the Zaire flag or its torch emblem.** The light green flag with a yellow disc and an arm holding a red torch was Mobutu's from 1971 until 17 May 1997 and reads as a political statement ([Britannica](https://britannica.com/EBchecked/topic/1355145)).

- Counts: the torch-and-arm emblem; a green field with a centered yellow disc (SHOULD avoid).
- Does not count: green as a state color.

**Caution: crowds dressed in white in marketing photography.** UDPS militants march in white. Unconfirmed: reported from a search excerpt ([Actualite.cd](https://actualite.cd/2026/09/22/kinshasa-ludps-et-ses-allies-marchent-sans-coup-ferir)).

**Caution: black-dominant layouts with condolence cues.** Black is generally the mourning color in francophone Central Africa ([Mount Royal University](https://mrujs.mtroyal.ca/index.php/cf/article/download/746/598)).

- Does not count: black text.
- No rule: "red means blood in the DRC" has no source.

### Rwanda

**MUST NOT use the 1962 red, yellow and green vertical tricolor.** It was retired in 2001 because of its association with the 1994 genocide and the regime behind it ([Britannica](https://www.britannica.com/topic/flag-of-Rwanda)).

- Counts: that tricolor in that order, any "R" device on it, retro "old Rwanda" graphics.
- Does not count: red, yellow and green as separate state colors, or the pan-African palette in other markets.

**SHOULD avoid gray or purple remembrance styling in commercial material around Kwibuka, from 7 April.** Gray is the official commemoration color, and Law 59/2018 punishes visual acts that trivialize the genocide with 5 to 7 years ([The New Times](https://www.newtimes.co.rw/article/90517/National/genocide-memorial-change-in-colour-for-mourning), [Law 59/2018](https://www.minijust.gov.rw/fileadmin/user_upload/Minijust/Publications/Laws/Law.Crime_of_Genocide_Ideology_2018.pdf)).

- Counts: gray ribbons, gray "we remember" campaigns.
- Does not count: neutral gray UI.

### Ghana

**SHOULD avoid red and black as the two dominant colors; MUST NOT on celebratory, promotional or win surfaces.** In southern Ghana funeral dress and decoration are red and black ([Calvin University](https://sites.calvin.edu/mkh2/ghza2016/red), [Cooper Hewitt](https://www.cooperhewitt.org/2018/09/07/adinkra-message-and-medium/)).

- Counts: red and black color blocks, brick red with black on promos, receipts or win screens.
- Does not count: black text on white with a red error state.

### Kenya

**MUST NOT use the flag, emblems, or their colors and adaptations in branding without written permission.** The National Flag, Emblems and Names Act covers commercial use, with a fine or up to six months ([Kenya Law](https://new.kenyalaw.org/akn/ke/act/1963/44)).

- Counts: the flag, black-red-green-white bands with the shield.
- Does not count: one of those colors alone.

**SHOULD avoid ODM orange or UDA yellow as the dominant brand color in campaign periods.** Color is the first marker of party in Kenya ([Nation](https://nation.africa/kenya/news/politics-influencing-fashion-trends-as-campaigns-hot-up-3761908), [Africa Check](https://africacheck.org/fact-checks/meta-programme-fact-checks/no-evidence-kenyan-news-anchors-yellow-outfits-indicate)).

- Does not count: orange as a warning accent.

### Nigeria

**MUST NOT use the flag or coat of arms without a license.** Unauthorized use in connection with any body is an offense under the Flags and Coat of Arms Act ([PLAC](https://www.placng.org/lawsofnigeria/print.php?sn=188)).

- Does not count: green and white as plain UI colors.

---

## 7. Europe

### Russia

**MUST NOT pair blue and yellow, or use white-blue-white bands or rainbow stripes.** Courts have fined and detained people for dyed hair, bracelets, fences and earrings in these colors, with no flag present ([RFE/RL](https://www.rferl.org/a/netyosov-fined--hair-dyed-ukrainian-national-flag/32955201.html), [OVD-Info](https://ovd.info/en/express-news/2026/09/22/student-justice-ministry-academy-has-been-fined-wearing-blue-and-yellow), [HRW](https://www.hrw.org/news/2024/02/15/russia-first-convictions-under-lgbt-extremist-ruling)).

- Counts: two-band layouts, ribbons, prominent paired blocks, rainbow bands or gradients.
- Does not count: blue and yellow far apart in a multi-hue palette. Unconfirmed threshold; enforcement is arbitrary.

### Belarus

**MUST NOT use white-red-white bands or pair blue and yellow; SHOULD avoid red and white as the dominant pair.** Prosecutions have reached red-white bracelets, curtains and food, and yellow-blue flowers and balloons, with arrests of 7 to 15 days and criminal terms up to 1.5 years ([PEN Belarus](https://penbelarus.org/en/2023/06/27/persecution-for-symbols-belarus-2022.html)).

### Ukraine, Lithuania, Latvia, Estonia and Moldova

**MUST NOT use orange and black stripes or a military Z or V.** The St George ribbon and Z and V are banned by statute, and the European Court of Human Rights upheld Ukraine's ban ([European Pravda](https://www.eurointegration.com.ua/eng/news/2024/12/12/7200529/), [ERR](https://news.err.ee/1609929956/over-1-000-violations-of-banned-symbols-law-logged-in-4-years)). Russia promotes the same ribbon as official, so it reads as pro-war everywhere else.

- Does not count: orange and black used apart, a Z or V in ordinary text.

### Germany and Austria

**SHOULD avoid black, white and red as three horizontal bands; MUST NOT combine them with an Iron Cross, eagle or war ensign.** The Imperial flags are the far right's stand-in for the banned swastika flag, and several German states confiscate them ([Jüdische Allgemeine](https://www.juedische-allgemeine.de/politik/schwarz-weiss-rot-legal/)).

- Does not count: black text, white ground and a red accent.

**MUST NOT use a red and white checkerboard that starts with a white field (Austria, Croatia).** It is the Ustasha arms, banned in Austria since 2019 ([Balkan Insight](https://balkaninsight.com/2019/02/13/austria-bans-two-croatian-ustasa-symbols/bi/)).

- Does not count: Croatia's current checkerboard, which starts with red.

### Hungary

**SHOULD avoid red and white horizontal multi-stripes.** The Árpád stripes were the Arrow Cross banner in 1944 and Jobbik's flag from 2006 ([JTA](https://www.jta.org/2006/10/31/lifestyle/nazi-linked-flag-surfaces-in-hungary)).

### Spain

**MUST NOT use Francoist flag elements.** The Democratic Memory Law fines exaltation of Francoist symbols from EUR 200 to EUR 150,000 ([Democratic Memory Law](https://en.wikipedia.org/wiki/Democratic_Memory_Law)).

- Counts: the eagle of Saint John, the yoke and arrows.
- Does not count: red and yellow, or the current flag.

### United Kingdom (Northern Ireland)

**SHOULD avoid green-white-orange or red-white-blue as alternating stripes or blocks.** These are sectarian territorial markers painted on kerbs ([CAIN, Ulster University](https://cain.ulster.ac.uk/images/symbols/unionloyal.htm), [Irish News](https://www.irishnews.com/news/northernirelandnews/2018/08/09/news/why-are-kerbs-painted-green-white-and-orange-a-hate-crime--1403237/)).

- Counts: flag-like bands, alternating edge strips on a receipt, bunting patterns.
- Does not count: green or orange used apart.

**Caution: green and orange as two opposed sides in a chart or two-option control.**

---

## 8. South Asia and the Middle East

### India

**MUST NOT use the tricolor, the Ashoka Chakra or the State Emblem in commerce without central government permission.** The Emblems and Names Act 1950 and the Flag Code 2002 restrict commercial use ([iPleaders](https://blog.ipleaders.in/indian-national-flag-laws-and-case-laws/)).

- Does not count: saffron, white and green used apart.

**SHOULD avoid saffron and green as two opposed sides; caution with saffron as a "national" brand color.** Saffron reads as patriotic to some and as BJP-aligned to others, as the 2026 row over the hockey kit showed ([Onmanorama](https://www.onmanorama.com/sports/other-sports/2026/07/31/blue-for-india-is-like-yellow-for-brazil-criticism-mounts-against-saffronisation-of-hockey.amp.html)).

**Caution: white as the dominant color of festive or wedding creative.** White is the color of widowhood in Hindu tradition ([Narratively](https://narratively.com/how-widows-vrindavan-got-their-color-back)).

### Bangladesh

**MUST NOT use the flag in a trademark, design or for trade without written permission** ([Bangladesh Flag Rules 1972](https://en.wikipedia.org/wiki/Flag_of_Bangladesh)).

**SHOULD avoid Awami League imagery, including black mourning styling around 15 August.** The party has been banned since May 2025 ([PTI via The Week](https://www.theweek.in/wire-updates/international/2025/05/12/fgn52-bangla-awami-ban.html)).

### Sri Lanka

**MUST NOT put the lion flag or the Buddhist flag on low-dignity items.** The government has asked retailers to remove such products and ordered action against disrespect of the Buddhist flag ([Daily FT](https://www.ft.lk/News/Sri-Lanka-asks-Amazon-to-remove-bikinis-and-doormats-featuring-its-flag/56-714755), [Tamil Guardian](https://www.tamilguardian.com/node/22748)).

- Counts: apparel, doormats, swimwear, the Buddhist flag's color stripe as decoration.

### Saudi Arabia

**MUST NOT use any national flag, religious symbol or sectarian symbol in commercial material, and MUST NOT print the Saudi flag on any product anywhere.** A 2024 commerce ministry rule bans them from products and promotions, and the flag carries the shahada ([Gulf News](https://gulfnews.com/world/gulf/saudi/saudi-arabia-bans-commercial-use-of-national-religious-and-sectarian-symbols-1.1731838256178)).

- Does not count: green alone.

### Israel and Palestine

**SHOULD avoid red, green, black and white composed as the Palestinian flag or a watermelon, and blue and white composed as the Israeli flag, in neutral products.** Either reads as a political statement, and Israel has restricted the Palestinian flag ([CSM](https://csmonitor.com/World/Middle-East/2024/0117/Seeds-of-resistance-Why-watermelon-symbolizes-Palestinian-solidarity), [Times of Israel](https://www.timesofisrael.com/knesset-advances-bill-banning-palestinian-flags-on-university-campuses/)).

- Does not count: those colors as separate UI colors.

### Iran

**SHOULD avoid green as a movement or solidarity signal.** Green was the color of the 2009 opposition movement ([V&A](https://collections.vam.ac.uk/item/O1814476)).

- Does not count: green as a success state.

### Lebanon

**MUST NOT use party flags or emblems; SHOULD avoid one party's color as the dominant color of Lebanon-only campaigns.** Party flags are sectarian markers, and the 2019 protests flew only the national flag ([NUS Middle East Institute](https://mei.nus.edu.sg/wp-content/uploads/2020/12/Insight-251-Sectarianism-and-the-Failure-of-Lebanon%E2%80%99s-2019-Uprising.pdf)). Unconfirmed: which color belongs to which party.

### Egypt

**MUST NOT use the black four-finger hand on yellow (Rabaa).** Displaying it has led to detention ([VOA](https://www.voanews.com/content/egyptians-defiant-over-rabaa-symbol/1800249.html)).

- Does not count: yellow alone.

### Turkey

**MUST NOT use the gray wolf sign or the MHP's three crescents** ([Wolf salute](https://en.wikipedia.org/wiki/Wolf_salute)).

**Caution: orange as the dominant color of civic material.** Orange is the AKP's color ([Wikipedia](https://en.wikipedia.org/wiki/Justice_and_Development_Party_(Turkey))).

---

## 9. East and Southeast Asia

### China

**MUST NOT use the flag, its design or the national emblem in a trademark or ad.** The 2020 amendments, in force since 2021, ban both ([AFP via The Peninsula](https://s.thepeninsula.qa/article/17/10/2020/China-passes-amendments-outlawing-insulting-national-flag)).

- Does not count: red and yellow as colors.

**MUST show market rises in red and falls in green.** Chinese readers read red as a gain ([PLoS ONE via DOAJ](https://doaj.org/article/625ec8a2bf2744b9a91eda8112faec65)).

- Counts: tickers, P&L, gain and loss deltas.

**MUST NOT render a living person's name in red.** Names of the condemned were written in red, so a red name reads as a death wish ([USC Folklore Archives](https://folklore.usc.edu/?p=43613)).

- Does not count: red seals, red backgrounds, red text that is not a name.

**SHOULD avoid white as the dominant color of gifts, envelopes or festive packaging, and red in condolence contexts.** White is the mourning color ([Dignity Memorial](https://www.dignitymemorial.com/en-ca/memorial-services/funeral-traditions/chinese-funeral-etiquette-and-superstitions)).

- Does not count: white UI backgrounds.

**SHOULD avoid a green hat on a man in imagery or merchandise.** "Wearing a green hat" means being a cuckold ([USC Folklore Archives](https://folklore.usc.edu/green-hats-in-chinese-culture/)).

### Hong Kong

**MUST NOT use yellow and blue as a two-state legend for merchants or users.** "Yellow" and "blue" shops were the 2019 political boycott lists, and businesses dropped the labels after the National Security Law ([AP](https://www.mvariety.com/?p=43866)).

**SHOULD avoid yellow umbrellas, yellow and black protest-gear pairings, and black or candle campaigns near 4 June.** Police have arrested people for commemorating 4 June ([VOA](https://www.voanews.com/a/6603517.html)).

- Does not count: yellow or black alone.

**MUST show market rises in red and falls in green.** Unconfirmed: same convention as China, weak source.

### Taiwan

**SHOULD avoid green and blue as two opposed sides in election periods; caution otherwise.** Green is the DPP camp and blue the KMT camp ([Pan-Green Coalition](https://en.wikipedia.org/wiki/Pan-Green_Coalition)).

**MUST show market rises in red and falls in green.** Unconfirmed: secondary source.

### Japan

**MUST NOT use black and white stripes in celebratory, retail or promotional contexts.** Black and white curtains hang at funerals; red and white is the celebratory pair ([Kōhaku maku](https://en.wikipedia.org/wiki/K%C5%8Dhaku_maku)).

- Does not count: black text on white.

**SHOULD avoid a living person's name in red.** Unconfirmed: weak sources only ([USC Folklore Archives](https://folklore.usc.edu/?p=43613)).

**Pair every market delta with a sign and an arrow.** Unconfirmed: Japan's dominant up and down convention is not sourced.

### South Korea

**MUST NOT render a living person's name in red.** Names of the dead were written in red ([Korea Herald](https://www.koreaherald.com/article/3323892)).

- Does not count: red seals.

**MUST show market rises in red and falls in blue.** Secondary sources only ([Rebecca's Korean Note](https://rebeccas-korean-note.ghost.io/why-korean-stock-charts-use-red-instead-of-green/)).

### Thailand

**MUST NOT pair royal yellow with royal imagery in commercial or humorous material.** Article 112 punishes insulting the monarchy with up to 15 years per count, and satirical calendars with yellow ducks drew two years ([CNN](https://amp.cnn.com/cnn/2023/03/08/asia/rubber-duck-jail-scli-intl)).

- Does not count: yellow as a plain UI or brand color.

**SHOULD avoid red and yellow as two opposed sides.** They were the rival street movements of 2006 to 2014 ([CSM](https://csmonitor.com/World/2010/0421/Thailand-reds-shirts-yellow-shirts-duel-over-victim-compensation)).

**SHOULD avoid bright festive palettes during official royal mourning.** Mourning for Queen Sirikit began 25 October 2025, a year for civil servants; check current guidance before a launch ([TTG Asia](https://www.ttgasia.com/2025/10/27/thailand-enters-period-of-mourning-following-passing-of-queen-mother/)).

### Myanmar

**MUST NOT use red with NLD imagery or the three-finger salute inside Myanmar.** These were the 2021 anti-coup symbols, and the NLD was dissolved in 2023 ([Al Jazeera](https://www.aljazeera.com/news/2023/3/30/us-uk-japan-australia-denounce-dissolution-of-myanmars-nld)).

- Does not count: red as a plain accent.

### Vietnam

**MUST show market rises in green, falls in red, ceiling in purple, floor in cyan and reference in yellow.** Vietnamese price boards use this five-color code ([TCBS](https://help.tcbs.com.vn/en/?p=39218)).

---

## 10. Conformance checklist

- [ ] Every market in the release has a dated color register with an owner.
- [ ] Every register entry has a source or is labeled unconfirmed.
- [ ] No surface shipped into Haiti pairs red and black, in light or dark theme.
- [ ] Every colored state carries a word, icon, or sign on the same element.
- [ ] Every state color pair passes a deuteranopia, protanopia, and grayscale check.
- [ ] No surface shipped into the Dominican Republic uses the flag, the coat of arms, or a flag-like red, blue and white arrangement.
- [ ] No surface combines Dominican and Haitian national colors or symbols.
- [ ] No surface in any market carries a party mark or a leader's image.
- [ ] Market data uses that market's up and down colors, with a sign and an arrow on every delta.
- [ ] No living person's name renders in red in China, Korea or Japan.
