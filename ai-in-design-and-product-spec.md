# AI in Design and Product Specification

**Conformance target:** AI used in the product, and in the process that builds it, does not flatten the product toward its training-data defaults or make itself unaccountable to the person its output acts on
**Audience:** Design, engineering, content, research, and anyone using an LLM to draft copy, synthesize research, or power a user-facing feature
**Scope:** LLM-generated or LLM-assisted UI copy, translations, personas, research synthesis, chat and voice assistants, explanations of automated decisions, and any model output a user reads or acts on
**Companion docs:** `../research/field-research-synthesis-spec.md`, `bias-audit-spec.md`, `gender-bias-spec.md`, `disability-and-ableism-spec.md`

This document turns the AI-and-language research base into project-ready rules. Terms **MUST**, **SHOULD**, and **MAY** follow [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119).

**Why this spec exists.** The bias and research specs govern how you learn from people and how you avoid encoding bias against them. This one governs the instrument now sitting between you and both of those: the model. It is the fastest current route by which a generic, averaged, training-distribution voice re-enters the product, because it operates upstream of every check the other specs perform. AI drafts the copy, translates the string, summarizes the interview, and then explains itself to a person whose money or standing depends on the answer. The flattening is measurable and it is invisible without a rule.

**Out of scope:** Model selection, infrastructure, cost, and evaluation harness engineering.

---

## 1. Purpose &amp; conventions

| Field | Content |
|---|---|
| **Rule** | Any AI-generated artifact that reaches a user or a decision MUST have a named human owner who reviewed it against local context, and MUST be identifiable as AI-generated in internal artifacts. |
| **Why** | Model output is fluent, plausible, and centered on its training distribution. Fluency is what makes it pass review unexamined. |
| **How to verify** | Pick any user-facing string, persona, or explanation. The team can say whether a model wrote it and who signed off. If not, non-conformant. |

Each section below uses the same Field/Content table format and lists **MUST / SHOULD / MAY** rules.

---

## 2. Homogenization is the default failure mode

| Field | Content |
|---|---|
| **Rule** | AI-assisted writing MUST NOT be shipped without a native-speaker pass that restores local voice, idiom, and framing. |
| **Why** | Writers using AI suggestions produce text measurably shifted toward the model's dominant training style, with local nuance flattened out, and this happens even when the writer keeps editorial control. The same convergence shows up in values and framing on judgment-laden topics. The effect lands on the writer, not only on the output, which is why "I wrote it myself, it just helped" is not a defense. |
| **How to verify** | Take AI-drafted copy and the shipped copy. A native speaker states what was restored. If nothing changed, the string was not reviewed, it was accepted. |

**MUST**

- Route every AI-drafted user-facing string through a native speaker of the target language who is empowered to rewrite, not only approve.
- Draft in the target language when the target language is not the model's dominant one, rather than writing in the dominant language and translating. Translation carries the source structure into every local edition.
- Use the project lexicon as authority over the model's word choice. The model does not name things.
- Preserve local idiom, register, and directness norms even where they read as blunt or unusual to the team.

**SHOULD**

- Have the local writer draft first and use AI only to tighten, rather than the reverse. Order of operations determines who is anchored to whom.
- Compare two or more independent drafts before settling, so one model's register does not become the product voice by default.
- Keep a short list of phrasings the model reliably imposes (over-politeness, hedging, "seamlessly", "empower") and grep for them before ship.

**MUST NOT**

- Ship model-generated copy in a language nobody on the team or partner team speaks.
- Use AI to generate a non-primary language edition as the only pass.
- Let AI generate personas, user quotes, or example scenarios that are then treated as evidence. Fabricated users are not users.

---

## 3. AI in research synthesis

| Field | Content |
|---|---|
| **Rule** | AI MAY assist with mechanical passes over raw research data, and MUST NOT produce the findings. |
| **Why** | Synthesis is the step where interpretation happens. A model summarizing interviews applies its own priors about what matters, and those priors come from its training distribution rather than from the market. Under `../research/field-research-synthesis-spec.md` §5, interpretation requires an analyst who knows the context and has authority to reject. |
| **How to verify** | Every theme in a readout traces to human-coded instances. Any theme whose only provenance is a model summary is struck. |

**MUST**

- Restrict AI in synthesis to: transcription assistance, first-pass search and retrieval, de-duplication, and formatting.
- Have humans perform coding, theme formation, and claim-strength labeling.
- Verify machine transcription against the audio by a fluent speaker before it is coded, in any language the model handles less well than its dominant one. Word error rates diverge sharply by language and the errors cluster on the terms that matter.
- Label AI-touched artifacts in the research corpus so a later reader knows which hop was mechanical.

**SHOULD**

- Use AI adversarially: ask it what evidence contradicts a human-formed theme, then verify the citations by hand.
- Keep raw audio as the system of record so a bad summary can always be revisited.

**MUST NOT**

- Paste raw participant data into any tool without checking the consent terms it was collected under.
- Accept an AI-generated quote, statistic, or citation without resolving it to the raw corpus.
- Let a model translate a verbatim that will be quoted in a decision document (see `../research/field-research-synthesis-spec.md` §3).

---

## 4. User-facing AI features

