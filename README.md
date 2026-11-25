# claude-ops-agents

Three Claude Code subagents for the operating side of a small online business: trustworthy numbers, spend decisions, and pages that convert.

- `data`: builds a regime map of everything that changed what a metric means (product versions, pricing models, funnel and tracking changes), tags contaminated data (bots, tests, legacy prices, broken tracking windows) without deleting it, publishes a trusted metric set with n, 95% intervals and a USABLE / DIRECTIONAL / DO-NOT-USE verdict, and plans sample sizes for pending decisions. Read-only on production systems.
- `finance`: decides every spend from unit economics (ARPU, churn, LTV, conversion chain, break-even CAC, max CPC), using trusted metrics first and labelling every number MEASURED, BENCHMARK or ASSUMED. Returns YES, NO, or TEST with a cap, end date and kill rule. It decides but never executes spend or enters payment details.
- `page-designer`: builds and reviews web pages reference-first. Captures real comparable pages, writes a measured design map, gets all words from your sales or copy agent, renders side by side at desktop and phone, walks every element for its conversion effect, runs QA with tracking totals checked before and after, deploys, and verifies live.

## Install

```
cp agents/*.md ~/.claude/agents/
# or, for one project
cp agents/*.md <your-project>/.claude/agents/
```

Restart Claude Code or run `/agents` to check they load.

## Files you need to create

- `knowledge/GOAL.md`: your current business goal.
- `research/DECISIONS-CURRENT.md`: a numbered decision log. Agents read the newest entries and append their own.
- `research/data/TRUSTED-METRICS.md`: created and kept current by the data agent. The finance agent reads it.
- Optional `knowledge/FINANCE-TARGETS.md`: your payback and LTV:CAC targets if they differ from the defaults (3 months, 3x).
- `knowledge/page-designer/KNOWLEDGE.md`: workflow detail, hard rules with reasons, the element-by-element conversion walk, a fold-measuring script, deploy steps, past mistakes, and a "settled, do not flag" list.
- `knowledge/page-designer/TOOLKIT.md`: the tools you have installed and which to use for which job.
- For page work: a product-facts file (what may be claimed), a copy canon, an offer file, a proof file with real results only, and a funnel-stages file shared with your sales agent.
- `lessons/<agent>.md`: one lessons file per agent, append only.

## Notes

The page designer calls a sales agent for every customer-facing word. The `claude-sales-agent` repo has one, or point it at your own.

All three agents ask the owner before any spend, account change, or production change.
