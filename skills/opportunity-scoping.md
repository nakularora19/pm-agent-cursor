# skills/opportunity-scoping.md

> Context dependencies: Load `pm-profile.md` and `context/current-quarter.md` before running this skill. Company goals and KPIs are defined there.

> Runtime inputs required: A problem statement or raw signal (user feedback, data finding, engineering observation, etc.) to start from.

> Output: A completed opportunity scoping doc. This becomes the input for `skills/prd.md` when moving into phase-level requirements.

---

## Purpose

This skill produces an opportunity scoping doc: the "why and what" document that validates a problem, sizes the opportunity, and lays out a phased approach to solving it. It is written before any phase-level PRD and serves as the anchor document for the entire project.

A good scoping doc answers three questions: Does this problem demonstrably exist? Is it worth solving given our current goals? How would we approach solving it in phases?

---

## How to invoke this skill

State the following at the start of your session after loading context:

> "Run opportunity scoping. Starting point: [problem statement or raw signal]."

Work through the sections in order. Do not skip ahead to solutions before the problem and proof points are solid. If the problem statement is weak or vague, stop and sharpen it before continuing.

---

## Document structure and methodology

Work through these sections in order. Draft each section before moving to the next. Do not draft the full document in one pass.

---

### Section 1: Problem definition

Write a clear, specific articulation of the problem. One to three sentences maximum.

A strong problem definition:
- Names the specific user or stakeholder experiencing the problem
- Describes what is happening and what the consequence is
- Avoids implying a solution

A weak problem definition is vague, too broad, or already implies a fix. If it reads like a solution brief, rewrite it.

Ask before drafting this section: who exactly has this problem, and what happens to them because of it?

---

### Section 2: Proof points

This section validates that the problem is real. List every signal you have that confirms the problem exists. Signals can be qualitative or quantitative.

Valid signal types:
- User feedback: direct quotes, support tickets, NPS verbatims, research findings
- Quantitative data: drop-off rates, error rates, low engagement metrics, funnel gaps
- Engineering feedback: known technical pain points affecting user experience
- Design observations: usability issues surfaced during research or reviews
- Commercial or partner feedback: signals from sales, account managers, or partners
- Internal user feedback: observations from people inside the company who use the product

Minimum bar: one strong, clear signal is enough to proceed. It does not need to be exhaustive. What matters is that at least one proof point is specific and credible, not that you have covered every source.

For each proof point, state: the source, what it shows, and why it is relevant to the problem.

If no strong proof point exists, flag this explicitly. Do not proceed to the hypothesis until the problem has at least one real signal behind it.

---

### Section 3: Hypothesis

One to two sentences only. State clearly what you believe will happen if you solve this problem and why.

A strong hypothesis:
- Takes a clear point of view. No hedging.
- Connects the solution direction to a specific outcome
- Is falsifiable: you could prove it wrong with data

Format to follow:
> If we [solution direction], then [expected outcome] because [reasoning].

A weak hypothesis is vague, covers multiple bets at once, or reads like a goal statement rather than a belief. Rewrite it until it takes a clear position.

---

### Section 4: Goal

One sentence. What does success look like at the project level?

This is not a metric. It is the outcome you are pursuing. The metric comes in the next section.

Example: "Make it easier for buyers to find relevant results on their first search."

---

### Section 5: Success metrics

List the metrics that will tell you whether you achieved the goal. Pull from `context/current-quarter.md` for north star and supporting metrics where relevant.

For each metric, state:
- Metric name
- Current baseline (if known)
- Target or direction of movement
- Type: primary, guardrail, or counter-metric

Keep this list short. Two to four metrics is usually right. If you have more than five, you are measuring everything and optimizing for nothing.

---

### Section 6: Opportunity sizing

This is where you make the case for why this is worth solving now. Connect the problem to the numbers.

Include:
- How many users are affected and how often
- What the current metric looks like and what it could look like if solved
- The downstream impact: what does a X% improvement in this metric mean for conversions, revenue, or retention? Reference the north star KPI from `context/current-quarter.md` to anchor this.
- Any time sensitivity: is there a reason to solve this now versus later?

Be specific with numbers. A vague opportunity section does not help prioritization conversations. If you do not have exact figures, use ranges and state your assumptions explicitly.