| Field | Content |
|---|---|
| **Rule** | An AI feature MUST be safe when it is wrong, and MUST be designed for the most constrained user in its audience rather than adapted to them later. |
| **Why** | The AI deployments that hold up in the field are the ones built around what users actually ask, in their language, on their device, with escalation to a human when the model cannot answer. The design lesson is the escalation path, not the chatbot. |
| **How to verify** | Force the feature to fail: unknown query, wrong language, no connectivity, ambiguous input. The user must end in a defined, safe, understandable state every time. |

**MUST**

- Define the **wrong-answer consequence** before building. If a wrong answer costs the user money, standing, or health, the feature requires a human escalation path, not a confidence score.
- Provide escalation to a human, reachable in the user's language and through whatever modality that user actually has.
- Support input the way people actually communicate: voice, code-switching, misspelling, partial phrases, local number and currency conventions.
- Degrade honestly offline. State that the answer is unavailable rather than serving a stale or fabricated one.
- Mark AI-generated content as AI-generated in the UI, in plain local language, without jargon.
- Never let a model's output be the final word on money owed, pay, or a user's standing. A human decision is required.

**SHOULD**

- Log unanswered and misunderstood queries and treat them as the product backlog. That loop is what separates a deployed assistant from a demo.
- Constrain the feature to a narrow, well-understood job rather than an open assistant.
- Test with the actual device tier and network conditions of the user population.

**MUST NOT**

- Ship an open-ended chat surface as the only route to a job a user must be able to finish.
- Present model confidence as a raw percentage to a user who has no way to act on it.
- Use AI output as an input to a scoring or gating rule without the audit required by `bias-audit-spec.md` §5.

---

## 5. Explainability that actually explains

| Field | Content |
|---|---|
| **Rule** | When an automated decision affects a user, the explanation MUST be built for that user's context and MUST be verified by comprehension testing, not by the presence of an explanation. |
| **Why** | Field studies of explainable-AI output repeatedly find that the people a decision acts on find standard explanations either incomprehensible or, worse, comprehensible and unconvincing. Letting people explore counterfactuals ("what if this value were different?") works where static explanations do not. Most explainability tooling assumes a technical reader, which is almost never who is on the receiving end. |
| **How to verify** | Show the explanation to five target users. Ask what the system decided and why, then ask what they would change to get a different outcome. Below 80% correct on both, non-conformant. |

**MUST**

- Explain in terms of **what the user can change**, not in terms of features and weights.
- Offer at least one **counterfactual**: the concrete change that would have produced a different outcome.
- Deliver the explanation in the user's language, in whatever modality that user can actually receive.
- Express any quantity in the explanation in a form the user can check against something they already know.
- Give the user a way to contest the decision, and route the contest to a human.

**SHOULD**

- Let the user explore, not only read: adjust an input and see the outcome change.
- Explain the system's limits as plainly as its conclusions, naming what it cannot see.
- Test explanations with the person the decision acts on, not with the supervisor who has the dashboard.

**MUST NOT**

- Show feature-importance charts, SHAP-style plots, or probability distributions to non-technical users.
- Claim explainability because a rationale string exists. Untested explanations are decoration.
- Write the explanation only in the primary language and translate later.

---

## 6. Provenance and accountability

| Field | Content |
|---|---|
| **Rule** | The product MUST record where AI acted, on whom, and under whose sign-off, and MUST re-audit when the model changes. |
| **Why** | Model versions change silently and behavior changes with them. Without a record, a regression in a less-resourced language is invisible until a user is harmed. |
| **How to verify** | The AI register exists, names each AI touchpoint, and each has an owner and a last-audited date. |

**MUST**

- Maintain an **AI register**: every touchpoint, its model and version, its consequence class, its language coverage, its human owner, and its last audit date.
- Re-run the `bias-audit-spec.md` audit on any model or version change.
- Measure quality per language, not in aggregate. Aggregate quality hides the weakest edition.
- State what data leaves the jurisdiction it was collected in, and under what terms.

**SHOULD**

- Keep a per-language regression suite of real queries and check it on each model change.
- Prefer a smaller, verifiable system over a general one where the consequence class is high.

**MUST NOT**

- Put AI provenance notes, model caveats, or audit status inside a design artifact or a shipped screen. They live in the register, the ticket, or this spec.
- Ship a model change to any language edition without testing that edition.

---

## 7. Conformance checklist

- [ ] Every AI-drafted user-facing string has a native-speaker rewrite pass (§2).
- [ ] Non-primary editions were drafted in-language, not translated from the primary one (§2).
- [ ] No AI-generated personas, quotes, or examples are treated as evidence (§2, §3).
- [ ] All research themes trace to human coding; AI limited to mechanical passes (§3).
- [ ] Machine transcription verified by a fluent speaker in every non-dominant language (§3).
- [ ] Wrong-answer consequence documented; human escalation path exists in-language (§4).
- [ ] Feature degrades honestly offline and marks AI content as AI (§4).
- [ ] Explanations pass an 80% comprehension test with target users, including a counterfactual (§5).
- [ ] Contest path routes to a human (§4, §5).
- [ ] AI register current; per-language quality measured; re-audited on model change (§6).
