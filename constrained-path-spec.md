# Constrained Path Specification

**Conformance target:** The most constrained user in the audience completes every core task on the shipped default path, with no separate lite edition required and no feature that exists only for them
**Audience:** Design, engineering, QA, and whoever owns the release gate
**Scope:** Payload weight, load and interaction timing, memory and storage use, data cost per task, degradation behavior, offline and interrupted states, alternate modalities and channels, and the device and network matrix used for release testing
**Companion specs:** `bias-audit-spec.md` (§2 axis register, §5 the rule this spec implements), `disability-and-ableism-spec.md` (pace, timeouts, modality), `gender-bias-spec.md` (shared and borrowed devices), `../interface/state-coverage-spec.md`, `WCAG-AA-spec.md`, `../research/field-research-synthesis-spec.md`

Terms **MUST**, **SHOULD**, and **MAY** follow [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119).

**The core claim:** the fallback never gets built. A team that designs for a good device on a good connection and plans a lightweight path "after launch" ships one path, and the constrained user gets a broken version of it. The only way the hard case works is if the hard case is the case everybody builds and tests against, with the richer experience layered on top for whoever can carry it.

**Who this is about.** Constraint is a set of conditions, not a place and not an income bracket. It covers a hospital or campus network that blocks most of the internet, a locked-down work laptop three operating-system versions behind, a metered or capped connection, a basement or a lift with one bar of signal, a five-year-old phone with a full disk, a satellite link with a two-second round trip, and a browser held at an old version by a policy the user cannot change. Any of these can belong to someone with plenty of money. Do not write the constrained user as a stereotype; write them as a measured profile.

**Out of scope:** Assistive technology conformance, which is `WCAG-AA-spec.md`. Server-side capacity and cost. Which features the product should have at all.

---

## 1. Purpose and conventions

| Field | Content |
|---|---|
| **Rule** | The build that ships MUST be the build that works under the constraint profile. A lighter alternative built later, or built as a stripped variant of the real product, does not satisfy this spec. |
| **Why** | Fallback paths are funded last, staffed thinnest, and cut first when a date slips. The observable result is a product where the primary path degrades into an unusable state under load rather than into a smaller working state, because nobody ever ran it that way. Building the constrained path first inverts the risk: the enhancement is what gets cut, and cutting it leaves a working product. |
| **How to verify** | Take the release candidate, run it on the profile device and network from §2, and complete every core task end to end. No separate build, no feature flag, no developer bypass. Any task that cannot be completed is a release blocker. |

Each section below uses the Field/Content table format and lists **MUST / SHOULD / MAY** rules.

---

## 2. Naming the constrained user

| Field | Content |
|---|---|
| **Rule** | Each market MUST have a dated, written **constraint profile** describing the device tier, network conditions, data cost, storage and battery reality, literacy and numeracy assumptions, and available modalities of the hardest case the product commits to serving. |
| **Why** | You cannot set a budget, pick a degradation order, or write a test without numbers. Teams without a profile substitute the machine on their desk, which is the fastest hardware and the best connection anyone in the audience will ever have. Every subsequent decision then inherits that assumption silently. |
| **How to verify** | The profile file exists, carries a date and an owner, and names a source for each value that is a measurement or a research finding rather than an estimate. A profile whose values cannot be traced to a source is non-conformant. |

**MUST**

- Derive the profile from the device tier, connectivity, and literacy entries in the `bias-audit-spec.md` §2 axis register for that market.
- Source every value from real evidence: telemetry from the existing user base, carrier or platform data, or field research conducted per `../research/field-research-synthesis-spec.md`. A persona workshop is not a source.
- Record the profile in a checked-in file, one per market, in a shape like this:

  ```yaml
  market: <market identifier>
  dated: <YYYY-MM-DD>
  owner: <name, role>
  covers: <share of the audience this profile is at or above, with source>
  device:
    tier: <make/model class, or minimum RAM, CPU class, screen size>
    os_version: <oldest version committed to>
    browser: <engine and version floor, and whether the user can update it>
    free_storage: <realistic free space, not device capacity>
    battery: <typical state of charge during use, and charging access>
  network:
    typical: <bandwidth down/up, latency, packet loss>
    worst_committed: <the floor the product must still work at>
    restrictions: <blocked ports, proxies, captive portals, filtered domains>
    stability: <expected drop frequency during a session>
  data_cost:
    metered: <yes/no/sometimes>
    cost_per_unit: <local currency per unit of data>
    relative: <cost of one core task as a share of typical daily discretionary spend>
  interaction:
    literacy: <reading level assumption, with source>
    numeracy: <what numeric formats are safely understood>
    language: <editions this profile applies to>
    modalities: <touch, keyboard, voice, SMS, print, assisted>
  sources:
    - <what each value came from>
  ```

