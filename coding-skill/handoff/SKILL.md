---
name: handoff
description: "This skill should be used when a context window is filling up (roughly 60-70%), before starting complex multi-session work, or when switching from planning to implementation — instead of a lossy compaction, produce a structured handoff document that captures decisions, constraints, exact identifiers, git state, and recommended next steps so a fresh session (or a different agent) resumes with no loss of critical context."
tags: [coding, context-engineering, session-continuity, handoff]
license: MIT
---

# Structured Session Handoff — a Lossless Alternative to Compaction

Built-in context compaction is lossy: specific variable names, subtle design
decisions, and boundary constraints frequently do not survive. Late in a long
session the agent then "forgets" what it decided and re-derives it, wasting far
more tokens than the compaction saved. A structured handoff replaces a lossy
summary with a deliberate, checklist-driven export of session state.

## When to Use

- The context window is ~60-70% full and quality is starting to degrade.
- Before beginning complex, multi-session work.
- When switching phases — e.g. from planning/design to implementation.
- When handing the work to another agent or tool (parallel work, or an
  independent adversarial review of the same state).

## What the Handoff Captures

- **Decisions and constraints, not a chat log.** Mine the full conversation and
  extract *why* things are the way they are — the load-bearing choices and the
  boundaries that must not be violated.
- **Exact identifiers, verbatim.** Variable/function/file names, thresholds,
  config keys, and boundary conditions copied exactly — these are precisely what
  lossy compaction drops.
- **Git state.** Current branch, what is committed vs. pending, and the key
  diffs in flight.
- **Reference, do not copy.** Link to existing artifacts (ADR, plan, PRD, issue)
  instead of duplicating their content into the handoff.
- **Redact secrets.** Strip API keys, tokens, and credentials from the export.
- **Recommended next steps / skills.** Name what the next session should do
  first and which methods or skills it should invoke.

## Method

1. Write the handoff as structured markdown with fixed sections (Intent, State,
   Decisions, Constraints, Files touched, Git, Open questions, Next steps). The
   sections act as checklists that force preservation — a blank section is a
   visible signal that something was lost.
2. Populate each section from the actual conversation, not from memory of it.
3. Keep identifiers and constraints verbatim; summarize only prose.
4. Start the next session by reading the handoff before touching code.

## Relation to Adjacent Skills

- For *compressing running history* mid-session (rather than exporting state at a
  boundary), see `builtin/context-engineering/context-compression`.
- For keeping *output* terse turn-to-turn, see `builtin/coding-skill/caveman`.

## Attribution

Distilled from the community "handoff" Claude Code skill
(github.com/mattpocock/skills), MIT-licensed. Body authored for this bank as a
general, environment-agnostic methodology.
