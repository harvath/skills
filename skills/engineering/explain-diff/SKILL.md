---
name: explain-diff
description: Produce a rich explanation of a code change — background, intuition, code walkthrough, and an interactive quiz — as a self-contained HTML page or a Notion page. Use when the user asks you to explain a diff, branch, PR, or commit range in depth.
---

# Explain Diff

Teach a reader how a code change works. Long-form, diagram-heavy, with a quiz at the end so they can check they actually understood it.

Adapted from [Geoffrey Litt's explain-diff gist](https://gist.github.com/geoffreylitt/a29df1b5f9865506e8952488eac3d524).

## Pick the output format first

| User asks for | Read |
| --- | --- |
| HTML, a file, "a page I can open", or says nothing | `html.md` |
| Notion, "put it in Notion", a shareable doc | `notion.md` |

Default to HTML. Notion needs the Notion MCP tools available — if they aren't, say so and offer HTML instead.

Everything below applies to both.

## Phase 1 — Establish the change

Identify what you're explaining: working tree diff, `main..HEAD`, a PR, a commit range, or files the user named. If it's ambiguous, pick the most likely target, say so, and state the assumption in the output.

## Phase 2 — Explore before you explain

Read past the diff. Trace callers, tests, config, data models, and docs until you can describe the **old path and the new path end to end**, not a file-by-file edit list. Prefer checked-in examples and tests over speculation.

Use the project's domain glossary (`CONTEXT.md`) for vocabulary, and check ADRs touching this area — the change may have a recorded rationale.

## Phase 3 — Build the narrative

Before writing anything, settle on:

- the problem or constraint that motivated the change
- how the old system behaved
- the smallest useful mental model of the new behavior
- how the implementation realizes that model
- edge cases, trade-offs, observable consequences

## Phase 4 — Structure

Title, one-paragraph summary, table of contents, then four sections in this order.

**Background.** Only the system needed for this change. Start with a beginner-friendly mental model, clearly marked skippable, then narrow to the exact components, contracts, and prior behavior involved.

**Intuition.** The core idea before implementation detail. Concrete toy inputs and outputs. Show old vs new side by side when the comparison is what makes it click.

**Code.** Walk through the changes in conceptual groups, ordered by execution or dependency flow — not alphabetical file order. Cite `file:line` where useful. Don't dump the diff.

**Quiz.** Exactly five multiple-choice questions. See the rules below.

Write with the clarity and flow of Martin Kleppmann — engaging, classic style, smooth transitions between sections. Explain jargon on first use. Use callouts for definitions, invariants, edge cases, and practical consequences.

Never claim behavior the source doesn't support. Distinguish what you observed from what you're inferring.

## Diagrams

Pick a **small set of reusable diagram families** and use them throughout, rather than one-off ornamental graphics. The useful ones:

- flow diagrams for requests, data, or control flow
- before/after panels for changed behavior
- labeled component cards for system boundaries
- a simplified mock of the app UI, for UI changes
- compact tables for mappings, invariants, and toy data

Never use ASCII diagrams. Label the arrows. **Always include example data** when a diagram describes data movement. Add a caption so the point survives without visual inspection.

## Quiz rules

Quiz design is part of the explanation, not decoration. Aim for medium difficulty: hard enough that you must understand the substance of the change to answer, but not gotchas.

Inspect all five questions **as a set** before emitting:

- **Vary the position of the correct answer.** Don't leave it in a fixed slot across the five.
- **Balance correct-answer positions** as evenly as possible.
- **Keep options comparable** in length, grammar, specificity, and hedging. The correct answer must not be the longest or the most technically precise one — that's the single most common tell. Shorten it or enrich the distractors.
- **Every distractor is a real misunderstanding** someone could hold about this change. No joke answers, no "all of the above", no trivia unanswerable from the page.
- **Ask about behavior, causality, contracts, edge cases, or trade-offs** — not phrases copied verbatim from the prose.
- **Explain both directions.** Say why the right answer is right, and name the misconception behind each distractor when it's instructive.

The format file covers how to make the quiz interactive and how to avoid leaking the answer in that medium.