- State the **share of the audience** the profile is at or above, and where that number came from. A profile covering the worst 1 percent is a different commitment from one covering the worst 30 percent.
- Re-date the profile at least every 12 months and whenever the product enters a new market.

**SHOULD**

- Keep one profile per market rather than a single global worst case, so a market is not held to a constraint nobody in it has.
- Record what the profile deliberately excludes, and who that leaves out, in the same shape `../research/field-research-synthesis-spec.md` §4 uses for exclusion by construction.
- Buy and keep the actual profile device on a shelf where the team works.

**MUST NOT**

- Describe the constrained user in terms of geography, income, or education where the real constraint is a device, a network, or an administrative policy.
- Copy a profile between markets.
- Let the profile drift upward because the old device got hard to buy. Replace the value with a measurement, not with convenience.

---

## 3. Budgets a build can fail

| Field | Content |
|---|---|
| **Rule** | The constraint profile MUST be expressed as numeric budgets for payload weight, time to first meaningful interaction, memory ceiling, and data cost per completed core task, and an automated check MUST fail the build when a budget is exceeded. |
| **Why** | Weight arrives one small addition at a time, and no single addition is ever the problem. Without an enforced ceiling the only feedback is a user complaint months later, by which point the cause is spread across a hundred commits. A check that warns but does not block gets ignored within about two sprints. |
| **How to verify** | Push a commit that deliberately adds weight past a budget. The pipeline must fail and must block the merge. If it warns, or if a human can wave it through without a recorded exception, the check is non-conformant. |

**MUST**

- Set, for each market profile, at minimum: transferred bytes for the first meaningful view, transferred bytes for a complete core task, time to first meaningful interaction measured on the profile device at the profile network, peak memory during the core task, and total data cost of the core task expressed in the profile's currency.
- Measure time to interaction as **when the user can act**, not when a load event fires or a spinner appears.
- Enforce every budget in continuous integration, on every change, as a blocking check.
- Measure on the profile device or an equivalent physical device in the pipeline, and record which one, since a budget measured on a fast machine is not a budget.
- Require a named owner and a written, dated exception for any budget raise, recorded where the next reviewer will see it.
- Count everything the user's connection actually pays for: markup, code, styles, fonts, images, media, third-party tags, analytics, and any runtime fetch.

**SHOULD**

- Budget per feature as well as per page, so the team can see which addition consumed the headroom.
- Report the trend, not only the current value, so slow growth is visible before it breaches.
- Set the data-cost budget against the profile's `relative` figure, so the number means something to the person paying it.

**MAY**

- Hold a small reserve below the ceiling for emergencies, if the reserve is explicit and not silently spent.

**MUST NOT**

- Publish an example budget as an industry standard. Numbers such as "under 200 KB for the first view" or "interactive within 5 seconds" are placeholders for the shape of the rule. Each adopting team derives its own from its own profile and replaces them.
- Exclude third-party scripts, tag managers, or analytics from the budget. The user pays for those the same way.
- Average the measurement across sessions in a way that hides the slow tail. Report a high percentile alongside the median.

---

## 4. Degradation order

| Field | Content |
|---|---|
| **Rule** | The product MUST carry a written, ordered list of what is dropped as conditions worsen, and the core task MUST be the last thing standing. |
| **Why** | Without a decided order, degradation is whatever the loading sequence happens to do, which usually means a decorative asset blocks the button. An ordered list turns an accident into a design decision and makes it reviewable. |
| **How to verify** | Throttle to each step of the order on the profile device and confirm the product sheds exactly the named layer and no more. Then confirm the core task still completes at the last step. Anything that fails out of order is a defect. |

**MUST**

- Write the order from first-dropped to last-dropped, covering at least: non-essential animation and transitions, decorative imagery, custom fonts, optional and secondary features, high-resolution or alternate media, non-critical telemetry, and finally the core task, which never drops.
- Load in that order too. The core task's markup, styles, and code MUST arrive and become usable before anything below it in the order starts transferring.
- Ship a usable state that does not depend on client-side scripting where the platform allows it, so a blocked, failed, or timed-out script does not remove the core task.
- Specify a system-font fallback stack for every custom face and render text in the fallback immediately rather than holding it invisible. Text that never appears because a font never arrived is a failure of the core task. See `../visual/design-tokens-and-theming-spec.md` for the token side of this.
- Reserve layout space for images so that shedding them does not move the controls under the user's finger.
- Treat telemetry as droppable and never let a failed or slow analytics call delay, block, or break a user action.
- Keep every control that the core task needs at the bottom of the order, including its labels, its error messages, and its confirmation.

