# /bet — Firefox Strategy Skill for Claude Code

A Claude Code slash command that takes a raw feature idea and produces a leadership-ready strategy brief — grounded in Mozilla mission, Firefox pillars, technical feasibility verification against the codebase, and shipping reality.

Designed for Firefox PMs. Tested against real product ideas including full briefs, reframes, and kill recommendations.

---

## Installation

1. Copy `bet.md` to `~/.claude/commands/bet.md`
2. Restart Claude Code (or start a new session)
3. Invoke with `/bet` followed by your idea

```
/bet I want to build a feature that shows users their per-site data consumption...
```

That's it. The skill will ask clarifying questions if needed, then run deep analysis and produce a strategy brief.

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

**Engineering Estimate Handoff** — on request after the brief. Structured input for an engineering estimation workflow.

---

## What to expect

- The skill is a **conversation**, not a one-shot generator. It may ask 1–2 clarifying questions before running analysis.
- If an idea has **bundled sub-bets**, the skill will split and reframe before producing a brief.
- If an idea has **fatal strategic or financial flaws**, the skill will recommend stopping and propose the smallest viable reframe — it will not produce a brief for a bet that should be killed.
- Analysis depth improves significantly if you provide: platform (Android/Desktop/Both), urgency signal ("why now"), and any known technical constraints upfront.

---

## Tips

- **Be specific about the user problem.** "Google's misalignment with Mozilla's values" is a company problem, not a user problem. The skill will catch this and push back.
- **Provide a platform.** Android and Desktop have different strategic weights, different technical stacks, and different DAU implications.
- **Include a "why now" if one exists.** Urgency signals (competitive window, platform moment, leadership deadline) directly influence the recommended stage.
- **Don't clean up the idea first.** The skill is designed to work with raw, half-formed thinking — that's when it's most useful.
