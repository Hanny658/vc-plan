# PLANS.md

> **vc-plan** — a structured planning document for AI coding agents (Codex, Claude Code, etc.)  
> Inspired by [OpenAI Cookbook: Codex Exec Plans](https://developers.openai.com/cookbook/articles/codex_exec_plans)

---

## 🎯 Target

Build a reusable, agent-friendly planning framework (`PLANS.md` + `AGENTS.md`) that:

- Gives AI coding agents a shared, persistent source of truth about project goals and state.
- Enables reproducible, multi-step task execution with clear verification criteria.
- Captures findings and progress so that any agent (or human) can resume work at any point.

---

## 📌 Current Status

| Area              | Status      | Notes                              |
|-------------------|-------------|------------------------------------|
| Repository        | ✅ Created   | Minimal scaffold in place          |
| README.md         | ✅ Done      | High-level description written     |
| PLANS.md          | 🔄 In progress | This file                        |
| AGENTS.md         | 🔄 In progress | Agent instructions skeleton      |
| Example project   | ⬜ Pending   | Demo application to be added       |
| CI / tests        | ⬜ Pending   | Validation pipeline not yet set up |

---

## 🗂 Multi-Step Implementation

### Phase 1 — Foundation (current)

- [x] Create repository with README
- [x] Draft `PLANS.md` template (this file)
- [x] Draft `AGENTS.md` template with agent instructions

### Phase 2 — Example project

- [ ] Add a minimal demo application (e.g., a simple CLI or web app)
- [ ] Apply the `PLANS.md` / `AGENTS.md` pattern to the demo project
- [ ] Show how an agent reads these files at the start of each session

### Phase 3 — Tooling & automation

- [ ] Add a script / GitHub Action that validates `PLANS.md` structure on every PR
- [ ] Provide a cookiecutter / starter template so teams can bootstrap their own repo
- [ ] Write documentation on how to integrate with Codex and Claude Code workflows

### Phase 4 — Community & iteration

- [ ] Publish usage examples and case studies
- [ ] Gather feedback and iterate on the template format
- [ ] Tag a stable `v1.0.0` release

---

## ✅ Verification

Each phase is considered complete when **all** of the following are true:

1. **Correctness** — The artefact (file, script, workflow) exists and passes any associated automated checks.
2. **Readability** — A human reviewer can understand the purpose without additional context.
3. **Agent-consumable** — An AI coding agent can ingest the file, identify the current step, and produce a valid next action without manual intervention.
4. **No regressions** — All previously passing tests / checks still pass.

> Verification command (once CI is set up):
> ```bash
> # Lint markdown
> npx markdownlint-cli "**/*.md"
>
> # Run project tests (Phase 2+)
> npm test
> ```

---

## 🔍 Findings

| # | Finding                                                                                         | Impact   | Action                                    |
|---|-------------------------------------------------------------------------------------------------|----------|-------------------------------------------|
| 1 | AI agents perform better when the plan is split into small, atomic steps with explicit criteria | High     | Keep each step under ~50 words            |
| 2 | Agents lose context across sessions — a persistent `Current Status` table is essential          | High     | Update the table after every work session |
| 3 | Mixing prose and checklists in one file causes agents to miss checklist items                   | Medium   | Use dedicated sections for each type      |
| 4 | Verification criteria that are runnable commands reduce ambiguity significantly                 | High     | Always include a runnable verification step |
| 5 | `AGENTS.md` should be kept separate to allow per-repo customisation without touching the plan   | Medium   | Maintain two distinct files               |

---

## 📈 Progress

```
[Phase 1 ███████████░░░░░░░░░░ 55%]
[Phase 2 ░░░░░░░░░░░░░░░░░░░░░  0%]
[Phase 3 ░░░░░░░░░░░░░░░░░░░░░  0%]
[Phase 4 ░░░░░░░░░░░░░░░░░░░░░  0%]
```

### Changelog

| Date       | Author          | Change                                              |
|------------|-----------------|-----------------------------------------------------|
| 2026-04-18 | copilot (agent) | Created initial `PLANS.md` and `AGENTS.md` skeleton |

---

*Last updated: 2026-04-18*
