# AGENTS.md

> Instructions for AI coding agents (Codex, Claude Code, and similar) working in this repository.  
> Read this file **at the start of every session** before taking any action.

---

## 🤖 Agent Identity & Scope

You are an AI coding agent assisting with the **vc-plan** project.  
Your primary responsibility is to advance the implementation described in [`PLANS.md`](./PLANS.md)  
one phase at a time, in small, verifiable steps.

---

## 📋 Session Startup Checklist

Before writing any code or making any changes, complete the following:

1. **Read `PLANS.md`** — identify the current phase and the next unchecked step.
2. **Read `AGENTS.md`** (this file) — confirm you understand the constraints and conventions.
3. **Check the `Current Status` table** in `PLANS.md` — note any areas marked 🔄 or ⬜.
4. **Summarise your intended action** in one sentence before proceeding.
5. **Confirm scope** — only work on the single next unchecked step unless explicitly told otherwise.

---

## 🛠 Working Conventions

### General

- **One step at a time.** Complete and verify one checklist item before moving to the next.
- **Small commits.** Each commit should correspond to exactly one logical change.
- **No unrelated changes.** Do not refactor, rename, or clean up code that is not part of the current step.
- **Preserve existing behaviour.** All previously passing tests must still pass after your change.

### Files

| File         | Purpose                                     | Who updates it            |
|--------------|---------------------------------------------|---------------------------|
| `PLANS.md`   | Project plan, status, findings, progress    | Agent **and** human       |
| `AGENTS.md`  | Agent instructions and conventions          | Human (primary), Agent OK |
| `README.md`  | Public-facing project description           | Human                     |
| `src/`       | Application source code (Phase 2+)          | Agent                     |
| `tests/`     | Automated tests (Phase 2+)                  | Agent                     |

### Updating `PLANS.md` after each step

After completing a step, the agent **must**:

1. Mark the completed checklist item with `[x]`.
2. Update the `Current Status` table (change status emoji as appropriate).
3. Append a row to the `Changelog` table with today's date and a short description.
4. Recalculate and update the progress bar percentages.

---

## ✅ Verification Protocol

Every change must be verified before it is considered done.

### Step-level verification

1. Run the verification command listed in the `Verification` section of `PLANS.md`.
2. If no command exists yet, manually inspect the artefact and confirm it meets the acceptance criteria.
3. Record the outcome in the session summary (see below).

### Session summary (append to PR description or commit message)

```
## Session Summary — <date>

**Step completed:** <step name>
**Verification:** <PASS / FAIL — brief note>
**Next step:** <next unchecked item>
**Blockers:** <none | description>
```

---

## 🔍 Findings Protocol

When you discover something noteworthy (a limitation, a better approach, an unexpected behaviour):

1. Add a row to the `Findings` table in `PLANS.md`.
2. Assign it an impact level: **High / Medium / Low**.
3. Propose a concrete action item.

---

## 🚫 Constraints

- **Do not** delete or overwrite `PLANS.md` or `AGENTS.md` without explicit human approval.
- **Do not** skip verification steps, even if the change seems trivial.
- **Do not** add new dependencies without listing them in a finding and getting approval.
- **Do not** push directly to `main` — all changes must go through a pull request.
- **Do not** expose secrets, credentials, or personally identifiable information in any file.

---

## 🔄 Handoff Instructions

If you cannot complete a step in one session, leave the repository in a clean state:

1. Commit any partial work to a feature branch with a clear message prefixed `WIP:`.
2. Update the `Current Status` table with the partial state.
3. Add a `Blockers` entry to the `Findings` table describing what is unfinished and why.
4. Leave a `<!-- AGENT RESUME POINT -->` comment in the relevant source file so the next agent can find it quickly.

---

## 📚 Reference

- [OpenAI Cookbook: Codex Exec Plans](https://developers.openai.com/cookbook/articles/codex_exec_plans)
- [Anthropic: Claude Code documentation](https://docs.anthropic.com/en/docs/claude-code)
- [`PLANS.md`](./PLANS.md) — the living project plan for this repository

---

*Last updated: 2026-04-18*
