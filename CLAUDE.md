## `.claude/` Directory Structure

- **`docs/`** — Architectural design references (architecture, tech decisions, data models, integrations, agent designs). `{topic}.md`
- **`specs/`** — Implementation specs, written before coding (state machine rules, tool definitions, API contracts, Pydantic schemas). Codeable detail level. `{topic}.spec.md`
- **`tasks/`** — Active work tracking. `progress.md` for overall status, `{type}-{desc}.task.md` for individual tasks (implementation steps, bugs, spikes)
- **`reports/`** — Completed analysis/research snapshots (reviews, benchmarks, spike findings, audits, post-mortems). Immutable after creation. `{topic}.report.md`
- **`cookbooks/`** — Step-by-step how-to recipes (add agent, add tool, debug Unity, extend pipeline, dev setup). `{action}.cookbook.md`