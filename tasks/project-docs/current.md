# Project doc set {#project-docs}

**Status:** ✅ Doc set and seven project agents in place; no open questions.
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
| Seven project agents added under `.claude/agents/` (04/11/2026) | They bootstrap from `CLAUDE.md` and the three `docs/` files and cite PRD `Out of scope` / `Open questions` and ARCHITECTURE `Building blocks` / `Runtime view` / `Risks` by heading. Renaming one of those headings means re-running `agent-setup` |
| `.claude/agent-memory/` gitignored | Agents read `CLAUDE.local.md`, so their notes can carry private context into a public repo |
| CSS list bullets: hyphen, in `--ink-muted` grey (04/11/2026) | Owner's choices. The em dash broke the no-em-dash rule and reached the ATS text; the first hyphen at `--border` grey nearly vanished in print |
| Page target: 2 A4 pages preferred, 3 acceptable (04/11/2026) | Owner's decision; recorded in PRD metrics and acceptance, essentials print-check, and the reviewer agents' severity |
| Skill rows kept as they are (04/11/2026) | Owner's decision after a review question; specifics in the gitignored `CLAUDE.local.md`. Not a finding to re-raise |
| Docs don't cite commits by hash | Some older commit subjects carry job-search context, and the repo is public |

## Gotchas {#gotchas}

| Symptom | Cause | Fix |
|---|---|---|
| Page count is null or 0 | `mdls` doesn't index `/tmp`; Chrome's PDF writes `/Type /Page` in a form a simple grep misses | `grep -ao '/Count [0-9]*' <pdf> \| head -1` |
| Em dash check passes but a CSS bullet still renders one | CSS writes it as the escape `"\2014"`, which the byte-form grep can't see | Also run `grep -c '\\2014' css/*.css` |
| A doc that documents the em dash check fails it | The command quotes the character itself | Write it as `printf '\342\200\224'` |
| Headless screenshot of the page is blank | Captured mid fade-in from `screen.css` | Print to PDF and read that |

## Next Steps {#next-steps}

None open. New questions go in `docs/PRD.md#open-questions`, which is the only copy.