**SHOULD**

- Trigger degradation on observed conditions, such as measured bandwidth, save-data preferences, reduced-motion preferences, or repeated timeouts, rather than only on a static device check.
- Let the user pick a lighter mode themselves, remember it, and never silently override it.
- Degrade in a way the user can see, so a missing image reads as a missing image rather than as a broken product.

**MUST NOT**

- Block first render on a font, an animation library, a consent banner script, or a third-party tag.
- Ship a spinner as the terminal state. Every wait resolves into content, a usable reduced state, or a stated failure with a next step, per `../interface/state-coverage-spec.md`.
- Degrade by hiding the core task behind a message telling the user to come back on a better connection.

---

## 5. Offline and interrupted work

| Field | Content |
|---|---|
| **Rule** | The product MUST behave honestly with no connection and with a connection that dies mid-action, and MUST NOT lose work the user already did. |
| **Why** | A connection that drops halfway through a submit is the ordinary case on the profile network, not an exception. Products that treat it as an exception either discard the user's input, or show a success state for something that never reached the server, and the second failure is worse because the user acts on it. |
| **How to verify** | Start a core task, disable the network mid-submit, and observe. The input must survive, the state shown must say what actually happened, and on reconnect the action must either complete once or be clearly abandoned. Repeat with the connection restored after several minutes and after several days. |

**MUST**

- Preserve user input locally the moment it is entered, so that a drop, a crash, a backgrounded app, or a low-memory kill does not discard it. See `../interface/forms-and-data-entry-spec.md`.
- Show the true state of every action: not started, queued locally, sent, confirmed by the server, or failed. A queued action MUST be labeled as queued, in plain language.
- Make queued actions visible, listable, and cancellable by the user before they send.
- Use idempotency on any action with a consequence, so a retry after an ambiguous failure does not create a duplicate.
- Timestamp cached data and label it with when it was last updated wherever the value could have changed since.
- Define, per data type, how stale is too stale, and stop presenting the value as current past that point.
- Define conflict resolution in advance for each syncing data type, and where the resolution is not obviously safe, show the user both versions and let them choose rather than picking silently.
- Handle the interrupted-then-resumed session across a restart, an update, and a device that ran out of storage while the queue was pending.

**SHOULD**

- Let the user complete and queue a core task fully offline where the task does not need a live server response to be meaningful.
- Retry with backoff and a cap, and surface a manual retry when automatic retries stop.
- Warn before an action that will not survive a drop, rather than discovering it afterward.

**MUST NOT**

- Show a success confirmation for anything the server has not confirmed. An optimistic display MUST be visibly provisional and MUST be corrected when the truth arrives, per `../interface/notifications-and-messaging-spec.md`.
- Present cached data as live, or render a stale value with no indication of its age.
- Clear a draft, a form, or a queue as part of an error path, a sign-out, or an update.
- Require a connection to view data the user has already downloaded.

---

## 6. Modality and the low-spec path

| Field | Content |
|---|---|
| **Rule** | Where the constraint profile shows that a share of the audience cannot use the primary interface at all, an alternate path MUST exist and MUST be a first-class edition: same core tasks, same quality gate, same release date. |
| **Why** | Some constraints are not gradients. A device below the platform floor, a network that blocks the protocol, a browser frozen by policy, or a user who will not read a screen does not get a slower version of the product; they get nothing. An alternate path built as a stub gets no tests, no content review, and no maintenance, which is how it ends up worse than having none. This is the same rule `bias-audit-spec.md` §3 applies to languages, for the same reason. |
| **How to verify** | Run the full core task suite on the alternate path with a real user from the affected group. Every task completes, with the same outcome and no step that says to use the main product instead. Compare defect counts between paths; a persistent gap is a blocking defect. |

**MUST**

