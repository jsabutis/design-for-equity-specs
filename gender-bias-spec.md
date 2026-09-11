# Gender Bias Specification

**Conformance target:** No product decision, string, default, or rule disadvantages women, and no design assumes a male user, a male device owner, or a male staff member
**Audience:** Design, engineering, content, research, data science, and QA
**Scope:** UI copy and grammar, personas and sample data, onboarding and identity requirements, device and access assumptions, staff-facing tooling, safety and abuse handling, scoring and eligibility rules, and any model-generated output
**Companion docs:** `bias-audit-spec.md`, `disability-and-ableism-spec.md`, `ai-in-design-and-product-spec.md`, `../research/field-research-synthesis-spec.md`

This document turns the gender-and-technology research base into project-ready rules. Terms **MUST**, **SHOULD**, and **MAY** follow [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119).

**Why this is separate from `bias-audit-spec.md`.** That spec treats gender as one axis among several and tells you to audit for it. This one exists because gender is the axis with the most product surface area: it runs through grammar, through who owns the phone, through who is permitted to hold an account, through who is safe doing the job, and through what a model assumes when it fills in a blank. Auditing it as one row of a table is how it gets missed.

**The core claim:** the product does not need to say anything sexist to disadvantage women. It only needs to assume that the user owns the device they are holding, that the account holder is the person in front of you, that a staff member can travel alone and work late safely, and that a name field, an ID requirement, or a grammatical default is neutral.

**Out of scope:** HR policy, hiring, and internal team composition. Those matter and are governed elsewhere.

---

## 1. Purpose &amp; conventions

| Field | Content |
|---|---|
| **Rule** | Every product decision MUST be checked against a woman user and a woman staff member operating under the access, safety, and authority constraints that are real in the market being served. |
| **Why** | Designs get validated against the modal user, who is more likely to be a man with his own device, his own documents, and unconstrained mobility. A design that only works for that user excludes a large share of the customer base, and usually most of the growth. |
| **How to verify** | Walk every primary flow as a woman who borrows a device, whose ID is in a name that does not match her account, and whose movement is constrained. Every failure is a defect, not an edge case. |

Each section below uses the Field/Content table format and lists **MUST / SHOULD / MAY** rules.

---

## 2. Access: whose device is it

| Field | Content |
|---|---|
| **Rule** | The product MUST work on a shared or borrowed device without exposing the user's private data to the device owner. |
| **Why** | Device sharing is ordinary wherever hardware is expensive relative to income, and the person doing the borrowing is disproportionately a woman borrowing from a man. Any design that treats the device as equivalent to the person leaks her data, her history, and her contacts to whoever holds the handset next. |
| **How to verify** | Complete a session, hand the unlocked device to someone else, and see what they can learn. Account state, history, contact names, and notification previews must all be unreachable without re-authentication. |

**MUST**

- Never render a sensitive value, a counterparty name, or a transaction detail in a notification preview or on a lock screen.
- Require re-authentication for account state, history, and any consequential action, with a session timeout short enough for a shared device.
- Provide a fast, obvious sign-out that leaves no residue in the UI, in autofill, or in cached views.
- Support a low-spec device path wherever a meaningful share of the user base does not own current hardware.
- Support the assisted case honestly: when someone else operates the device on the user's behalf, the record MUST show who acted and on whose account.

**SHOULD**

- Offer a quick-hide or discreet mode where a user may be observed while using the product. *(verify with users in your market before assuming the need)*
- Keep the account recoverable without the device, since a woman may lose access to a device she does not own.

**MUST NOT**

- Treat device possession as proof of identity.
- Persist the last user's data in a view that loads before authentication.
- Assume a one-person-one-device model in analytics. Sessions per device is not users.

---

## 3. Authority: whose account is it

| Field | Content |
|---|---|
| **Rule** | Identity, name, and documentation requirements MUST accommodate women's real legal and social circumstances, and MUST NOT require a man's participation. |
| **Why** | Name changes at marriage, documents held by a spouse or parent, informal work histories, and lower rates of independent formal ID are ordinary and gendered. Every requirement that assumes a stable name, an independently held document, and a formal income history filters women out before the product is ever evaluated. |
| **How to verify** | List every field and document the onboarding flow requires. For each, state who is less likely to have it and why. Any requirement that fails women disproportionately needs an alternative path or an explicit accepted-risk decision with a named owner. |

**MUST**

- Accept name shapes as they actually occur: maiden and married names, multi-part surnames, apostrophes, hyphenation, single names, and non-Latin characters.
- Provide an alternative verification path where a required document is disproportionately unavailable, or record the exclusion per `../research/field-research-synthesis-spec.md` §4.
- Let a name be corrected or changed without losing account history.
- Keep the account holder's control of the account absolute in the interface. No flow may require a third party's approval that the product itself introduces.
- Support the reality that a woman may be acting on behalf of a household or a business without that erasing her own record.

**SHOULD**

