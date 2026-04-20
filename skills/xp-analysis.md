# skills/xp-analysis.md

> Context dependencies: Load `pm-profile.md` and `context/current-quarter.md` before running this skill. KPIs, supporting metrics, and active project names are defined there. Do not hardcode them here.

> Runtime inputs required: (1) experiment data file or screenshot from AB console, (2) relevant project scoping doc from `projects/`.

---

## Purpose

This skill runs a complete experiment analysis and produces three audience-specific outputs from a single input. The goal is to eliminate repetitive formatting work and ensure consistent, high-quality readouts across every channel.

---

## How to invoke this skill

State the following at the start of your session after loading context:

> "Run XP analysis. Inputs: [data file or screenshot filename] and [project scoping doc filename]."

The agent will confirm it has loaded `current-quarter.md` and the project scoping doc before proceeding.

---

## Analytical methodology

Work through these steps in order. Do not skip steps or combine them.

**Step 1: Extract the data**

Before extracting anything, read the project scoping doc and identify:

- Primary metrics: the metrics this experiment is designed to move
- Guardrail metrics: the metrics that must not regress
- Counter-metrics: any secondary metrics being monitored for unintended effects
- Segmentation cuts: any specific user segments called out in the scoping doc (for example mobile vs. desktop, new vs. returning). If segmentation is specified, run the analysis for each segment separately in addition to the overall result.

Then, for each identified metric, extract and report for each variant vs. control:

- Absolute value for variant and control
- Percentage difference vs. control
- Statistical significance: state the confidence level explicitly. If not available in the data, say so. Do not imply significance where it has not been confirmed.

If the scoping doc does not specify metrics clearly, stop and ask before proceeding. Do not infer which metrics to analyze.

**Step 2: Evaluate against current quarter metrics**

Cross-reference the extracted data against the supporting metrics table in `current-quarter.md`. For each metric in that table that is affected by this experiment, state explicitly whether the result is positive, negative, neutral, or inconclusive. Flag any guardrail metrics that moved negatively, even if the movement is within noise.

**Step 3: Summarize the experiment context**

From the project scoping doc, extract and summarize:

- Problem statement and opportunity
- Solution tested: UX change, messaging change, feature change, or model change
- Experiment audience: percentage of users and any segmentation applied
- Hypothesis that was being tested

**Step 4: Form a recommendation**

Based on steps 1 to 3, state a clear recommendation: default, iterate, or roll back. Provide two to three sentences of reasoning. If the data is inconclusive, say that explicitly and state what additional data or runtime would be needed before a decision can be made.

Do not hedge or soften the recommendation. If the data supports a clear call, make it.

---

## Output format

Produce three outputs in sequence. Label each one clearly. Do not combine them.

---

### Output 1: XP analysis (wiki format)

Audience: team and stakeholders who need the full picture. Will be pasted into the project wiki page.

Structure:
- Experiment overview: one short paragraph covering what was tested, why, and who was in the experiment
- Data results: structured table with all metrics, variants, and significance
- Performance summary: one to two paragraphs interpreting the results. What moved, what did not, and what that means
- Recommendation: default, iterate, or roll back with reasoning
- Next steps: two to three concrete actions following the decision

Tone: clear, analytical, no filler. Write for someone who will read this in six months and needs to understand what happened without asking anyone.

---

### Output 2: Stakeholder Slack summary (team channel)

Audience: your immediate team and cross-functional partners. Posted to the internal XP results channel.

Structure:
- One line stating the experiment name and outcome
- Two to three sentences on what was tested and why
- Key metric highlights with directional indicators
- Recommendation and next step
- Link placeholder for wiki

Tone: concise and direct. Use short sentences. Include relevant emojis for scannability. Match the register of a high-performing team's internal channel: not casual, not formal. No jargon that only engineers would understand.

Length: aim for eight to twelve lines maximum. If it is longer, cut it.

---

### Output 3: Company-wide Slack update

Audience: broader company. Posted to a general product or company updates channel. Many readers will have no context on this project.

Structure:
- One sentence on what the experiment was and what it affects
- One sentence on the result
- One sentence on what happens next

Tone: plain language. No metrics unless they are the headline story. No acronyms. Write for someone in finance or operations who cares about outcomes, not methods.

