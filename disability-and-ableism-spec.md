# Disability and Ableism Specification

**Conformance target:** No product decision, string, image, moderation rule, or model output treats disabled people as lesser, as inspirational, or as absent
**Audience:** Design, engineering, content, data science, QA, and support
**Scope:** UI copy and imagery, personas and sample data, onboarding and identity requirements, staff-facing tooling, support and escalation, moderation and abuse handling, scoring and gating rules, and any model-generated output
**Companion docs:** `WCAG-AA-spec.md`, `bias-audit-spec.md`, `gender-bias-spec.md`, `ai-in-design-and-product-spec.md`

Terms **MUST**, **SHOULD**, and **MAY** follow [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119).

**Why this is not the WCAG spec.** WCAG governs whether a screen is *operable* by someone using assistive technology. This spec governs whether the product *treats disabled people as equals*. A screen can pass every WCAG success criterion and still infantilize the person using it, exclude them at onboarding, fail to recognize hate aimed at them, or score them lower for being slower. Those are different failures with different fixes, and conformance to one has never implied the other.

**Why it matters at this scale.** Over a billion people have a disability of some kind, and most of us acquire one if we live long enough. This is the world's largest minority group, and it is not a segment sitting outside the user base. It is inside the customer base, the staff, and the partner network right now, mostly undisclosed.

**Out of scope:** Assistive technology conformance (see `WCAG-AA-spec.md`), medical accommodation policy, and HR practice.

**Verification status:** Rules marked *(verify with users in your market)* are inferences from the research literature rather than from field research in the market being served, and MUST be confirmed before driving a shipped decision, per `../research/field-research-synthesis-spec.md` §5.

---

## 1. Purpose &amp; conventions

| Field | Content |
|---|---|
| **Rule** | Every surface MUST be designed on the assumption that disabled people are already using it, as customers and as staff, without having told anyone. |
| **Why** | Disclosure rates are low, and the incentives to disclose get worse wherever disability carries stigma or wherever someone's livelihood depends on being seen as capable. A product that only accommodates disability once it is declared accommodates almost nobody. |
| **How to verify** | For any flow, name what happens to a user who cannot see the screen, cannot hear the tone, cannot use both hands, or needs more time, and who has told you none of this. If the answer is "they would have to contact support", the flow fails. |

Each section below uses the Field/Content table format and lists **MUST / SHOULD / MAY** rules.

---

## 2. Disability is defined locally, not imported

| Field | Content |
|---|---|
| **Rule** | What counts as a disability, what counts as an accommodation, and what counts as an insult MUST be established with disabled people in the market being served, not carried over from the team's own market. |
| **Why** | Cross-cultural audits of language models found the failure running in both directions: models trained on one region's norms flagged ableism in contexts where that reading did not apply, while models trained on another under-recognized it and dismissed some conditions as not disabilities at all. Importing either norm produces a product that is confidently wrong about its own users. |
| **How to verify** | The market's disability axis entry in the `bias-audit-spec.md` §2 register names locally salient conditions and locally used terms, sourced from disabled people in that market, and is dated. |

**MUST**

- Enumerate, per market, the disabilities that are locally common and locally consequential, in the terms locally used, and record them in the axis register.
- Include disabled people from the market in the research that informs the design, per §8.
- Treat the accommodation as locally defined too. What works for a blind user in one country is not automatically what tested well in a usability lab in another.

**SHOULD**

- Record where local norms and the team's own default conflict, and decide explicitly rather than defaulting to the team's reading.

**MUST NOT**

- Assume a diagnostic category translates, or that a category absent from local vocabulary is absent from the population.
- Apply one jurisdiction's legal definition of disability as the product's operating definition everywhere.

---

## 3. Language and framing

| Field | Content |
|---|---|
| **Rule** | Copy MUST NOT patronize, infantilize, inspire, or pity, and MUST NOT use disability as a metaphor for failure. |
| **Why** | Patronization and infantilization are the most routine categories in the ableist-microaggression literature: "you are so inspirational" for doing what everyone does, or addressing the companion rather than the person. Products reproduce this through tone and through casual metaphor long before they reproduce it through policy. |
| **How to verify** | Grep the string files for ableist metaphor. Separately, have a disabled reviewer read the primary flows and mark anything that talks down. Both passes are required; the grep alone will not catch tone. |

**MUST**

- Address the account holder directly, never their assistant, family member, or representative, even when someone else is operating the device (see §5).
- Remove disability-as-defect metaphor from all copy: `crazy`, `insane`, `lame`, `dumb`, `blind spot`, `deaf to`, `crippled`, `tone-deaf`, `paralyzed`, and their equivalents in every language edition. These appear in translations as readily as in the source language, and they carry the same weight.
- Never congratulate a user for completing an ordinary task in a way that implies it was remarkable for them.
- Use the person-first or identity-first construction that disabled people in that market use, established per §2, rather than picking one from a style guide written elsewhere.

**SHOULD**

