---
name: karpathy-agent-discipline
description: "This skill should be used when a coding agent tends to make silent assumptions, over-engineer, or modify unrelated code as a side effect — apply four behavioral constraints (think before coding, prefer simplicity, make surgical edits, and drive execution from verifiable success criteria) so that changes stay minimal, assumptions are surfaced, and every edited line traces back to the request."
tags: [coding, agent-behavior, discipline, code-quality]
license: MIT
---

# Four Behavioral Constraints for Coding Agents

Three recurring failure modes of coding agents, per Andrej Karpathy:

1. Silently making a wrong assumption.
2. Over-complicating the code.
3. Modifying unrelated things as a side effect.

Four constraints counter them. They bias toward caution over speed; for trivial
tasks, use judgment.

## The Four Constraints

1. **Think before coding.** State assumptions explicitly. If more than one
   interpretation of the request exists, surface them instead of silently
   picking one. When something is genuinely unclear, stop and ask rather than
   guess.

2. **Simple first.** Do not build beyond what was asked. Do not create an
   abstraction for a single use. Do not write error handling for impossible
   cases. If the output is 200 lines where 50 would do, rewrite it smaller.

3. **Surgical edits.** Touch only what the request requires. Do not "improve"
   adjacent code. Do not refactor what is not broken. Every changed line should
   be traceable to the user's request; if you cannot justify a change by the
   request, revert it.

4. **Goal-driven execution.** Turn the task into a verifiable success criterion
   before starting. "Fix the bug" becomes "write a test that reproduces it, then
   make it pass." Weak criteria force constant clarification; strong criteria let
   the agent run independently and know when it is done.

## When to Apply

- General-purpose default for any code-editing task.
- Especially when working in a large or unfamiliar codebase where side-effect
  edits and speculative abstractions are most costly.
- When a task is under-specified — constraint 1 (surface assumptions) and
  constraint 4 (define success) are the highest-leverage moves.

## Trade-off

These guidelines favor caution and minimalism over raw speed. On throwaway or
trivial tasks the ceremony is not worth it — apply judgment about when the
discipline pays for itself.

## Attribution

Distilled from the "andrej-karpathy-skills" CLAUDE.md discipline template
(github.com/multica-ai/andrej-karpathy-skills;
github.com/forrestchang/andrej-karpathy-skills), based on guidance from Andrej
Karpathy. Body authored for this bank as a general, environment-agnostic
methodology.
