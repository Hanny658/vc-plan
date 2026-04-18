# vc-plan

`vc-plan` is a governance-first template for AI coding workflows based
on a living `PLANS.md` execution specification.

## What This Repository Is

This repository demonstrates how to run multi-step engineering work with
stateless agents by using:

- `PLANS.md` as the canonical execution state and design document.
- `AGENTS.md` as the operational policy that governs agent behavior.

The current milestone focuses on planning governance, not runtime
feature implementation.

## How an Agent Should Start

1. Read [PLANS.md](./PLANS.md) end-to-end.
2. Read [AGENTS.md](./AGENTS.md) end-to-end.
3. Select exactly one next unchecked item in the `Progress` section of
   `PLANS.md`.
4. Execute that item, run verification, and update plan evidence before
   moving on.

## Execution Rules Location

- Living specification and execution state: [PLANS.md](./PLANS.md)
- Agent policy and safety constraints: [AGENTS.md](./AGENTS.md)
- Source methodology: [OpenAI Cookbook article][execplan-doc]

## Verification Baseline

Preferred command when available:

- `npx markdownlint-cli "**/*.md"`

If unavailable, perform manual structural verification and record the
result in the session summary and plan evidence.

[execplan-doc]: https://developers.openai.com/cookbook/articles/codex_exec_plans