---

### Section 7: Phased roadmap

Lay out how you would approach solving this problem in phases. Each phase should represent a meaningful increment of value, not just a chunk of engineering work.

For each phase:
- Phase name (e.g. MVP, Phase 2, Phase 3)
- One sentence on what this phase delivers and for whom
- Key scope inclusions: what is in
- Key scope exclusions: what is explicitly out
- Dependencies or prerequisites
- Rough sizing if known (S, M, L or weeks estimate)

Each phase will get its own PRD using `skills/prd.md`. The scoping doc does not need to define requirements at that level.

Note: if a phase is small enough that requirements can be captured in a single ticket, state that explicitly rather than planning a full PRD for it.

---

## Output format

Produce the scoping doc as a clean markdown document with the seven sections above as headers. Use the document as if it will be pasted into a wiki or shared with stakeholders directly.

Tone: clear and direct. Write for someone who will read this without any prior context on the problem. No jargon, no filler, no passive voice.

Length: as short as it can be while still being complete. A strong scoping doc is usually one to two pages. If it is running longer, cut the proof points section down to the three strongest signals and tighten the opportunity sizing.

---

## Sample output

The sample below uses the Marketflow synthetic company. Use it to calibrate tone, structure, and level of detail.

---

**Sample: Low availability messaging on Marketflow search**

### Problem definition

Buyers who land on search result pages with fewer than five listings have no indication of why results are scarce or how to broaden their search. This creates a confusing dead-end experience that leads to session abandonment.

### Proof points

- Quantitative: Internal funnel data shows a 34% higher session abandonment rate on pages returning fewer than five results compared to the overall search average. Affects approximately 8% of search sessions.
- User feedback: Recurring theme in NPS verbatims: buyers describe feeling confused or thinking the product is broken when they see sparse results pages. Three separate usability sessions in Q3 surfaced the same behavior unprompted.

### Hypothesis

If we surface clear messaging explaining why results are limited and provide an actionable prompt to broaden search criteria, buyers will recover their session rather than abandoning, improving conversion rate on low-availability pages without negatively impacting overall metrics.

### Goal

Help buyers understand and recover from low availability search results instead of abandoning their session.

### Success metrics

| Metric | Baseline | Target | Type |
|---|---|---|---|
| Session abandonment rate on low-availability pages | 34% above average | Neutral or better vs. average | Primary |
| Search refinement rate on low-availability pages | Unknown | Increase vs. control | Primary |
| Overall search to checkout conversion rate | 3.2% | No regression | Guardrail |

### Opportunity sizing

8% of search sessions currently land on low-availability pages. Of those, abandonment is 34% higher than the site average. If we reduce abandonment on these pages to the site average, the estimated recovery is approximately 2.7% of currently lost sessions. At current traffic and average order value, this represents an estimated $1.1M in incremental GMV per quarter. No engineering infrastructure changes required, making this a high return, low cost opportunity.

### Phased roadmap

**MVP**
Deliver clear messaging on low-availability pages explaining the situation and surfacing one actionable recovery prompt (broaden search criteria).
In scope: messaging copy, banner component, trigger logic based on result count threshold.
Out of scope: personalized recommendations, seller-side interventions.
Dependencies: frontend component library, result count signal available in current API response.
Sizing: M (3 to 4 weeks including experiment setup).
PRD: `projects/low-availability-messaging-mvp.md`

**Phase 2**
If MVP validates the messaging approach, expand recovery options to include personalized suggestions based on search history.
In scope: recommendation logic, ML signal integration.
Dependencies: ML and AI DS lead, 3 to 4 week lead time required.
Sizing: L (6 to 8 weeks).
PRD: to be written after MVP readout.

---

## Notes for adapting this skill

- The proof points section is the most commonly skipped. Do not skip it. A scoping doc without validated proof points is a solution looking for a problem.
- The hypothesis must take a position. If it could apply to any project, it is too generic.
- The opportunity sizing section should always connect to the north star KPI in `context/current-quarter.md`. If you cannot draw that line, reconsider whether this is the right problem to solve right now.
- Each phase in the roadmap will become its own PRD using `skills/prd.md`. Keep phase scope tight enough that a PRD is achievable without becoming unwieldy.
