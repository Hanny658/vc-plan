# Governance-First ExecPlan for vc-plan

This ExecPlan is a living document. The sections `Progress`,
`Surprises & Discoveries`, `Decision Log`, and
`Outcomes & Retrospective` must be kept up to date as work proceeds.

This repository uses [PLANS.md](./PLANS.md) as the source of truth and
follows the OpenAI ExecPlan methodology in the Codex cookbook article on
multi-hour problem solving.

## Purpose / Big Picture

This repository standardizes how AI coding agents and humans coordinate
long-running implementation work. After this refactor, a stateless agent
can enter the repo, read this file, identify exactly one next actionable
step, execute that step with verification, and leave durable evidence for
the next contributor.

The user-visible outcome is deterministic handoff quality: no hidden
context, no ambiguous "current status" interpretation, and no skipped
verification. The repository remains governance-first in this milestone;
runtime features in `src/` and `tests/` are intentionally out of scope.

## Progress

- [x] (2026-04-18 00:00Z) Created initial repository scaffolding and
  first-pass `README.md`, `PLANS.md`, and `AGENTS.md`.
- [x] (2026-04-18 00:00Z) Replaced status-table-driven planning with an
  ExecPlan-first structure where checkbox progress is authoritative.
- [x] (2026-04-18 00:00Z) Aligned `AGENTS.md` startup protocol to read
  plan sections, execute one unchecked step, verify, and update evidence.
- [x] (2026-04-18 00:00Z) Upgraded `README.md` into an operator guide
  that points to the living spec and execution policy.
- [x] (2026-04-18 00:00Z) Validated documents with
  `npx markdownlint-cli "**/*.md"` and resolved lint findings.
- [ ] Start Phase 2 by adding a minimal demo application and mapping it
  to this ExecPlan workflow.

## Surprises & Discoveries

- Observation: Agents follow small, atomic steps more reliably than broad
  phase descriptions.
  Evidence: Earlier plans with mixed prose and long checklists increased
  ambiguity when selecting the next task.

- Observation: Shared state is more robust when progress lives in one
  checkbox list with timestamps.
  Evidence: Status tables and separate progress bars can drift from real
  execution state.

- Observation: Verification instructions are dependable when they are
  executable commands with fallback guidance.
  Evidence: Command-based acceptance criteria reduce interpretation
  variance between sessions.

## Decision Log

- Decision: Use `Progress` checkboxes with timestamps as the only
  execution-state authority.
  Rationale: A stateless agent must identify the next step deterministically
  without reconciling multiple status representations.
  Date/Author: 2026-04-18 / Codex

- Decision: Keep this milestone governance-only and avoid runtime
  implementation work.
  Rationale: The priority is reproducible planning and handoff behavior
  before feature delivery.
  Date/Author: 2026-04-18 / Codex

- Decision: Preserve strict constraints from legacy instructions while
  rewriting them as execution-facing policy.
  Rationale: Safety and scope control are already valuable and should
  remain stable during structural refactor.
  Date/Author: 2026-04-18 / Codex

## Outcomes & Retrospective

This milestone established an ExecPlan-first contract for repository
governance. The planning surface now prioritizes explicit intent,
executable steps, deterministic verification, and resumable evidence.

What remains is operational proof through ongoing work: complete the
pending markdown validation item, then run Phase 2 work using this
process to confirm the governance model scales to runtime tasks.

## Context and Orientation

The repository currently contains three governance artifacts:

- `PLANS.md`: canonical living specification and execution state.
- `AGENTS.md`: policy file defining how agents must consume and update
  `PLANS.md`.
- `README.md`: operator entrypoint for humans and agents.

No production runtime modules have been introduced yet. Future work is
expected under `src/` and `tests/`, but this milestone intentionally
does not modify those paths.

## Plan of Work

The governance refactor proceeds by making `PLANS.md` self-contained and
outcome-oriented, then updating `AGENTS.md` so agent behavior is derived
from this contract. Finally, `README.md` is rewritten as a concise
operator guide that makes onboarding trivial for new contributors.

All changes are documentation-only and additive in purpose. Any future
structural change to this plan must be recorded as a revision note at the
end of this file with date, change description, and rationale.

## Concrete Steps

Run commands from repository root:
`c:\Users\hanny\Desktop\MyProjectSpace\vc-plan`.

1. Rebuild `PLANS.md` with required top-level sections and migrate status
   semantics to timestamped progress checkboxes.
2. Update `AGENTS.md` so startup and completion procedures consume and
   update the living plan contract.
3. Rewrite `README.md` into an operator guide pointing to `PLANS.md` and
   `AGENTS.md`.
4. Run markdown lint when available:
   `npx markdownlint-cli "**/*.md"`
5. If lint is unavailable, manually verify heading structure, link
   correctness, and checklist semantics, then record verification in the
   session summary and evidence log.

## Validation and Acceptance

Acceptance for this milestone is behavioral and documentation-driven:

- Fresh-start simulation: a new agent can read `README.md`, then
  `PLANS.md`, and identify exactly one next unchecked `Progress` item.
- Resume simulation: after a partial session, another agent can continue
  from `Progress`, `Decision Log`, and revision notes.
- Discovery simulation: when new information appears, the agent records it
  in `Surprises & Discoveries` with evidence and updates `Decision Log`
  if course changes.
- Constraint regression: `AGENTS.md` still enforces one-step scope,
  mandatory verification, no unrelated edits, no direct push to `main`,
  and no dependencies without finding and approval.

Verification command for this repository:

- `npx markdownlint-cli "**/*.md"`

Expected result:

- Lint passes, or lint is unavailable and manual verification is recorded
  with rationale and no structural defects.

## Idempotence and Recovery

These documentation steps are idempotent. Re-running the workflow should
only append new evidence or revision notes, not corrupt state.

If an edit is interrupted, restore coherent Markdown first, then update
`Progress` to reflect exact completion status using separate done and
remaining items. Never infer completion without verification evidence.

If command-based verification fails due to missing tooling, do not install
new dependencies automatically. Record the limitation, do manual
verification, and add a follow-up unchecked item for toolchain enablement.

## Artifacts and Notes

Use this standard session summary for every completed step (commit
message, PR description, or equivalent trace location):

Session summary template:

- Step completed: [step name]
- Verification: [PASS / FAIL - brief note]
- Next step: [next unchecked item]
- Blockers: [none | description]

Change evidence should remain concise and auditable. Preferred evidence
includes command output snippets, checklist state transitions, and
references to updated policy text.

## Interfaces and Dependencies

Documentation interface contract:

- `PLANS.md` is the source of truth for execution state.
- `AGENTS.md` is execution policy and must be consistent with `PLANS.md`.
- `README.md` is the operator entrypoint and must point to both files.

Repository behavior contract:

- No runtime API or type changes are part of this governance milestone.
- New dependencies are forbidden unless explicitly logged and approved.
- Verification is mandatory for every completed step.

### Plan Revision Notes (append-only)

- 2026-04-18: Replaced phase-table format with an ExecPlan-first living
  spec and removed `Current Status` table dependency.
  Reason: Establish deterministic, stateless execution based on one
  authoritative progress list.
