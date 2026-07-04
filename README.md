# skill-bank

A curated, merged **skill bank** of general, environment-agnostic methodology
skills, organized for the [Ling-RL](https://github.com/dddgogogo) skill-hint
teacher (SDAR-channel self-distillation). Each skill follows the
[Agent Skills](https://agentskills.io/) standard (`SKILL.md` with YAML
frontmatter + a rich markdown body), so this repo also works as a plain
Agent-Skills library for Claude Code, Cursor, Codex, etc.

## Sources

This bank **merges three upstream libraries verbatim** (skill bodies unchanged);
all three are MIT-licensed. Full credit to their authors:

| Category (here) | Upstream | Author | Skills |
|---|---|---|---|
| `thinking-models/` | [tjboudreaux/cc-thinking-skills](https://github.com/tjboudreaux/cc-thinking-skills) | tjboudreaux | 39 |
| `context-engineering/` | [muratcankoylan/agent-skills-for-context-engineering](https://github.com/muratcankoylan/agent-skills-for-context-engineering) | Muratcan Koylan | 15 |
| `thinking-partner/` | [mattnowdev/thinking-partner](https://github.com/mattnowdev/thinking-partner) | mattnowdev | 1 (150+ models) |

See `LICENSE` for the license notice and per-source attribution.

## How it is reorganized

The upstream repos ship their skills under `skills/` alongside their own docs,
evals, and tooling. This bank keeps **only the skills**, regrouped into three
flat category directories and stripped of repo cruft:

```
thinking-models/            # cc-thinking-skills, "thinking-" prefix dropped
  .overview                 # curated navigation (what each skill is / when to use)
  first-principles/SKILL.md
  bayesian/SKILL.md
  ...
context-engineering/
  .overview
  tool-design/SKILL.md
  ...
thinking-partner/           # one integrated meta-skill (150+ models)
  .overview                 # navigation (one whole meta-skill)
  SKILL.md
  references/               # L3 model catalog + diagnostics (progressive disclosure)
```

## `.overview` navigation

Every category carries a hand-curated `.overview` — the L1 navigation the
skill-hint judge reads to select a skill. Each line is
`` `<id>`: <name> — <when to use> `` where `<id>` is the stable selection id
(e.g. `builtin/thinking-models/first-principles`). The `builtin/` prefix
reflects that this repo is mounted as the bank's shipped `builtin/` layer.

Skills are selected and read **whole** — the bank never splits a skill into
fragments. The integrated `thinking-partner` skill is one entry
(`builtin/thinking-partner`); its `references/` provide the full 150+-model
catalog via progressive disclosure.

## Using it with Ling-RL

Mounted as a git submodule; the skill-hint teacher's loader scans it as the
`builtin/` layer (operator libraries live in a sibling `user/` layer). See
Ling-RL `docs/skill-bank.md`.