- Keep error copy factual and non-blaming. "That did not go through" beats anything implying the user failed.
- Record settled disability terminology in the project lexicon so it is decided once.

**MUST NOT**

- Use a disabled person as an inspirational illustration for a general audience.
- Frame an accommodation as a favor, a special case, or an exception granted.
- Use "normal" or "regular" to describe the non-disabled path.

---

## 4. Representation

| Field | Content |
|---|---|
| **Rule** | Disabled people MUST appear in ordinary roles in the product's imagery and examples, including as operators and decision-makers, and MUST NOT appear only in an accessibility-themed context. |
| **Why** | Generative image models could not depict disability at all until recently, and the associations they did produce framed it as dependency. That is the ambient default sample data inherits. A product whose only disabled figure appears next to a screen-reader setting has stated that disabled people are a settings category rather than users. |
| **How to verify** | Tabulate every persona, avatar, illustration, and example by role and by whether disability is depicted. Disability appearing only in accessibility contexts is a defect. |

**MUST**

- Include disabled people among administrators, reviewers, specialists, and customers in illustrative content, in the earning and operating roles, not only the receiving one.
- Depict a range of disabilities, including non-visible ones, rather than a wheelchair as the sole signifier.
- Apply `bias-audit-spec.md` §4 alongside this: disability interacts with gender, age, and skin tone, and the audit looks at the combination.

**SHOULD**

- Co-review imagery with disabled people from the user population before shipping.

**MUST NOT**

- Depict disability as dependency, as a burden on a caregiver, or as the reason a task needs help.
- Use disability imagery in a fundraising or sympathy register.

---

## 5. Access without erasure

| Field | Content |
|---|---|
| **Rule** | Where a disabled user is assisted by another person, the product MUST keep the account holder in control and visible on the record. |
| **Why** | Assisted use is common and is not itself a problem. The harm is when the product treats the helper as the user, which erases the account holder's authority over their own account and creates exactly the dependency framing the imagery rules reject. This mirrors `gender-bias-spec.md` §2, and the two failures often land on the same person. |
| **How to verify** | Run an assisted session. The record must show who acted and on whose account, the confirmation must address the account holder, and nothing about the flow may require the helper's continued involvement. |

**MUST**

- Show who performed the action and on whose account, on the confirmation and in history.
- Address confirmations and notifications to the account holder.
- Keep every function reachable without the helper, at whatever pace the user needs.
- Never impose a timeout that ends a consequential flow because the user was slow. Where a timeout is required for security, it must be extendable and must warn before it fires.
- Support audio as an equal modality, not as an accessibility fallback. The same audio path serves users who will not read the screen and users who cannot see it.

**SHOULD**

- Allow a trusted-helper arrangement to be recorded and revoked by the account holder. *(verify with users in your market)*
- Support one-handed and low-precision operation as an ordinary case: large targets, no drag-only gestures, no time-limited taps.

**MUST NOT**

- Require disclosure of a disability to unlock an accommodation.
- Route a disabled user's account decisions through a third party the product introduced.
- Make audio the only channel for anything, or make visual the only channel for anything. Every cue needs a second modality.

---

## 6. Moderation, abuse, and support

| Field | Content |
|---|---|
| **Rule** | Any channel where users or staff reach each other MUST be able to recognize and act on hate directed at disabled people, and MUST NOT reduce a disabled user's reach or service as a workaround. |
| **Why** | A large platform's documented response to hate aimed at disabled creators was to suppress those creators' content, because its classifiers could not detect the hate itself. That is the failure mode to design against: when the system cannot police the abuse, it polices the target. Compounding it, audited models are consistently more tolerant of ableist content in less-resourced languages than in the identical sentence in English, which is exactly the case for every non-primary edition. |
| **How to verify** | Take 20 real messages from the market, half benign and half ableist in local judgment, in each supported language, through the moderation and support rules. Every misclassification is a defect with a named cause. |

**MUST**

- Never reduce a user's reach, visibility, or service level as a substitute for handling abuse aimed at them.
- Measure ableist-content false negatives per language. A classifier trained on the primary language is not a classifier for any other surface (`bias-audit-spec.md` §3).
- Route reports to a human who reads the local language and who has been briefed on the local reading of ableist harm.
- Cover the harassment categories the research names, not only slurs: patronization and infantilization, privacy invasion (demands for a diagnosis or "what happened to you"), denial of disability, sexual harassment, and encouragement of self-harm.
- Support reporting by voice, since a text-only report path excludes part of the population it exists to protect.

**SHOULD**

- Track reports by reporter identity where data allows, and treat a skew as a design signal rather than a moderation load.
- Give support staff a documented path to escalate a harm they can see but cannot categorize.

**MUST NOT**

- Require a user to describe their disability in order to report abuse about it.
- Treat "the classifier did not flag it" as evidence that nothing happened.

---

## 7. Scoring, gating, and intersections

