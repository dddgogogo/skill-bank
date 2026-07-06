---
name: caveman
description: "This skill should be used when an agent's responses are dominated by narration, preamble, and restated summaries rather than content — apply a terse, information-dense output style that strips conversational filler while preserving every technical fact, file path, identifier, and code block byte-for-byte. Use for long agentic sessions, status updates, plans, and code reviews where output volume drives cost. Cuts output tokens ~60-75% with zero information loss."
tags: [coding, token-optimization, output-style, context-engineering]
license: MIT
---

# Caveman Output Mode — Terse, Lossless Agent Output

Most of an agent's output tokens are not code or facts — they are narration:
"Let me explain what I'm going to do." "Based on the code I've analyzed."
"Here's a summary of what I found." In a multi-turn session this narration is
re-read on every turn, so its cost compounds. The fix is a disciplined output
style, not a smaller model or a lossy summary.

## When to Activate

- Long agentic sessions where output volume, not reasoning, drives cost.
- Status updates, execution plans, and multi-step task narration.
- Code reviews (one line per issue: location, problem, fix).
- Any turn whose content is a handful of facts wrapped in paragraphs of prose.

Do not activate for the adjacent concern of compressing *history* rather than
*output* — see `builtin/context-engineering/context-compression` and
`builtin/coding-skill/handoff`.

## Core Method

- Short declarative sentences. Infinitive verbs. No greetings, no preamble, no
  restating the question, no "as you can see" / "in summary" scaffolding.
- Preserve **all** technical content verbatim: file paths, symbol names, CLI
  commands, numbers, error strings, and code blocks byte-for-byte. Compression
  applies to prose only, never to content.
- Prefer lists over paragraphs. One item per line. Lead each line with the
  concrete thing (path, symbol, value), then the point.
- Drop hedging and meta-commentary about your own process. State the result.

## Safety Rails — When to Drop the Style

- Code and diffs are never abbreviated or elided to save tokens.
- Revert to normal prose for anything where nuance prevents error: safety
  warnings, destructive or irreversible operations, security caveats, and
  ambiguous instructions that need a careful explanation.
- The style shrinks output tokens only. It must not suppress a fact, a caveat,
  or a step the reader needs to act correctly.

## Trade-off

Terseness reads as blunt. That is acceptable for machine-facing or expert-facing
output; for user-facing explanation where tone matters, use judgment and keep
enough prose to stay clear.

## Attribution

Distilled from the community "caveman" Claude Code skill
(github.com/mattpocock/skills; github.com/JuliusBrussee/caveman), MIT-licensed.
Body authored for this bank as a general, environment-agnostic methodology.
