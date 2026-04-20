# pm-agent-cursor

A personal operating system for product managers working with AI tools.

This is not a prompt library. It is a context architecture: a structured set of files that you load into your AI tool of choice so every session starts with full context about who you are, how you work, and what you are working on. The result is that your AI outputs compound in quality over time instead of starting from zero every session.

---

## The core idea

Most PMs use AI by typing a request and hoping for a useful response. The output quality depends entirely on how well the model guesses your context, your standards, and your intent.

This system inverts that. You invest once in building your context layer. Every session loads that context automatically. The model stops guessing and starts working with real information about your role, your KPIs, your projects, and your output standards.

The gap between a PM who does this and one who does not compounds fast.

---

## How it works

The system has four layers. Load them in this order at the start of any task:

```
1. pm-profile.md          Who you are, how you work, your output standards
2. context/               What matters this quarter: KPIs, projects, stakeholders
3. skills/                How to do specific tasks: methodology and output formats
4. projects/              Per-project context: metrics, hypothesis, audience
```

Each layer is independent and reusable. Skills files do not hardcode KPIs. KPIs live in `context/current-quarter.md` and get referenced at runtime. When your quarter changes, you update one file.

---

## Folder structure

```
pm-agent-cursor/
├── pm-profile.md                   Your PM identity, working modes, output standards
├── context/
│   └── current-quarter.md          Company goals, KPIs, active projects, stakeholders
├── skills/
│   ├── xp-analysis.md              Experiment analysis: three outputs from one input
│   ├── prd.md                      PRD writing: section by section with review checklist
│   ├── competitive-research.md     Competitor analysis and synthesis
│   ├── opportunity-scoping.md      Problem framing and opportunity sizing
│   ├── prioritization.md           Tradeoff analysis and sequencing
│   ├── stakeholder-comms.md        Message framing for different stakeholder types
│   └── user-feedback-analysis.md   Qualitative feedback synthesis at scale
├── projects/
│   └── sample-project.md           Template for per-project scoping docs
├── agents/
│   └── README.md                   Multi-step workflows built on top of skills (coming soon)
├── examples/
│   └── README.md                   Sanitized real outputs showing the system in action
└── team/
    └── README.md                   Team capacity and structure layer (v2)
```

---

## Getting started

### Step 1: Fork and personalize

Fork this repo. Start with `pm-profile.md` and replace the content with your own context. Be honest about how you work, including where you are still growing. The profile is most useful when it is accurate, not flattering.

### Step 2: Update the context layer

Open `context/current-quarter.md`. Replace the Marketflow synthetic data with your real company goals, KPIs, active projects, and stakeholders. Update this file at the start of each quarter.

### Step 3: Load into your tool

**Cursor:** Add this repo to your workspace. Reference files using `@filename` in your prompts.

**Claude Projects:** Upload the relevant files to your project context. Start each session by referencing them.

**ChatGPT Projects:** Attach files to your project. Reference them in your system instructions.

**Claude Code / Codex:** Point to the files in your session instructions using their paths.

### Step 4: Run your first skill

Try the XP analysis skill with a real or synthetic experiment:

```
Load pm-profile.md, context/current-quarter.md, and projects/[your-project].md.
Run XP analysis. Inputs: [data file] and [project scoping doc].
```

---

## What is built vs. what is coming

| File | Status |
|---|---|
| `pm-profile.md` | Done |
| `context/current-quarter.md` | Done |
| `skills/xp-analysis.md` | Done |
| `skills/prd.md` | Coming soon |
| `skills/competitive-research.md` | Coming soon |
| `skills/opportunity-scoping.md` | Coming soon |
| `skills/prioritization.md` | Coming soon |
| `skills/stakeholder-comms.md` | Coming soon |
| `skills/user-feedback-analysis.md` | Coming soon |
| `agents/` | Coming soon |
| `examples/` | Coming soon |
| `team/` | v2 |

---

## Design decisions worth knowing

**Why separate context from skills?**
Skills files contain methodology that does not change. KPIs and project context change every quarter. Keeping them separate means you update one file instead of editing every skill file at the start of each quarter.

**Why three outputs from one XP analysis?**
A wiki page, a team Slack message, and a company-wide update serve different audiences with different context and different needs. Producing all three from one analysis run eliminates reformatting work and ensures consistency across channels.

**Why does pm-profile.md include weaknesses?**
An agent that knows where you are still developing can help you compensate proactively. A profile that only lists strengths is decoration, not context.

**Why a projects/ layer?**
Per-project context (primary metrics, guardrails, segmentation, hypothesis) should travel with the project, not be hardcoded into skill files. This makes every skill portable across any experiment or initiative without modification.

---

## Synthetic data notice

All company names, metrics, project names, and examples in this repo use fictional data for Marketflow, a synthetic two-sided marketplace. Nothing in this repo reflects real company data or is attributable to any employer.

---

## Roadmap

- v1: Core context and skills layer (current)
- v2: Team and capacity layer, agent workflows, real examples
