---
name: ux-audit
description: >
  Run structured UX audits using proven frameworks (HEART, LIFT, UXR/HEA, CORE).
  Use this skill whenever the user mentions: UX audit, UX review, usability problems,
  user flow issues, onboarding problems, drop-off, conversion problems, product friction,
  "users are confused", "why do users leave", "check my design", "analyze this flow",
  "improve my product", or any request to evaluate a digital product's user experience.
  Activates when user shares a screenshot, URL, or description of an interface and
  wants to understand what's wrong. Also use when combining multiple UX frameworks,
  or when the user wants to produce structured UX findings for a team or stakeholder.
  This skill handles the full audit process end-to-end — intake, framework selection,
  structured analysis, prioritized recommendations, and success metrics.
---

# UX Audit Skill

Structured UX analysis using four proven frameworks. Run the full process — the
user does not need to know any frameworks or prompts.

---

## Step 1 — Intake: Check what was provided

**Scan the conversation immediately:**

| Provided | Action |
|----------|--------|
| Screenshot / image | **Mode A** — skip questions, start audit now |
| URL | **Mode B** — crawl with Playwright, then audit |
| Text description only | **Mode C** — ask max 3 focused questions |

### Mode C questions (text only)
Ask only what's missing. Stop at 3.
1. **What is the product / flow?** (what exactly are we auditing)
2. **Where does it hurt?** (onboarding, conversion, retention, specific feature)
3. **What signals do you have?** (user quotes, analytics, support complaints)

If any of this was already provided — skip straight to Step 2.

---

## Step 2 — Select framework

| Situation | Framework |
|-----------|-----------|
| Product scaled but users don't love it / low NPS | **HEART** |
| Drop-off, users not converting, something blocking action | **LIFT** |
| You know *what* breaks but not *why* | **UXR / HEA** |
| Team needs fast decision + clear next steps | **CORE** |
| Post-research: synthesizing interviews or tests | **Synthesis** |

When uncertain → use **LIFT** (fastest, most actionable for most cases).

State which framework you chose and why in one sentence before running it.

Read the full framework spec from `references/frameworks.md` before executing.

---

## Step 3 — Run the audit

Always structure output as:

```
## UX Audit — [Framework name]

### What we analyzed
[1–2 sentences on scope and input mode used]

### Key findings
[3–7 findings. Each: description + severity (high/med/low) + location in flow]

### Root causes
[Not symptoms — the actual reason the problem exists.
"Button is small" = symptom. "User doesn't know what happens next" = root cause.]

### Prioritized recommendations
1. [Highest impact fix] — why this first
2. [Second fix] — why
3. [Third fix] — why

### What to measure
[How you'll know if the fix worked — specific metric or observable behavior]
```

---

## Step 4 — Offer next steps

After delivering the audit, offer one of:
- "Want me to go deeper on any specific finding?"
- "Should I write a design brief for the top recommendation?"
- "Want a second perspective using a different framework?"

---

## Input modes — detailed execution

### Mode A — Screenshot / image (fastest)

Start immediately when an image is provided. Do not ask clarifying questions first.

1. Describe what you see: layout, hierarchy, copy, interactive elements
2. Identify the user's likely goal at this screen
3. Select framework (default: LIFT for single screens, HEART for full product)
4. Run audit from visual analysis alone

Be specific about visual elements:
- "The primary CTA is below the fold on mobile"
- "There are 4 competing headlines with equal visual weight"
- "No trust signals visible near the payment form"

If multiple screens → map the flow first, then audit across it.

---

### Mode B — URL (live audit)

Use Playwright via bash to crawl the flow and capture real screenshots before auditing.

```bash
npm install -g playwright 2>/dev/null
npx playwright install chromium 2>/dev/null

node -e "
const { chromium } = require('playwright');
(async () => {
  const browser = await chromium.launch();
  const page = await browser.newPage();
  await page.setViewportSize({ width: 1280, height: 800 });
  await page.goto('URL_HERE');
  await page.screenshot({ path: '/home/claude/screen_01.png', fullPage: true });
  // Navigate key steps and capture each
  await browser.close();
})();
"
```

After capturing:
1. View each screenshot
2. Map the full flow (entry → goal completion)
3. Note: hierarchy, CTA placement, trust signals, friction points, copy clarity
4. Run audit across the full captured flow

---

### Mode C — Text description

Run heuristic audit from description alone after asking the 3 intake questions.
Use evidence from user quotes, analytics, or support tickets to strengthen findings.

---

## Severity scale

| Level | Definition |
|-------|------------|
| **High** | Blocks the user or causes errors — fix immediately |
| **Medium** | Creates friction, confusion, or hesitation — fix this sprint |
| **Low** | Polish — improves experience but not blocking |

---

## Key principles

- **Specific over generic** — Never "improve clarity". Say which element, what the problem is, and what to change.
- **Root cause over symptom** — Diagnose why, not just what.
- **One framework per audit** — Don't blend frameworks in a single audit.
- **Severity always** — Rate every finding. Not all problems are equal.
- **Business framing** — Express findings in terms of conversion, retention, and trust.
- **Cognitive load lens** — Most UX problems are cognitive overload in disguise.

---

## Integration with other skills

- **design-intelligence** → cognitive science behind why a problem exists
- **ux-designer** → strategy, psychology, and flow redesign recommendations
- **refactoring-ui** → visual hierarchy, spacing, color, and typography fixes
- **ux-process** → if the audit reveals a need for research or redesign planning

---

## Reference files

- `references/frameworks.md` — Full specs for HEART, LIFT, UXR/HEA, CORE, Synthesis, and Cognitive Load checklist
