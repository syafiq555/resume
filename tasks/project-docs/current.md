# Project doc set {#project-docs}

**Status:** created 04/11/2026, uncommitted.
**Owner:** the repo owner. `update-claude-docs` maintains `CLAUDE.md`; edits to `docs/` go through this doc.

> Public repo: this file is world-readable. No job-search context here.

## Quick Start {#quick-start}

- Set: `docs/PRD.md`, `docs/ARCHITECTURE.md`, `docs/ARCHITECTURE-ESSENTIALS.md`, `CLAUDE.md` (index + precedence), `AGENTS.md` (pointer).
- Frames: PRD uses the standard table shape trimmed to a one-page product; ARCHITECTURE uses arc42 trimmed to sections with an analogue.
- Protected content: `[SOURCED]` / `[INFERRED]` / `[TBD]` tags and `[TBD]` headings. Pruning passes must keep them.
- Maintenance test for essentials: is it still short enough to be read whole?

## Decisions {#decisions}

| Decision | Why |
|---|---|
| Public-repo rule leads essentials | `gh repo view` shows PUBLIC; private positioning notes already live in gitignored `CLAUDE.local.md` and must stay there |
| Honesty, verb and qualifier rules written generically | The specifics behind them are job-search context (see above) |
| No `.claude/agents/`, so no `agent-setup` run | Nothing to bootstrap |
| CSS list bullets changed from em dash to hyphen (04/11/2026) | Owner's choice; brings the rendered page in line with the no-em-dash rule |

## Open findings {#open-findings}

Recorded, not resolved; the owner decides. Mirrored in `docs/PRD.md#open-questions`.

- Angular / .NET Core appear unqualified in the Frontend / Backend skill rows.
- 2-page length is observed, not a written target.
