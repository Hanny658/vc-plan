# Cross-Project ExecPlan Skeleton

This repository provides a reusable Markdown skeleton for running
coding-agent workflows across projects.

## What You Get

- `PLANS.md`: a living ExecPlan with state, decisions, and validation.
- `AGENTS.md`: execution policy that agents must follow.

The core addition in this version is a mandatory preliminary step:
`Project Intention Buildup`.

## Project Intention Buildup

Before implementation, the agent must:

1. Extract intent from the user prompt.
2. Infer project context from the current repository structure.
3. Fill project-specific sections in `PLANS.md`.
4. Ask the user whenever high-impact details are uncertain.

This gate prevents silent assumptions and improves cross-session
reliability.

## How To Reuse In Another Repository

1. Copy `PLANS.md` and `AGENTS.md` into the target repository root.
2. Replace placeholders in `PLANS.md` during intention buildup.
3. Start execution from the first unchecked `Progress` item.
4. Keep `Progress`, `Decision Log`, and findings updated every step.

## Verification Baseline

Preferred command when available:

- `npx markdownlint-cli "**/*.md"`

If unavailable, do manual structural verification and record the result
in the session summary.

## Methodology Reference

- [OpenAI Cookbook: Using PLANS.md for multi-hour problem solving]
  [execplan-doc]

[execplan-doc]: https://developers.openai.com/cookbook/articles/codex_exec_plans
