# skill-bank

A curated, merged **skill bank** of general, environment-agnostic methodology
skills, organized for the [Ling-RL](https://github.com/dddgogogo) skill-hint
teacher (SDAR-channel self-distillation). Each skill follows the
[Agent Skills](https://agentskills.io/) standard (`SKILL.md` with YAML
frontmatter + a rich markdown body), so this repo also works as a plain
Agent-Skills library for Claude Code, Cursor, Codex, etc.

## Sources

This bank **merges three upstream libraries verbatim** (skill bodies unchanged);
all three are MIT-licensed. A fourth category, `coding-skill/`, holds short
methodology skills **distilled** (not copied verbatim) from well-regarded
community coding-agent skills — each `SKILL.md` carries its own attribution.
Full credit to all authors:

| Category (here) | Upstream | Author | Skills |
|---|---|---|---|
| `thinking-models/` | [tjboudreaux/cc-thinking-skills](https://github.com/tjboudreaux/cc-thinking-skills) | tjboudreaux | 39 |
| `context-engineering/` | [muratcankoylan/agent-skills-for-context-engineering](https://github.com/muratcankoylan/agent-skills-for-context-engineering) | Muratcan Koylan | 15 |
| `thinking-partner/` | [mattnowdev/thinking-partner](https://github.com/mattnowdev/thinking-partner) | mattnowdev | 1 (150+ models) |
| `coding-skill/` (distilled) | caveman · handoff · andrej-karpathy-skills | mattpocock / JuliusBrussee · mattpocock · forrestchang / multica-ai (per skill) | 3 |

See `LICENSE` for the license notice and per-source attribution.

## How it is reorganized

The upstream repos ship their skills under `skills/` alongside their own docs,
evals, and tooling. This bank keeps **only the skills**, regrouped into flat
category directories and stripped of repo cruft. The Stage-A catalog is now
generated live from each skill's frontmatter, so the per-category `.overview`
files were dropped:

```
thinking-models/            # cc-thinking-skills, "thinking-" prefix dropped
  first-principles/SKILL.md
  bayesian/SKILL.md
  ...
context-engineering/
  tool-design/SKILL.md
  ...
thinking-partner/           # one integrated meta-skill (150+ models)
  SKILL.md
  references/               # L3 model catalog + diagnostics (progressive disclosure)
coding-skill/               # distilled community coding-agent methodology skills
  caveman/SKILL.md
  handoff/SKILL.md
  karpathy-agent-discipline/SKILL.md
```

## Catalog / navigation

The L1 navigation the skill-hint judge reads to select a skill is **generated
live from each skill's frontmatter** — one `## <category>` section per top-level
dir, each listing every member as `` `<id>`: <name> — <description> `` where
`<id>` is the stable selection id (e.g.
`builtin/thinking-models/first-principles`). The `builtin/` prefix reflects that
this repo is mounted as the bank's shipped `builtin/` layer. Because the catalog
is regenerated on load, it never goes stale — add a skill and it appears next
reload. A category may optionally carry a `.overview` file whose prose is
prepended to that section as a framing preamble (not the skill list); the
shipped bank ships none.

Skills are selected and read **whole** — the bank never splits a skill into
fragments. The integrated `thinking-partner` skill is one entry
(`builtin/thinking-partner`); its `references/` provide the full 150+-model
catalog via progressive disclosure.

## Using it with Ling-RL

Mounted as a git submodule; the skill-hint teacher's loader scans it as the
`builtin/` layer (operator libraries live in a sibling `user/` layer). See
Ling-RL `docs/skill-bank.md`.
