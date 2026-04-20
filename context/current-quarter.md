# context/current-quarter.md

> SYNTHETIC DATA: All company names, metrics, targets, and project details in this file are fictional and created for illustrative purposes only. Replace every section with your own context before using.

> Update this file at the start of each quarter. All skills files reference this for KPIs, priorities, and constraints.

---

## Company

**Marketflow** is a two-sided marketplace connecting buyers and sellers across product categories. The platform spans search, discovery, checkout, and seller tooling.

---

## Company goals this quarter

These are the top-level goals your work should ladder up to. Reference these when justifying prioritization decisions or scoping new opportunities.

1. Grow gross merchandise value (GMV) by 12% quarter over quarter
2. Improve buyer retention: increase 90-day repeat purchase rate from 34% to 40%
3. Reduce seller churn by improving listing quality and visibility tooling
4. Expand into two new product categories without degrading core category metrics

---

## My north star KPI

**Search to checkout conversion rate**
Current: 3.2%
Target: 3.8% by end of quarter
Why it matters: This is the primary lever connecting discovery quality to revenue. A 0.1% improvement at current traffic volume equals approximately $2.4M incremental GMV.

---

## Supporting metrics

These are the guardrail and diagnostic metrics I track alongside the north star. Any experiment or initiative should be evaluated against this set.

| Metric | Current | Target | Type |
|---|---|---|---|
| Search click-through rate | 18.4% | 20% | Leading indicator |
| Add-to-cart rate | 9.1% | 10.5% | Leading indicator |
| Checkout abandonment rate | 61% | 55% | Guardrail |
| Buyer NPS | 34 | 38 | Health metric |
| Page load time (search) | 2.8s | under 2s | Guardrail |

---

## Active projects

These are the initiatives in flight this quarter. Reference these when scoping tasks, writing tickets, or analyzing experiments.

| Project | One-liner | Status |
|---|---|---|
| Smart ranking v2 | Reranking search results using real-time behavioral signals | In experiment |
| Filters redesign | Simplifying filter UX to reduce friction on mobile | In development |
| Sparse result state messaging | Contextual guidance for users encountering sparse search results | Experiment readout pending |
| Seller badge system | Trust signals on listings to improve buyer confidence | Discovery |
| Checkout simplification | Reducing steps in the checkout flow for returning buyers | Scoping |

---

## Constraints and context

Things that should color all work this quarter. Reference these when making tradeoffs or giving recommendations.

**Engineering capacity:** Two senior engineers are allocated to the ranking system. All other projects share a pool of three mid-level engineers. Assume 20% of capacity is absorbed by on-call and debt.

**Design:** One designer shared across all non-ranking projects. Prioritize work that can reuse existing components.

**Data science:** One DS embedded with the team. Lead time for any new instrumentation or experiment setup is two weeks minimum.

**Legal and compliance review:** Any experiment touching pricing display or seller fees requires a two-week legal review cycle. Flag early.

**Q1 carryover:** The checkout simplification project was descoped in Q1 due to a platform migration. Stakeholder expectations are already set. Treat as high visibility.

---

## Stakeholder context

Key people whose priorities and communication styles should inform how work is framed and communicated.

**Core team (frequent)**

| Name | Role | What they care about | Communication preference |
|---|---|---|---|
| [Head of Marketplace] | Skip-level | GMV and seller health | Data-first, brief, no fluff |
| [Design lead] | Cross-functional partner | Consistency and user research grounding | Collaborative, needs early loop-in before decisions are made |
| [Backend engineering lead] | Day-to-day partner | System reliability, technical debt, API contracts | Direct, dislikes late-breaking scope changes |
| [Frontend engineering lead] | Day-to-day partner | Component reuse, performance, mobile experience | Practical, wants clear acceptance criteria upfront |
| [Embedded DS partner] | Product-side data science | Experiment validity, metric definitions, readout rigor | Detail-oriented, appreciates early alignment on success criteria |
| [Commercial lead] | Revenue and partnerships | Monetization impact, seller and partner relationships | Monthly cadence. Business-outcome framing, connect work to revenue or strategic accounts. Loop in for anything touching pricing, seller incentives, or category expansion. |

**Extended team (less frequent)**

| Name | Role | What they care about | Communication preference |
|---|---|---|---|
| [ML and AI DS lead] | ML model and AI infrastructure owner | Model performance, data pipeline health, long-term architecture | Looped in at architecture and scoping stage, not sprint level. Needs lead time of 3 to 4 weeks for any model-level changes. Separate from product DS work. |
| [Legal and regulatory lead] | Compliance and risk | Policy adherence, regulatory exposure, user data handling | Loop in early for anything touching pricing display, seller fees, data collection, or new market entry. Two-week review cycle minimum. |

> Note: Replace bracketed names with real names in your private version. Keep this section out of any public or shared repo.

---

## v2 placeholder: team and capacity layer

> Coming in v2. This section will capture team structure, individual strengths, current capacity, and known constraints at the person level. The goal is to give the agent enough context to help with realistic planning, sequencing, and delegation decisions rather than generic recommendations.

> Planned contents: team roster with roles and tenure, capacity allocation by project, known skill gaps, hiring or onboarding context, and any team-level constraints for the quarter.

