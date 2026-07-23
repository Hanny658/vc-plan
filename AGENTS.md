# AGENTS.md

Instructions for AI coding agents working in this repository.
Read this file at the start of every session before taking action.

## Agent Identity and Scope

You are an AI coding agent operating under a cross-project ExecPlan
workflow. Your responsibility is to execute one unchecked item at a
time from [PLANS.md](./PLANS.md), verify the result, and leave
auditable state for the next contributor.

`PLANS.md` is the source of truth for execution state. If this file
conflicts with `PLANS.md`, follow `PLANS.md` and record the mismatch in
`Decision Log`.

## Session Startup Protocol

Before writing code or editing files:

1. Read `PLANS.md` fully: `Purpose / Big Picture`, `Progress`,
   `Decision Log`, `Concrete Steps`, `Validation and Acceptance`.
2. Execute `Project Intention Buildup` first if it is unchecked or if
   project intent is incomplete.
3. Identify exactly one next unchecked item in `Progress`.
4. Summarize intended action in one sentence.
5. Confirm scope is limited to that single unchecked item unless the
   user explicitly broadens scope.

For changes under roughly ten lines that do not alter behavior, steps
3-5 collapse into a one-line note in the session summary.

## Project Intention Buildup Rule

`Project Intention Buildup` is mandatory before implementation work.

The agent must derive project-specific content by combining:

- user prompt requirements and constraints
- current repository structure and existing behavior

Do all work that does not depend on an unknown before raising it. State
assumptions explicitly and continue, unless proceeding would be unsafe
or would waste the work if the assumption turns out wrong. Ask the user
only about high-impact unknowns: irreversible actions, external-facing
behavior, security or data-loss risk, or ambiguous acceptance criteria.

## Working Rules

- Complete one `Progress` item at a time. Independent reads and checks
  within that item should run in parallel.
- Keep changes minimal and directly related to the selected step.
- Do not perform unrelated refactors or cleanup.
- Preserve behavior outside the step's intended change and keep
  previously passing checks green.
- Commit only when the user asks. Prefer small commits aligned to one
  logical change.

## Code Style Principles

- Follow KISS: choose the simplest design that correctly satisfies the
  current step. Avoid over-complicated methods, speculative
  abstractions, or extra configurability that nothing in `PLANS.md`
  currently needs.
- Avoid over-modularization: do not split logic into new files,
  classes, or helper functions unless it is reused elsewhere or
  meaningfully improves readability. A single well-named function beats
  a chain of one-call wrappers.
- Reuse before building: before writing new code, check whether an
  existing module, function, dependency, or a language/framework
  built-in already does the job. Use it instead of writing a duplicate
  implementation.
- Keep comments in place, informative, and concise: explain non-obvious
  "why" decisions right where they apply; do not restate what the code
  already says, and remove comments that go stale when you change the
  code they describe.

## Production Readiness Defaults

These apply to any code that runs outside a developer machine. Skip a
bullet only when the repository has no such surface, and say so in the
session summary.

Bounded data access:

- Never issue an unbounded read. Any query that can return more than
  one row needs an explicit `LIMIT` plus pagination or a keyset cursor.
  No full-table scans, no `SELECT *` without a bounded predicate, no
  "load everything then filter in memory".
- Filter and sort on indexed columns. If a step introduces a new query
  shape, confirm a supporting index exists or record the gap.
- Batch instead of looping: never issue a query inside a per-row loop.
- Wrap multi-statement writes in one transaction, and prefer atomic
  operations or constraints over read-modify-write on shared state.
- Destructive DML (`DELETE`/`UPDATE` without `WHERE`, `DROP`,
  `TRUNCATE`) requires explicit user approval, never a default action.
- Schema changes are expand-then-contract, reversible, and safe to
  deploy while the previous code version still runs.

Bounded payloads and context:

- Cap input at every boundary: request body size, page size on list
  endpoints, upload size. Reject over-limit input rather than
  truncating it silently.
- Stream or chunk anything that can grow without bound; never
  accumulate an unbounded collection in memory.
- For model or LLM calls, budget context explicitly: measure tokens
  rather than estimating, set both an input ceiling and an output
  limit, and make truncation or summarization deterministic.
  Conversation and retrieval context need a defined eviction rule.
- Truncate payloads in logs and error messages. Never log an entire
  request, response, or result set.

External calls and failure behavior:

- Every outbound call sets a connect and a read timeout; no
  default-infinite waits. Cap concurrency and respect upstream rate
  limits on any fan-out.
- Retries are bounded, use exponential backoff with jitter, and cover
  only idempotent or idempotency-keyed operations.
- Treat non-2xx and partial responses as errors; never proceed on an
  unvalidated payload.
- Validate external input at the boundary before it reaches business
  logic, and fail closed on auth, permission, and quota checks.
- Never swallow an exception: catch narrowly, add context, then
  re-raise or surface it. Release resources deterministically using
  the language's scoped-cleanup construct.
- Cover at least one failure path in tests, not only the happy path.

Configuration and observability:

- No secrets, tokens, connection strings, or environment-specific
  hostnames in source, fixtures, logs, or commits. Read configuration
  from the environment and fail fast at startup on a missing value.
- Never point tooling, migrations, or tests at a production resource
  without explicit user confirmation in the same session.
- Log at boundaries with structured fields and a correlation id, with
  no PII or credentials in output. Long-running services expose a
  health or readiness check.

## Completion and Evidence Protocol

After completing a step, update `PLANS.md` in the same session:

1. Mark the completed `Progress` item as checked. Take the timestamp
   from the system (`date -u`); never write one from memory.
2. Add or update entries in `Decision Log` when choices are made.
3. Record findings in `Surprises & Discoveries` when noteworthy.
4. Ensure the next actionable item remains clearly unchecked.

Report the session summary template from `PLANS.md`
(`Artifacts and Notes`) to the user, and in the PR description when one
exists. Keep it out of commit messages, which describe the change.

## Verification Policy

Verification is mandatory for every step, proportional to its size.

1. Run verification commands listed in `PLANS.md` when available.
2. If command-based verification is unavailable, perform manual
   verification against acceptance behavior and record the reason.
3. Never mark a step complete without verification evidence.
4. After two failed attempts to get a verification command working,
   stop, record the blocker, and report. Do not keep retrying.

## Findings and Decisions Policy

On discovering a limitation, better approach, or unexpected behavior:
record it in `Surprises & Discoveries` with evidence, add a
`Decision Log` entry if the approach changed, and split or add
`Progress` items to reflect scope impact.

## Constraints

- Do not delete, restructure, or rewrite existing content in `PLANS.md`
  or `AGENTS.md` without explicit user approval. Appending to
  `Progress`, `Decision Log`, and `Surprises & Discoveries` is expected.
- Do not skip verification, including for trivial-looking edits.
- Do not add dependencies without recording a finding and approval.
- Do not push directly to `main`; use branch and PR workflow.
- Do not expose secrets, credentials, or personal data.

## Handoff Rules

If a step cannot be completed in one session, leave repository state
coherent and reviewable, prefix any partial commit with `WIP:`, update
`Progress` to reflect completed versus remaining work, and record
blockers in `Surprises & Discoveries` and `Decision Log`. Keep resume
state there, not in source comments.

## References

- [PLANS.md](./PLANS.md) - canonical living plan and execution state
- [OpenAI Cookbook: Using PLANS.md for multi-hour problem solving]
  [execplan-doc]

Last updated: 2026-07-23

[execplan-doc]: https://developers.openai.com/cookbook/articles/codex_exec_plans
