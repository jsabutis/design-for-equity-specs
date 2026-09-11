# Bias Audit Specification

**Conformance target:** No shipped surface encodes a representational, linguistic, or structural bias against the population it serves
**Audience:** Design, engineering, content, data science, and QA
**Scope:** UI copy, taxonomies, defaults, imagery, forms, ranking and scoring logic, moderation and abuse rules, model-generated output, and any classifier that acts on a user
**Companion docs:** `gender-bias-spec.md` (gender in depth, since it carries more product surface area than any other single axis), `disability-and-ableism-spec.md`, `ai-in-design-and-product-spec.md`, `WCAG-AA-spec.md`, `../research/field-research-synthesis-spec.md`

This document turns the bias and fairness research base into project-ready rules. Terms **MUST**, **SHOULD**, and **MAY** follow [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119).

**The core claim:** bias in a product is rarely a slur in a string file. It is an English-only abuse filter, a name field that rejects a legitimate naming convention, a default that assumes one kind of account holder, a risk score trained on who was already trusted, and a house standard written for one market and applied to every other.

**Out of scope:** Model training, fine-tuning methodology, and legal compliance regimes.

---

## 1. Purpose &amp; conventions

| Field | Content |
|---|---|
| **Rule** | Every surface MUST be audited against the axes of exclusion that are load-bearing in the market it actually serves, not against a generic diversity checklist imported from elsewhere. |
| **Why** | Systems that score well on a general fairness benchmark routinely encode a bias the benchmark never asked about. The salient axis is local and it varies: in one market it is language prestige, in another it is age or disability or rural address. A checklist written somewhere else will not name it. |
| **How to verify** | The product carries a written list of its salient exclusion axes for each market, dated and sourced to research with actual users per `../research/field-research-synthesis-spec.md`. No list, non-conformant. |

Each section below uses the same Field/Content table format and lists **MUST / SHOULD / MAY** rules.

---

## 2. Naming the axes (do this first)

| Field | Content |
|---|---|
| **Rule** | Before any audit, the team MUST enumerate the axes along which people are excluded, penalized, or made invisible in this specific market. |
| **Why** | An audit that only checks the two or three axes everyone checks will pass a product that quietly ranks by language, address, device tier, or disability status. |
| **How to verify** | The axis list exists, names at least one axis a generic checklist would have missed, and is signed off by someone with direct knowledge of the market. |

**MUST**

- Maintain an **axis register** per market, minimally covering: gender, language and dialect prestige, literacy and numeracy, disability, age, geography, income and device tier, and whatever social hierarchy is load-bearing locally.
- Name each axis in the terms locally used, not in the researcher's paraphrase.
- Derive the register from contact with actual users, not from a desk review.
- Name the **combinations** that carry the most risk, not only the axes. Harm compounds at intersections rather than adding: audits of LLM hiring evaluations have found disability raising measured harm by anywhere from 1.15x to 58x, worst where it intersects another marginalized attribute. An audit that checks one axis at a time will pass a product that fails the people standing at the crossing.

**SHOULD**

- Record for each axis the concrete mechanism by which the product could act on it (a field, a default, a score, a filter, a training corpus).
- Review the register whenever the product enters a new market or serves a new user role.
- Keep the intersection list short and specific, three to five combinations, so it gets audited rather than admired.

**MUST NOT**

- Copy an axis register between markets.
- Treat "we don't collect that attribute" as evidence of neutrality. Proxies do the work: postal code, language, device, name.

---

## 3. Language and linguistic bias

| Field | Content |
|---|---|
| **Rule** | Every language the product serves MUST receive equal functional quality, and MUST NOT be a degraded translation of the primary edition. |
| **Why** | Automated language tooling is built dominant-language-first. The models, the labels, and the training data all lean the same way, so speakers of every other supported language get worse protection and worse service out of the same product. The asymmetry shows up in every language-backed feature, not only the obvious ones. |
| **How to verify** | Run the full task suite in each supported language, on a real device, with a native speaker. Every task must complete with equal step count and no untranslated string. |

**MUST**

- Treat every supported language as a **first-class edition**: same features, same quality gate, same launch date. A feature that works only in the dominant language does not ship.
- Verify layout in every language, including the longest translation. Text-expansion breakage is a bias defect, not a cosmetic one. Widow and orphan rules apply per edition; see the project design rules.
- Ensure any filter, search, keyword rule, abuse classifier, or validation regex is authored and tested **per language**, by a speaker of that language.
- Accept local orthographic variation in input (diacritics present or absent, transliteration, code-switching) rather than rejecting it.
- Test names, addresses, and phone formats against real local data. Single-name users, multi-part surnames, and non-Latin scripts MUST validate.

**SHOULD**

- Source terminology from the project lexicon, which records the words users actually use, over a translator's formal register.
- Keep a per-language defect count and treat divergence between languages as a release blocker.

**MUST NOT**

- Machine-translate user-facing copy without native-speaker review.
- Use single-language profanity, abuse, or fraud keyword lists on multilingual content.
- Present a language as supported when only part of the surface is translated.

---

## 4. Representational bias in content and imagery

| Field | Content |
|---|---|
| **Rule** | People depicted, named, or exemplified in the product MUST reflect the actual user population, and MUST NOT map social roles onto demographic groups. |
| **Why** | Authored and generated content reliably assigns agency to some groups and passivity to others, reproducing stereotypes through ordinary examples. Product copy does the same thing through sample data, and nobody reviews sample data. |
| **How to verify** | Extract every persona, sample name, avatar, illustration, and example transaction. Tabulate role against demographic. Any correlation between role and group is a defect. |

**MUST**

