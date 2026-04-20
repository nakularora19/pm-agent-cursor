# skills/prd.md

> Context dependencies: Load `pm-profile.md` and `context/current-quarter.md` before running this skill.

> Runtime inputs required: The completed opportunity scoping doc for this project from `projects/`. The PRD is phase-specific. Run this skill once per phase, not once per project.

> Output: A phase-level PRD ready to share with engineering, design, and stakeholders.

---

## Purpose

This skill produces a phase-level PRD: the "how and what specifically" document for a single phase of work. It takes the scoping doc as its input and translates the phase description into detailed product requirements.

The scoping doc answers why and what at the project level. The PRD answers what exactly and how we know it is done at the phase level.

One PRD per phase. If a phase is small enough to be captured in a single ticket, skip this skill and write the ticket directly.

---

## How to invoke this skill

State the following at the start of your session after loading context:

> "Run PRD for [phase name]. Input: [scoping doc filename]."

Draft section by section. After each section is drafted, review and confirm before moving to the next. Do not draft the full PRD in one pass.

---

## Document structure and methodology

---

### Section 1: Phase overview

Three to five sentences covering:
- Which phase this is and what project it belongs to
- What this phase delivers and for whom
- How it fits into the broader phased roadmap from the scoping doc
- Link or reference to the parent scoping doc

This section is the orientation for anyone reading the PRD without prior context.

---

### Section 2: Problem reminder

One to two sentences only. Restate the core problem from the scoping doc in the context of this phase. Do not copy-paste from the scoping doc verbatim. Reframe it at the phase level.

This keeps the requirements grounded in the user problem rather than drifting into feature delivery mode.

---

### Section 3: Goals and success metrics

Restate the phase-specific goal in one sentence.

Then list the metrics for this phase pulled from the scoping doc. For each metric confirm:
- Metric name
- Baseline
- Target or direction
- Type: primary, guardrail, or counter-metric

If this phase has experiment-specific metrics not in the scoping doc, add them here and flag them as phase-specific.

---

### Section 4: Scope

**In scope**
List what this phase will deliver. Be specific. Vague scope leads to late-stage disagreements.

**Out of scope**
List what is explicitly not being built in this phase. This is as important as the in scope list. If something obvious is missing, explain why it is deferred.

**Open questions**
List any unresolved decisions that need to be made before or during build. Assign an owner and a deadline for each where possible.

---

### Section 5: User stories and requirements

This is the core of the PRD. For each key user story, state:

- User story: As a [user type], I want to [action] so that [outcome].
- Acceptance criteria: the specific conditions that must be true for this story to be considered done. Write these as testable statements.
- Edge cases: any non-happy-path scenarios that engineering needs to handle.

Group related stories together if the phase has multiple distinct flows.

Keep requirements at the product level, not the implementation level. Describe what the experience should do, not how engineering should build it.

---

### Section 6: Design and UX notes

Reference any design files, prototypes, or research that informs this phase. If designs are not ready, state what decisions are still outstanding and who owns them.

Flag any UX constraints or non-negotiables that requirements must respect.

If no design work exists yet, state that explicitly rather than leaving this section blank.

---

### Section 7: Dependencies and risks

**Dependencies**
List everything this phase depends on that is outside your direct control: other teams, infrastructure, third-party systems, legal review, data availability, etc. For each dependency, state the owner and the lead time required.

Reference `context/current-quarter.md` for known constraints (engineering capacity, DS lead times, legal review cycles).

**Risks**
List the two to three things most likely to go wrong in this phase. For each risk, state the likelihood, the impact, and the mitigation plan.

Do not list risks without mitigations. An unmitigated risk list is just a worry list.

---

### Section 8: Stakeholder and launch plan

Who needs to be informed or involved before, during, and after this phase ships?

Reference the stakeholder table in `context/current-quarter.md`. For each relevant stakeholder, state:
- When they need to be looped in
- What they need to know or approve
- Who owns that communication

Include a brief launch checklist: what needs to be true before this ships to users? (Experiment setup, legal sign-off, comms drafted, metrics instrumented, etc.)

---

## Output format

Produce the PRD as a clean markdown document with the eight sections above as headers. Write as if this will be shared directly with engineering and design leads.

Tone: precise and unambiguous. Every requirement should have one clear interpretation. If something could be read two ways, rewrite it.

Length: as short as it can be while covering all eight sections completely. Cut anything that does not directly help the team build or make decisions. A PRD that is too long does not get read.

---

## Sample output

