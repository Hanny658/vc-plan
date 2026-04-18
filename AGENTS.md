# AGENTS.md

Instructions for AI coding agents working in this repository.
Read this file at the start of every session before taking action.

## Agent Identity and Scope

You are an AI coding agent operating under a cross-project ExecPlan
workflow.

Your primary responsibility is to execute one unchecked item at a time
from [PLANS.md](./PLANS.md), verify the result, and leave auditable
state for the next contributor.

`PLANS.md` is the source of truth for execution state. If this file
conflicts with `PLANS.md`, follow `PLANS.md` and record the mismatch in
`Decision Log`.

## Session Startup Protocol

Before writing code or editing files:

1. Read `PLANS.md` fully, focusing on `Purpose / Big Picture`,
   `Progress`, `Decision Log`, `Concrete Steps`, and
   `Validation and Acceptance`.
2. Read `AGENTS.md` fully to confirm policy constraints.
3. Execute `Project Intention Buildup` first if it is unchecked or if
   project intent is incomplete.
4. Identify exactly one next unchecked item in `Progress`.
5. Summarize intended action in one sentence.
6. Confirm scope is limited to that single unchecked item unless the
   user explicitly broadens scope.

## Project Intention Buildup Rule

`Project Intention Buildup` is mandatory before implementation work.

The agent must derive project-specific content by combining:

- user prompt requirements and constraints
- current repository structure and existing behavior

If anything important is uncertain after inspection, ask the user before
proceeding. Do not guess on high-impact unknowns.

## Working Rules

- Execute one logical step at a time.
- Keep changes minimal and directly related to the selected step.
- Do not perform unrelated refactors or cleanup.
- Preserve existing behavior and keep previously passing checks green.
- Prefer small commits aligned to one logical change.

## Completion and Evidence Protocol

After completing a step, update `PLANS.md` in the same session:

1. Mark the completed `Progress` item as checked with timestamp if not
   already present.
2. Add or update entries in `Decision Log` when choices are made.
3. Record findings in `Surprises & Discoveries` when noteworthy.
4. Ensure the next actionable item remains clearly unchecked.

For each step, include this summary block in commit message, PR
description, or equivalent trace:

Session summary template:

- Step completed: [step name]
- Verification: [PASS / FAIL - brief note]
- Next step: [next unchecked item]
- Blockers: [none | description]

## Verification Policy

Verification is mandatory for every step.

1. Run verification commands listed in `PLANS.md` when available.
2. If command-based verification is unavailable, perform manual
   verification against acceptance behavior and record the reason.
3. Never mark a step complete without verification evidence.

## Findings and Decisions Policy

When discovering limitations, better approaches, or unexpected behavior:

1. Record the observation in `Surprises & Discoveries` with evidence.
2. If approach changes, add a `Decision Log` entry with rationale.
3. Reflect scope impact by splitting or adding `Progress` items.

## Constraints

- Do not delete or overwrite `PLANS.md` or `AGENTS.md` without explicit
  user approval.
- Do not skip verification, including for trivial-looking edits.
- Do not add dependencies without recording a finding and obtaining
  approval.
- Do not push directly to `main`; use branch and PR workflow.
- Do not expose secrets, credentials, or personal data.

## Handoff Rules

If a step cannot be completed in one session:

1. Leave repository state coherent and reviewable.
2. If committing partial work, use a clear `WIP:` prefix.
3. Update `Progress` to reflect completed versus remaining work.
4. Record blockers in `Surprises & Discoveries` and `Decision Log`.
5. Leave an `AGENT RESUME POINT` comment in the most relevant file when
   helpful.

## References

- [PLANS.md](./PLANS.md) - canonical living plan and execution state
- [OpenAI Cookbook: Using PLANS.md for multi-hour problem solving]
  [execplan-doc]

Last updated: 2026-04-18

[execplan-doc]: https://developers.openai.com/cookbook/articles/codex_exec_plans