| Field | Content |
|---|---|
| **Rule** | Any scoring, limit, ranking, or gating rule MUST be audited for disability impact and for compounding at intersections before it ships. |
| **Why** | Audits of LLM hiring evaluations found that adding a disability identity to a candidate profile increased measured harm by 1.15x to 58x depending on the model, and that the harm compounded at intersections with other marginalized attributes rather than adding. Any rule built on speed, session length, volume, travel, or device continuity converts a disability into a lower score and calls it performance. |
| **How to verify** | Split outcome rates by disability where data allows, and by the highest-risk axis combinations for the market. Where disability is not collected, reason explicitly about the proxies, since speed and mobility are proxies. |

**MUST**

- Document, for every scoring or gating rule, which inputs are sensitive to speed, precision, mobility, endurance, or continuous availability. Each carries disability.
- Audit at intersections, not one axis at a time, per `bias-audit-spec.md` §2 and §5.
- Treat slower completion, more corrections, and assisted sessions as supported patterns rather than risk signals.
- Give any penalized user a visible outcome, an explanation they can act on, and a route to a human, per `ai-in-design-and-product-spec.md` §5.

**SHOULD**

- Set the tolerance for disability-linked disparate impact before measuring it.
- Track who never reaches the product at all, not only who it scores.

**MUST NOT**

- Use time-to-complete, error rate, or device continuity as a trust proxy without this audit.
- Collect a disability status in order to feed it into a risk model.

---

## 8. Research with disabled participants

| Field | Content |
|---|---|
| **Rule** | Research informing a decision that affects disabled users MUST include disabled participants, recruited and moderated in ways that do not inflate positive feedback. |
| **Why** | Response bias is a recognized and largely unaddressed problem in accessibility research specifically: participants who depend on a service, or who are grateful to be asked, report satisfaction that observation does not support. This stacks on the general response bias covered in `../research/field-research-synthesis-spec.md` §2. |
| **How to verify** | Check the participant table for disabled participants and for the de-biasing technique used in each session. Positive feedback from a session with neither is marked low-confidence. |

**MUST**

- Include disabled participants in proportion to the user base, and report that count alongside raw n.
- Use a de-biasing technique in every session, per `../research/field-research-synthesis-spec.md` §2, and weight behavior above stated preference.
- Compensate and schedule so that participation does not depend on being able to travel.
- Never let the person who provides a participant's service moderate their session.

**SHOULD**

- Recruit through disabled people's own organizations rather than through an intermediary population that skews non-disabled. *(verify with users in your market)*
- Ask about assisted use and device sharing explicitly rather than inferring them.

**MUST NOT**

- Generalize a finding to all users from a sample with no disabled participants.
- Treat a disabled participant as a representative of all disability.

---

## 9. AI and generated output

| Field | Content |
|---|---|
| **Rule** | Any model-generated text or decision reaching a user MUST be checked for ableist assumption, in every supported language, and MUST NOT be trusted to recognize ableism on its own. |
| **Why** | When models identify and explain ableism they do it differently from disabled people themselves, and disabled reviewers describe the result as cold, calculated, and condescending. Combined with the over- and under-rating findings and the gap in less-resourced languages, a model is not a competent judge of ableist harm, and it is a reliable source of ableist assumption in its own output. |
| **How to verify** | Prompt each feature with disability-neutral inputs and inspect what it assumes about capability, independence, and competence. Repeat in every supported language. Compare any ableism-detection output against a disabled reviewer's judgment. |

**MUST**

- Have a disabled reviewer, not a model, make the final call on whether content is ableist.
- Test generated output for ableist assumption per language, not in aggregate.
- Re-run this check on any model or version change, per `ai-in-design-and-product-spec.md` §6.

**SHOULD**

- Keep a fixed set of disability-probe prompts as a regression suite.

**MUST NOT**

- Deploy an automated ableism classifier as the only gate on a language whose false-negative rate has never been measured.
- Let a model infer a disability and act on the inference.

---

## 10. Conformance checklist

- [ ] Axis register names locally salient disabilities in locally used terms, dated, sourced from disabled people in that market (§2).
- [ ] No disability-as-defect metaphor in any language edition; disabled reviewer has read the primary flows for tone (§3).
- [ ] Confirmations address the account holder, never the helper (§3, §5).
- [ ] Disabled people appear in operator and decision-maker roles in imagery, not only in accessibility contexts (§4).
- [ ] Assisted sessions name who acted and on whose account; nothing requires the helper's continued involvement (§5).
- [ ] No consequential flow ends on a timeout the user cannot extend (§5).
- [ ] Every cue has a second modality; audio is an equal channel, not a fallback (§5).
- [ ] Reach or service is never reduced as a substitute for handling abuse (§6).
- [ ] Ableist-content false negatives measured per language; reports routed to a local-language human (§6).
- [ ] Every scoring and gating rule audited for disability impact and at intersections (§7).
- [ ] Speed, error rate, and device continuity are not trust proxies (§7).
- [ ] Research includes disabled participants with a de-biasing technique per session (§8).
- [ ] Generated output probed for ableist assumption in every language; a disabled reviewer makes the final ableism call (§9).