- Ask for gender only where it changes what the product does. If it is collected, state why, and offer a prefer-not-to-say option that does not degrade service.
- Design the recovery flow for someone who cannot produce the original document.

**MUST NOT**

- Require a spouse's, parent's, or employer's consent, signature, or presence for a user's own account.
- Use marital status, household role, or a name mismatch as an input to a risk or trust rule.
- Infer gender from a name and act on the inference.

---

## 4. Language and grammatical default

| Field | Content |
|---|---|
| **Rule** | Copy MUST be gender-accurate in every language edition, and where a language forces a gendered form, the product MUST use the correct one rather than defaulting to masculine. |
| **Why** | Gender bias operates inside gendered grammar rather than in overt statements, which is why review in the primary language never catches it. Any edition in a language with grammatical gender inherits the problem: a masculine default addressed to a woman tells her, in every sentence, that the product was not built for her. |
| **How to verify** | Set a test account to each supported gender and read every string in every language. Any sentence that misgenders the user, or that forces a gender the product does not know, is a defect. |

**MUST**

- Write strings that do not require knowing the user's gender wherever the language allows it. Restructure the sentence rather than guessing.
- Where the language requires agreement and the product knows the user's gender, use the correct form in every edition, not only the primary one.
- Where the language requires agreement and the product does not know, use a construction that does not assume masculine.
- Apply this to every role noun in the product: administrator, reviewer, supervisor, manager, customer. If the language has a feminine form in ordinary use, ship it.
- Review the gendered forms with native speakers per language, per `bias-audit-spec.md` §3.

**SHOULD**

- Prefer role and action phrasing over personal address where agreement is contested or unsettled locally.
- Record settled gendered forms in the project lexicon so they are decided once.

**MUST NOT**

- Ship a masculine default as a placeholder to be fixed later.
- Machine-translate gendered copy without native review (`ai-in-design-and-product-spec.md` §2).
- Use gendered honorifics as a required field.

---

## 5. Representation in content and examples

| Field | Content |
|---|---|
| **Rule** | Women MUST appear across the full range of roles the product depicts, including the authoritative and technical ones, and MUST NOT be confined to the recipient or beneficiary role. |
| **Why** | Sample data is where stereotypes ship unnoticed. If every sample administrator is a man and every sample recipient is a woman, the product has stated a view about who decides and who receives, without anyone writing that sentence. |
| **How to verify** | Tabulate every persona, avatar, sample name, and example record by role against gender. Any correlation between role and gender is a defect. |

**MUST**

- Vary gender across roles: administrators, reviewers, supervisors, specialists, and customers must all include women in sample and illustrative content.
- Show women in the earning, deciding, and operating roles, not only in the receiving role.
- Keep example amounts, seniority, and occupations for women equivalent to those shown for men.
- Apply `bias-audit-spec.md` §4 alongside this: gender interacts with skin tone, age, disability, and geography, and the audit must look at the combination.

**SHOULD**

- Co-review imagery with women from the user population before shipping.
- Rotate sample data and re-audit periodically.

**MUST NOT**

- Depict the successful or trusted state with one gender and the failing or confused state with another.
- Use a woman as the default illustration for a help, tutorial, or low-competence context.
- Use real customer identities as sample data.

---

## 6. Safety and harassment

| Field | Content |
|---|---|
| **Rule** | Any surface where users can reach each other MUST be designed on the assumption that women will receive harassment there, and MUST give them controls that work before it happens. |
| **Why** | An open channel is not neutral. Studies of open voice and messaging platforms have found women receiving threats, abuse, unwanted advances, and blackmail at a volume that pushes them out of participation entirely. Without controls, the channel transfers the cost of participation onto women. Most products contain the same channel in a smaller form: messaging, callback numbers, and any in-person or scheduled contact between two users. |
| **How to verify** | For every path by which one user can contact another, state what a woman can do about unwanted contact, how fast it takes effect, and whether using it costs her anything. |

**MUST**

- Never expose a user's personal phone number, precise location, or home address to another user as a side effect of using the product.
- Provide block and report on any user-to-user channel, effective immediately, without requiring an explanation.
- Route reports to a human who reads the local language, per `bias-audit-spec.md` §6.
- Design field, visit, and on-site flows so that a woman is not required to travel alone at night, carry valuables, or meet at an unspecified location. Where the operating model requires it, that is a product finding to escalate, not a UI problem to style around. *(verify with users in your market)*
- Let a user leave or pause a channel without losing access to the core product.

**SHOULD**

- Default new user-to-user channels to closed, opening them deliberately rather than automatically.
- Log harassment reports by gender of reporter and treat a skew as a design signal, not only a moderation load.

**MUST NOT**

- Make personal contact details the default mechanism for support or dispute resolution.
- Require a woman to interact with someone she has blocked in order to complete a task.
- Treat harassment as a moderation problem only. It is an access problem.

---

## 7. Scoring, eligibility, and pay

