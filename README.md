# ux-audit

> Claude skill — structured UX audits using proven frameworks.

## What it does

Runs end-to-end UX audits on any digital product. Works from screenshots, URLs, or text descriptions. Identifies root causes (not just symptoms), prioritizes fixes by severity, and defines metrics to measure improvement.

## Frameworks included

**HEART** (Google) — When the product has scaled but users do not love it. Measures Happiness, Engagement, Adoption, Retention, Task success. Best for low NPS or satisfaction problems.

**LIFT** (WiderFunnel) — When users are not converting or dropping off. Analyzes Value, Relevance, Clarity, Anxiety, Distraction, Urgency. Best for funnel optimization and landing pages.

**UXR / HEA** — When you know *what* breaks but not *why*. Maps: What Happens → Why It Happens → What to Change. Best for diagnosing onboarding failures and feature abandonment.

**CORE** — When the team needs a structured decision fast. Covers Context, Obstacles, Resolution, Evaluation. Best for mid-sprint pivots and stakeholder reviews.

**Synthesis** — After user research. Clusters signals into patterns, extracts insights, produces prioritized recommendations from interviews or usability tests.

## How it works

Claude automatically selects the right framework based on your problem, then delivers findings with severity ratings, root causes, and specific recommendations — not generic advice.

Input modes:
- **Screenshot / image** → instant audit, no questions asked
- **URL** → Playwright crawl, then audit across the full flow
- **Text description** → 3 intake questions, then heuristic audit

## Structure

```
ux-audit/
├── SKILL.md              # Main skill logic and intake process
└── references/
    └── frameworks.md     # Full specs: HEART, LIFT, UXR/HEA, CORE, Synthesis
```

## Install

Download `ux-audit.skill` from [Releases](../../releases) and install via Claude.ai → Settings → Skills.