- Decide from the profile, in writing, whether an alternate path is required, and record the decision and its owner either way.
- Give the alternate path the same core tasks, the same content review, the same test suite, and the same release gate as the primary path.
- Keep account, data, and history shared across paths, so a user can start on one and finish on the other without losing state.
- Support a non-visual path for any core task where the profile lists a modality that is not the screen, and treat audio or voice as an equal channel rather than an accessibility afterthought, per `disability-and-ableism-spec.md` §5.
- Support a non-app channel where the profile shows the platform itself is out of reach, and hold that channel to the same content standards as the app, per `../content/voice-and-content-spec.md`.
- Apply the same privacy and consent rules on every path, since a lower-spec channel usually carries weaker transport guarantees, per `../data/privacy-consent-and-data-handling-spec.md`.

**SHOULD**

- Let the user choose a path rather than inferring it from a capability check alone, and let the choice persist.
- Keep the paths in one codebase or one content source where possible, so a change cannot land on one and miss the other.
- Test the shared and borrowed device case on the alternate path too, per `gender-bias-spec.md` §2.

**MUST NOT**

- Ship an alternate path with a subset of core tasks and call it supported.
- Route a user on the alternate path to a human support queue for something the primary path does automatically.
- Let the alternate path lag a release. Shipping it later is how it stops being maintained.

---

## 7. Testing on the real thing

| Field | Content |
|---|---|
| **Rule** | Before each release, every core task MUST be run on the physical profile device over the profile network conditions, by a person, with the result recorded. |
| **Why** | A throttled desktop browser reproduces bandwidth and nothing else. It runs the profile's code on a fast processor, with a large memory pool, a warm cache, a modern engine, a stable connection, and a screen the tester can read. Every failure specific to the constrained user survives that test intact and reaches them instead. |
| **How to verify** | The release record names the device, the operating system and browser versions, the network conditions, the date, and the person who ran it, and lists each core task as passed or failed. A release with no such record is non-conformant. |

**MUST**

- Test on the physical device named in the profile, at the profile's operating system and browser versions, not on the newest device with a throttle applied.
- Test over real network conditions matching the profile, including latency and packet loss, not bandwidth alone.
- Run the test before release, as a gate, and record the result. A defect found after a user complains does not count as having tested.
- Cover explicitly what a simulator cannot show: sustained processor and memory pressure on old silicon, thermal throttling, a device with almost no free storage, an app killed in the background and resumed, a real captive portal or filtering proxy, screen legibility outdoors or on a worn display, high latency with intermittent loss, battery drain over a full session, and the real cost meter ticking while the task runs.
- Include the alternate path from §6 in the same gate.
- Re-run the gate whenever the profile changes, a dependency is added, or a budget from §3 is raised.

**SHOULD**

- Automate the budget checks from §3 on a physical device in the pipeline, and keep the human run for what automation cannot see.
- Test on a device that has been used, with a full disk, many installed apps, and a degraded battery, rather than a factory-fresh unit.
- Have someone who is not on the build team run the gate at least once per release cycle.

**MUST NOT**

- Substitute an emulator, a simulator, or a throttled desktop browser for the physical device test and report it as passed.
- Test only on the office network.
- Accept a passing automated budget as evidence that a task is completable. The budget measures weight and timing, not whether the flow works.

---

## 8. Conformance checklist

- [ ] Dated constraint profile per market, with an owner and a source for every value (§2).
- [ ] Profile states the share of the audience it covers, and where that number came from (§2).
- [ ] Profile describes conditions, not a stereotype of who the constrained user is (§2).
- [ ] Payload, time-to-interaction, memory, and data-cost budgets set from the profile (§3).
- [ ] Budget checks run automatically and block the merge, with exceptions named and dated (§3).
- [ ] Third-party scripts and analytics counted inside the budget (§3).
- [ ] Written, ordered degradation list with the core task last (§4).
- [ ] Load order matches the degradation order, verified under throttling (§4).
- [ ] Text renders in a fallback face when a custom font does not arrive (§4).
- [ ] Input survives a mid-action connection drop, a crash, and an app restart (§5).
- [ ] Every action shows its true state, and nothing is confirmed before the server confirms it (§5).
- [ ] Cached data carries its age and stops being presented as current past a defined limit (§5).
- [ ] Conflict resolution defined per syncing data type, with the user deciding where it is not safe to guess (§5).
- [ ] Alternate-path decision recorded, either way, with an owner (§6).
- [ ] Alternate path carries the same core tasks, quality gate, and release date as the primary (§6).
- [ ] Core task suite run on the physical profile device over profile network conditions before release (§7).
- [ ] Release record names device, versions, network, date, tester, and per-task result (§7).