| Field | Content |
|---|---|
| **Rule** | Any scoring, limit, commission, or eligibility rule MUST be audited for gendered disparate impact before it ships, including through proxies. |
| **Why** | Women's participation is more often shaped by interrupted availability, shared devices, and social cost, none of which are performance. A rule built on uninterrupted activity, volume, or device continuity converts those constraints into a lower score, a lower limit, or a lower payout, and calls it merit. |
| **How to verify** | Split outcome rates by gender for every scoring, limit, and payout rule. Where gender is not collected, reason explicitly about the proxies and say so. |

**MUST**

- Document, for every scoring or gating rule, which inputs are sensitive to availability, mobility, device access, or transaction size, since each carries gender.
- Audit commission, payout, and limit structures for gendered outcome differences, not only for gendered language.
- Ensure the penalized user can see the outcome and reach a human, per `ai-in-design-and-product-spec.md` §5.
- Treat interrupted or part-time activity patterns as a supported case rather than a risk signal.

**SHOULD**

- Set the tolerance for gendered disparate impact before measuring it.
- Track who the product never reaches, not only who it scores.

**MUST NOT**

- Use historical performance as ground truth where the history was produced under the exclusion being audited.
- Use device continuity, session length, or hours of availability as a trust proxy without a gender audit.

---

## 8. Research and evidence

| Field | Content |
|---|---|
| **Rule** | Research that informs a product decision MUST include women participants in proportion to the user base, interviewed under conditions where they can speak freely. |
| **Why** | A session conducted in front of a spouse, an employer, or a supervisor produces the answer that is safe to give, which compounds the response bias covered in `../research/field-research-synthesis-spec.md` §2. A study that under-samples women, or samples them under observation, produces findings that then justify a design built for men. |
| **How to verify** | Check the participant table for gender split and, per session, who else was present. Sessions with a spouse or supervisor present are marked and weighted accordingly. |

**MUST**

- Report the gender split of every study alongside raw n.
- Record who else was present in each session, and treat a session observed by a spouse, employer, or supervisor as lower confidence.
- Include a woman moderator or local woman researcher where the topic is money, autonomy, or safety. *(verify with users in your market)*
- Recruit through channels that reach women, and state which channels structurally missed them.

**SHOULD**

- Run at least one women-only session per study and compare its themes against the mixed sessions.
- Ask about device access and account control explicitly rather than inferring them.

**MUST NOT**

- Generalize a finding to all users from a sample that was mostly men.
- Recruit only through an intermediary population that skews male.

---

## 9. AI and generated output

| Field | Content |
|---|---|
| **Rule** | Any model-generated text, example, or decision that reaches a user MUST be checked for gendered assumption before it ships, in every language. |
| **Why** | Model gender bias surfaces through inference and through gendered grammar rather than through overt statements, and it is consistently worse in languages with less training data, where evaluation is thinnest. Any non-primary edition is exactly that case. |
| **How to verify** | Prompt the feature with gender-neutral inputs and inspect what it assumes: pronouns, occupations, amounts, competence, and tone. Repeat in every supported language. |

**MUST**

- Test generated output for gendered assumption per language, not in aggregate.
- Have a native speaker review generated copy for grammatical gender before ship.
- Re-run this check on any model or version change, per `ai-in-design-and-product-spec.md` §6.

**SHOULD**

- Keep a fixed set of gender-probe prompts as a regression suite.

**MUST NOT**

- Let a model infer a user's gender and act on that inference.
- Ship generated content in a gendered language without native review.

---

## 10. Conformance checklist

- [ ] Full flow completed as a woman on a borrowed device, with no leak to the device owner (§2).
- [ ] No sensitive values, names, or details in notification previews or on lock screens (§2).
- [ ] Every onboarding requirement checked for who is less likely to have it, with an alternative path or a named accepted risk (§3).
- [ ] Name fields accept maiden, married, multi-part, single, and non-Latin names; changes preserve history (§3).
- [ ] No flow requires a spouse's, parent's, or employer's participation (§3).
- [ ] Every language edition read with each gender set; no masculine default anywhere (§4).
- [ ] Role-by-gender table for personas, imagery, and sample data shows no role stereotyping (§5).
- [ ] Women appear in earning, deciding, and operating roles, not only receiving (§5).
- [ ] Block and report on every user-to-user channel, immediate, no explanation required (§6).
- [ ] No personal contact details or precise location exposed as a side effect of use (§6).
- [ ] Field and on-site flows do not require a woman to travel alone at night, or the constraint is escalated as a product finding (§6).
- [ ] Every scoring, limit, and payout rule split by gender or reasoned about via proxies (§7).
- [ ] Study participant tables report gender split and who else was present (§8).
- [ ] Generated output probed for gendered assumption in every supported language (§9).

---

## 11. References

- `bias-audit-spec.md` for the axis register method this spec deepens.
- `../research/field-research-synthesis-spec.md` for the standard every *(verify with users in your market)* item must meet.
