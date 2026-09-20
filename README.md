# Ledgerly AI Employees — code extract

This repo is a **read-only extract** of the "Ledgerly AI" subsystem from the
main `ledgerly-final` monorepo: the autonomous AI employees (Kato, Safi, Nia,
Tuma, Jabali, Maya and friends), the incident/engineering workflow they run
on, and the chat/admin console around them.

It exists so a reviewer can read this one system without checking out the
whole finance monorepo. **It does not build or run standalone** — it's
missing the finance core, the HTTP framework, other feature modules, and the
frontend shell those files import from. Treat it as a code-reading slice, not
a deployable app.

## Where things live

- `node-backend/src/features/ledgerly-ai/` — the backend feature: provider
  routing/execution (Codex CLI + Claude Code CLI, run in locked-down Docker
  containers), the incident workflow state machine, named-employee registry,
  tool gateway, chat/memory, custom agents, git/deploy automation, policy and
  security controls.
- `modules/ledgerly-ai/frontend/` — the chat/admin console UI (React).
- `ledgerly-ai/docs/` — architecture, operations, and backup/recovery docs.
- `ledgerly-ai/workers/` — the `Dockerfile`s for the Codex and Claude Code
  worker images the incident workflow spawns.
- `node-backend/migrations/0103…0123_ledgerly_ai_*.sql` — the schema
  (`lai_*` tables), in order.
- `node-backend/test/ledgerly-ai-*.test.ts` — the test suite for this
  subsystem.
- `.github/workflows/ledgerly-ai-ci.yml` — its CI workflow.
- `node-backend/.env.example` — the `LEDGERLY_AI_*` environment variables it
  reads (trimmed from the monorepo's full example file; no real values).

## Start here

1. `ledgerly-ai/README.md` and `ledgerly-ai/docs/ARCHITECTURE.md` for the
   big picture — what the employees are, how a task or incident flows
   through investigation → implementation → QA → git → deployment.
2. `node-backend/src/features/ledgerly-ai/index.ts` — how the feature wires
   into the backend (routes, queue jobs, schedules).
3. `node-backend/src/features/ledgerly-ai/incidents/service.ts` — the
   engineering incident workflow itself.
4. `node-backend/src/features/ledgerly-ai/providers/` — how a provider (the
   actual CLI-based AI worker) gets ranked, sandboxed and executed.
5. `ledgerly-ai/docs/OPERATIONS.md` — day-to-day operational notes.

Extracted from `ledgerly-final` on 2026-09-20; not synced automatically —
treat it as a snapshot, not a mirror.