- Vary demographics **across roles, not within a single stereotype**. If the sample agent is always male and the sample customer always female, that is a defect regardless of image quality.
- Use locally sourced names and imagery, checked with people from the market, never a stock set carried over from the team's own.
- Depict disability and the full age range in the ordinary case, not only on an accessibility-themed screen.
- Keep example amounts, occupations, and locations plausible for the actual user base.

**SHOULD**

- Co-design illustration and iconography with the people who will read it. See `../illustrations/scribe-illustrations-spec.md` where illustration carries meaning rather than decorating.
- Rotate sample data periodically and re-audit.

**MUST NOT**

- Use real customer names or identifying details as sample data.
- Depict the "successful" state with one demographic and the "error" or "delinquent" state with another.
- Ship untranslated placeholder content or stock avatars into an edition they were never chosen for.

---

## 5. Structural bias in logic, defaults, and scoring

| Field | Content |
|---|---|
| **Rule** | Any rule that ranks, scores, gates, flags, or penalizes a user MUST be audited for disparate impact along the axis register before it ships, and MUST be explainable to the person it acts on. |
| **Why** | This is where bias does material damage. A trust score built on past behavior encodes past exclusion; a fraud flag tuned on one usage pattern punishes every other one; a default that assumes a current-generation device excludes whoever does not have one. The bias usually surfaces not in overt language but in what the system infers and how it then treats the user. |
| **How to verify** | For each rule, compute outcome rates split by each axis in the register, and by the intersections named in §2, where data allows. Where data does not allow, state that explicitly and reason about the proxy. |

**MUST**

- Document, for every gating or scoring rule: its inputs, the proxies those inputs carry, and its intended and observed outcome distribution.
- Check defaults for embedded assumptions: account holder identity, literacy, connectivity, device capability, name shape, address shape, credit history, ID possession.
- Provide a **path for the penalized user**: any user who is flagged, downranked, or blocked MUST be able to see that it happened, in their language, and MUST have a route to a human.
- Make the **most constrained user in the audience the default path**, not the fallback. Identify that user in the axis register and design for them first. A feature usable only on new hardware and a fast connection is structurally biased against everyone else.
- Re-audit any rule whose inputs change.

**SHOULD**

- Prefer transparent rules over opaque scores where the decision affects money or livelihood.
- Set an explicit tolerance for disparate impact before measuring, so the result cannot be rationalized after the fact.
- Track who the rule never reaches, not only who it acts on.

**MUST NOT**

- Ship a score that no one on the team can explain in one sentence to the user it scores.
- Use "the model said so" as a rationale in a decision affecting a user's money, standing, or pay.
- Treat historical behavior as ground truth when the history was produced under the exclusion being audited.

---

## 6. Moderation, abuse, and safety rules

| Field | Content |
|---|---|
| **Rule** | Community, abuse, and moderation standards MUST be interpreted per market rather than applied as one global rulebook. |
| **Why** | A single uniform standard is not equality. It exports the norms of whoever wrote it and systematically mis-handles speech everywhere else. Moderation practice also legitimately differs between public and private contexts, and a rulebook that ignores that difference gets both wrong. |
| **How to verify** | Take 20 real messages from the market, half benign and half harmful in local judgment, through the rules. Every misclassification is a defect with a named cause. |

**MUST**

- Have local reviewers define what counts as harmful in each market, and record where that differs from the house default.
- Support reporting and appeal in the user's language, including by voice where a share of users will not type it.
- Log false positives by language and treat a language-skewed false-positive rate as a blocking defect.

**SHOULD**

- Allow context-appropriate rules for private and group settings rather than one policy everywhere.
- Give moderators local-language tooling of equal quality to the primary-language tooling.

**MUST NOT**

- Enforce a rule in a language whose false-positive rate has never been measured.
- Silently downrank or filter without any user-visible signal.

---

## 7. Audit cadence and evidence

| Field | Content |
|---|---|
| **Rule** | The bias audit MUST run at defined trigger points and MUST produce a dated, filed artifact with named findings and owners. |
| **Why** | One-off audits at launch miss everything introduced afterward, which is most things. |
| **How to verify** | The audit artifact exists, is dated within the cadence, and each open finding has an owner and a decision. |

**MUST**

- Run the audit at: new market, new language, new user-facing role, any new scoring or classification rule, any model or model-version change, and at minimum every 6 months.
- File findings with severity, axis, surface, evidence, and owner. Deferred findings carry an explicit accepted-risk statement from a named person.
- Include at least one reviewer from the affected market with authority to block.

**SHOULD**

- Re-run the audit against the deployed build, not the source, and capture the rendered evidence.
- Keep findings in the existing ticket system rather than a parallel doc.

**MUST NOT**

- Put audit findings, caveats, or open questions inside the design or the shipped screen. They belong in the review layer, the ticket, or this artifact.
- Close a finding on the basis of intent ("that is not what we meant"). Close on measured outcome.

---

## 8. Conformance checklist

- [ ] Dated axis register per market, naming a locally load-bearing axis (§2).
- [ ] Named intersections, three to five, carried into the audit (§2).
- [ ] Every supported language passes the full task suite, native-speaker verified (§3).
- [ ] All filters, classifiers, and validators authored per language (§3).
- [ ] Role-by-demographic table for personas, imagery, and sample data shows no role stereotyping (§4).
- [ ] Every gating or scoring rule has documented inputs, proxies, and outcome split (§5).
- [ ] Every penalized user can see it, in their language, with a route to a human (§5).
- [ ] The most constrained user in the audience is on the default path (§5).
- [ ] Moderation rules defined per market, false positives tracked by language (§6).
- [ ] Audit dated within cadence, findings owned, market reviewer had blocking authority (§7).
