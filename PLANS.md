# Cross-Project Governance-First ExecPlan Skeleton

This ExecPlan is a living document. The sections `Progress`,
`Surprises & Discoveries`, `Decision Log`, and
`Outcomes & Retrospective` must be kept up to date as work proceeds.

Use this file as a reusable skeleton across repositories. At project
start, replace placeholder values and keep this file as the single source
of execution state.

## Purpose / Big Picture

Project: [PROJECT_NAME]

User problem to solve: [PROBLEM_STATEMENT]

Observable outcome after delivery: [USER_VISIBLE_OUTCOME]

Out of scope for this plan: [NON_GOALS]

This plan must enable a stateless coding agent to understand project
intent, execute one step at a time, and leave auditable evidence for
resumption by another agent or human.

## Progress

- [ ] (YYYY-MM-DD HH:MMZ) Project Intention Buildup (required first
  step): derive project-specific intent from the user prompt and current
  repository structure; for any uncertainty, ask the user before moving
  to implementation.
- [ ] (YYYY-MM-DD HH:MMZ) Lock milestone-1 scope and acceptance behavior
  from the intention record.
- [ ] (YYYY-MM-DD HH:MMZ) Implement one verified milestone with minimal
  related edits.
- [ ] (YYYY-MM-DD HH:MMZ) Capture findings, decisions, and follow-up
  steps for the next session.

## Surprises & Discoveries

Record noteworthy findings discovered during execution.

Entry template:

- Observation: [what was unexpected]
  Impact: [High | Medium | Low]
  Evidence: [command output, failing test, or concrete behavior]
  Action: [what should be done next]

## Decision Log

Record every meaningful implementation or planning decision.

Entry template:

- Decision: [what was chosen]
  Rationale: [why this path]
  Date/Author: [YYYY-MM-DD / agent-or-human]

Seed decision:

- Decision: Add `Project Intention Buildup` as a mandatory preliminary
  step before all implementation work.
  Rationale: Reusable skeletons fail when project-specific intent is
  implicit; this step makes intent explicit and auditable.
  Date/Author: 2026-04-18 / Codex

## Outcomes & Retrospective

Summarize completed outcomes at each major milestone or session end.
Compare actual results to the purpose defined above.

Entry template:

- Outcome: [what was completed]
  Verification: [PASS | FAIL with short note]
  Gap: [what remains]
  Lesson: [what to keep or change next time]

## Context and Orientation

Fill this section during `Project Intention Buildup`.

- Product or service context: [brief description]
- Primary users: [who benefits]
- Key paths/modules: [repo-relative paths]
- Runtime/toolchain baseline: [language, package manager, test runner]
- Constraints: [security, compliance, deadlines, performance]

## Plan of Work

Always start with `Project Intention Buildup` before coding.

During intention buildup, combine two inputs:

1. User prompt requirements and constraints.
2. Existing repository structure, manifests, and implemented behavior.

If any high-impact requirement remains uncertain after repository
inspection, ask the user directly and wait for clarification before
proceeding.

After intent is locked, execute exactly one unchecked `Progress` item,
verify it, and then update `Progress`, `Decision Log`, and
`Surprises & Discoveries` as needed.

## Concrete Steps

Run commands from repository root `[REPO_ROOT_PATH]`.

1. Project Intention Buildup.
   - Read the latest user prompt.
   - Inspect repository structure and existing implementation.
   - Fill placeholders in `Purpose / Big Picture`,
     `Context and Orientation`, and `Interfaces and Dependencies`.
   - List unresolved assumptions.
   - Ask user about unresolved, high-impact unknowns.
2. Convert clarified intent into one concrete unchecked `Progress` item.
3. Execute only that item with minimal related edits.
4. Run verification commands from `Validation and Acceptance`.
5. Record evidence and keep next step clearly visible in `Progress`.

## Validation and Acceptance

Define project-specific validation during intention buildup.

Required validation blocks:

- Structural/documentation checks: [COMMAND_OR_MANUAL_CHECK]
- Automated tests: [TEST_COMMAND]
- Scenario check: [manual behavior to observe]

Acceptance standard:

- The completed step changes behavior or evidence in a way a human can
  verify.
- Verification result is recorded with PASS or FAIL.
- No previously passing checks regress.

## Idempotence and Recovery

Plan steps must be safe to re-run.

- Re-running a completed documentation step should append evidence, not
  corrupt historical state.
- If interrupted, split partially completed work into done and remaining
  `Progress` items.
- If verification tooling is unavailable, record the limitation, perform
  manual checks, and create a follow-up item to restore automation.

## Artifacts and Notes

Use these templates for every step.

Session summary template:

- Step completed: [step name]
- Verification: [PASS / FAIL - brief note]
- Next step: [next unchecked item]
- Blockers: [none | description]

Project intention record template:

- Goal: [one-sentence mission]
- Success criteria: [observable outputs]
- In scope: [boundaries]
- Out of scope: [boundaries]
- Known risks: [top risks]
- Open questions for user: [must-answer uncertainties]

## Interfaces and Dependencies

Documentation contract (cross-project):

- `PLANS.md` is the source of truth for execution state.
- `AGENTS.md` is execution policy and must be consistent with
  `PLANS.md`.
- `README.md` is the operator entrypoint.

Project contract (fill during intention buildup):

- Public interfaces affected: [API/CLI/schema/module names]
- Backward compatibility policy: [required behavior]
- Dependency policy: [allowed additions and approval rules]

### Plan Revision Notes (append-only)

- 2026-04-18: Converted repository-specific plan into a cross-project
  reusable skeleton with placeholders and templates.
  Reason: Enable reuse across repositories while preserving ExecPlan
  rigor.
- 2026-04-18: Added mandatory `Project Intention Buildup` preliminary
  step with explicit user-clarification gate for uncertain requirements.
  Reason: Ensure project-specific intent is derived explicitly before
  implementation.