Length: three to five lines maximum.

---

## Sample outputs

The samples below are based on a fictional experiment for Marketflow. Use these to calibrate tone, format, and level of detail for each output type.

---

**Sample experiment:** smart-ranking-v2
A reranking experiment that used real-time behavioral signals to reorder search results for buyers on the Marketflow homepage feed.

---

**Sample output 1: XP analysis (wiki format)**

**Experiment overview**
The smart-ranking-v2 experiment tested a new search ranking model that incorporates real-time click, dwell, and add-to-cart signals to reorder results dynamically. The experiment ran for three weeks across 50% of logged-in buyers on the homepage feed. The hypothesis was that behaviorally informed ranking would surface more relevant results, increasing click-through and downstream conversion.

**Data results**

Metrics below are as defined in the smart-ranking-v2 scoping doc: primary metrics (click-through rate, add-to-cart rate, conversions per user, revenue per user), guardrail metric (page load time), and counter-metric (checkout abandonment rate).

| Metric | Type | Control | Variant | Change | Significant |
|---|---|---|---|---|
| Search click-through rate | Primary | 18.4% | 19.8% | +1.4% | Yes (95%) |
| Add-to-cart rate | Primary | 9.1% | 9.6% | +0.5% | Yes (95%) |
| Total conversions per user | Primary | 0.34 | 0.37 | +8.8% | Yes (99%) |
| Revenue per user | Primary | $4.21 | $4.48 | +6.4% | Yes (95%) |
| Checkout abandonment rate | Counter | 61% | 60.2% | -0.8% | No |
| Page load time (search) | Guardrail | 2.8s | 3.1s | +0.3s | Yes (99%) |

**Performance summary**
The variant drove meaningful improvements across all primary conversion metrics. Click-through rate and add-to-cart both moved positively and reached significance, confirming the hypothesis that behaviorally ranked results surface more relevant items earlier in the feed. Revenue per user lift of 6.4% is material at current traffic volume.

One guardrail metric requires attention before defaulting: page load time increased by 0.3 seconds and reached statistical significance. This exceeds the target threshold of under 2 seconds when combined with the current baseline. The frontend engineering lead should be consulted on whether this can be addressed before rollout.

**Recommendation**
Iterate before defaulting. The conversion and revenue results are strong and support defaulting this experience. However, the page load regression is a guardrail violation that needs to be resolved first. Recommend a two-week sprint to optimize the model serving latency, then re-evaluate for default.

**Next steps**
1. Frontend and ML engineering leads to assess load time regression and propose a fix
2. Re-run load time benchmarks after optimization
3. If load time returns to baseline, proceed with default and company-wide announcement

---

**Sample output 2: Stakeholder Slack summary**

:bar_chart: smart-ranking-v2 XP update: strong results, one guardrail to resolve before defaulting

We tested a new ranking model that uses real-time behavioral signals (clicks, dwell time, add-to-cart) to reorder homepage search results. The goal was to surface more relevant items earlier and drive conversion.

Key results:
:chart_with_upwards_trend: Conversions per user: +8.8%
:moneybag: Revenue per user: +6.4%
:three_button_mouse: Search click-through rate: +1.4%
:warning: Page load time: +0.3s (guardrail exceeded)

The conversion and revenue results are strong. We are not defaulting yet because page load time regressed beyond our threshold. Engineering is scoping a fix now. If resolved in the next two weeks, we will proceed with the default.

Wiki link: [insert link]

---

**Sample output 3: Company-wide Slack update**

Our new search ranking model, which personalizes results based on how buyers interact with the feed, showed an 8.8% increase in purchases per user in testing. We are making a small performance improvement before rolling it out to everyone. Expected rollout in two to three weeks.

---

## Notes for adapting this skill

- The three output formats are fixed. Do not combine them or skip one because it feels redundant. Each serves a different audience with different context and needs.
- Sample outputs are illustrative only. Tone and format should be consistent but content will vary by experiment.
- If statistical significance data is missing from the input, state that clearly in the analysis. Do not estimate or infer significance.
- If a guardrail metric moves negatively, always flag it even if the primary metrics are positive. Do not bury it.

