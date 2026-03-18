# Firefox Product Strategy Skills for Claude Code

Two Claude Code slash commands for Firefox PMs:

- **`/bet`** — takes a raw feature idea and produces a leadership-ready strategy brief + engineering estimate handoff
- **`/plan`** — takes an approved engineering estimate and produces a sequenced, file-level implementation plan

Designed for Firefox PMs. Tested against real product ideas including full briefs, reframes, and kill recommendations.

---

## Installation

Copy skills to your Claude commands directory:

```
cp bet.md ~/.claude/commands/bet.md
cp plan.md ~/.claude/commands/plan.md
```

Restart Claude Code (or start a new session), then invoke with `/bet` or `/plan`.

```
/bet I want to build a feature that shows users their per-site data consumption...
```

```
/plan [paste Engineering Estimate Handoff + EngEstimator breakdown]
```

---

## Optional dependencies

The skill works without any of these. Each improves analysis fidelity.

| Dependency | What it enables | How to check |
|------------|-----------------|--------------|
| Local Firefox repo | Verified pref lookups, FeatureManifest checks, prior art | Auto-detected at `~/firefox`, `~/mozilla-central`, `~/src/firefox`, `~/src/mozilla-central` |
| `searchfox-cli` | Symbol and API lookup against Mozilla codebase | `which searchfox-cli` |
| Glean Dictionary MCP | Metric verification without a local repo | Check MCP tool list at session start |

If none of these are present, the skill falls back to searchfox.org web lookups and flags lower-confidence findings.

---

## What you get

**Strategy brief** covering:
- The Bet and The Payoff
- Bottom Line: recommendation (Explore / Validate / Build), why now, #1 open question
- Strategy Alignment across Firefox pillars with explicit DAU/revenue links
- Mozilla Mission check — structural advantage and limits
- Trust & Agency Check with flag key (🔴 redesign or stop / 🟡 mitigable / 🟢 clean)
- Technical Feasibility with verified file:line citations
- UX Dependencies
- Versioning Plan with decision gates
- Measurement Plan (feature metrics + guardrails)
- Key Assumptions & Open Questions

**Engineering Estimate Handoff** — on request after the brief. Structured input for an engineering estimation workflow, compatible with EngEstimator-style skills.

---

## What /plan produces

Takes the Engineering Estimate Handoff from `/bet` plus an EngEstimator `show breakdown` output and produces:

- **Execution sequence** — tiered checklist (Tier 1 foundational → Tier N testing), respecting Firefox's mandatory build ordering (moz.build, WebIDL, IPDL, StaticPrefs, metrics.yaml, header-before-impl, etc.)
- **Task details** — for each task: exact file path, Create/Modify action, what to write (function signatures, class structure, key logic), pattern reference (file:line of analogous Firefox code), verification command, point estimate, and dependencies
- **Open items table** — unresolved EngEstimator questions that block specific tasks

Output is a document for human review. Code execution is a separate deliberate step.

---

## What to expect

**`/bet`:**
- Conversational, not one-shot. May ask 1–2 clarifying questions before running analysis.
- Splits bundled sub-bets before producing a brief.
- Recommends stopping (with reframe) for fatal strategic or financial flaws — it will not produce a brief for a bet that should be killed.
- Analysis improves significantly with: platform, urgency signal ("why now"), and known technical constraints upfront.

**`/plan`:**
- Requires three inputs: the `/bet` Engineering Estimate Handoff, EngEstimator `show breakdown` output, and the phase to plan (V1 by default).
- Reads source files from the EngEstimator's identified paths before producing the plan — this is not a one-shot from text alone.
- Produces a document for review. Verify file paths and patterns with the engineering team before executing task by task.

---

## Tips

- **Be specific about the user problem.** "Google's misalignment with Mozilla's values" is a company problem, not a user problem. The skill will catch this and push back.
- **Provide a platform.** Android and Desktop have different strategic weights, different technical stacks, and different DAU implications.
- **Include a "why now" if one exists.** Urgency signals (competitive window, platform moment, leadership deadline) directly influence the recommended stage.
- **Don't clean up the idea first.** The skill is designed to work with raw, half-formed thinking — that's when it's most useful.