The sample below covers the MVP phase of the low availability messaging project from Marketflow. It is abbreviated to illustrate tone and structure, not to show every requirement.

---

**Sample: Low availability messaging MVP**

### Phase overview

This is the MVP phase of the low availability messaging project on Marketflow search. It delivers clear messaging and a recovery prompt to buyers who land on search result pages with fewer than five listings. This is Phase 1 of 2 as defined in the opportunity scoping doc: `projects/low-availability-messaging.md`. Phase 2 (personalized recovery recommendations) will be scoped after this phase readout.

### Problem reminder

Buyers hitting low availability pages today have no context for why results are sparse and no clear path to recover their search. This phase directly addresses that gap for the MVP case.

### Goals and success metrics

Goal: Reduce session abandonment on low availability pages by giving buyers a clear explanation and one actionable next step.

| Metric | Baseline | Target | Type |
|---|---|---|---|
| Session abandonment on low-availability pages | 34% above site average | At or below site average | Primary |
| Search refinement rate on low-availability pages | Not instrumented | Increase vs. control | Primary |
| Overall search to checkout conversion rate | 3.2% | No regression | Guardrail |

### Scope

In scope:
- Messaging component explaining why results are limited
- Single recovery CTA: broaden search criteria (adjusts radius or removes filters)
- Trigger logic: display when result count is below five
- Mobile and desktop responsive implementation
- Experiment setup for A/B test against current experience

Out of scope:
- Personalized recommendations (Phase 2)
- Seller-side interventions or inventory nudges
- Changes to search ranking or result fetching logic

Open questions:
- What is the exact threshold for "low availability"? Currently assuming fewer than five results. Confirm with DS partner by [date].
- Should the banner persist if the buyer dismisses it? Owner: frontend engineering lead. Needed before build starts.

### User stories and requirements

**Story 1: Buyer sees low availability messaging**
As a buyer who lands on a search results page with fewer than five listings, I want to understand why results are limited so that I do not think the product is broken.

Acceptance criteria:
- Messaging is displayed when result count is below the defined threshold
- Copy clearly communicates that limited results are due to availability, not a system error
- Messaging is visible above the fold on both mobile and desktop without obscuring existing results

Edge cases:
- Result count changes after initial load (buyer adjusts filters): messaging should update dynamically
- Zero results page: this is a separate state and is out of scope for this phase

**Story 2: Buyer takes a recovery action**
As a buyer seeing the low availability message, I want a clear way to broaden my search so that I can find more options without having to figure out how to adjust filters myself.

Acceptance criteria:
- A single CTA is displayed alongside the messaging
- CTA triggers a predefined search broadening action (expand radius by one step or remove the most restrictive active filter)
- The action and its effect are clearly communicated to the buyer before they take it

Edge cases:
- No filters are active and radius is already at maximum: CTA should not display if no broadening action is available

### Design and UX notes

Wireframes in progress. Design lead to share by [date]. Key constraint: the messaging component must use the existing banner component from the design system. No new components to be created in this phase.

### Dependencies and risks

Dependencies:
- Result count signal: confirmed available in current search API response. No backend changes needed.
- Experiment setup: DS partner needs two weeks lead time for instrumentation. Align on start date before build begins.
- Legal review: not required for this phase. Messaging copy does not touch pricing or fees.

Risks:
- Risk: Messaging copy tone lands as alarming rather than helpful, increasing abandonment. Likelihood: medium. Mitigation: copy to be reviewed by design lead and tested in a low-traffic experiment before full rollout.
- Risk: Dynamic result count update causes messaging to flicker on page load. Likelihood: low. Mitigation: frontend engineering lead to define debounce logic before build.

### Stakeholder and launch plan

- DS partner: loop in now to align on instrumentation and experiment setup timeline
- Frontend engineering lead: align on component approach and open questions before sprint starts
- Design lead: designs needed before build. Currently in progress.
- Head of Marketplace: inform when experiment launches. No approval needed.

Launch checklist:
- Experiment instrumented and validated in staging
- Copy reviewed and approved by design lead
- Mobile and desktop QA complete
- DS partner confirms metric baselines are captured
- Experiment launched at agreed traffic split

---

## Notes for adapting this skill

- Run this skill once per phase, not once per project. The scoping doc covers the full project. This covers one phase.
- Section 4 open questions must have owners. An open question without an owner is just a risk in disguise.
- Section 5 acceptance criteria must be testable. If QA cannot verify it, rewrite it.
- If a phase is simple enough to fit in a ticket, skip this skill entirely and write the ticket. Use judgment on what warrants a full PRD.
