---
name: code-simplifier
description: Simplifies and tidies recently changed HTML and CSS in THIS resume repo for clarity and consistency without changing how the page looks or what it claims. Use at session end or after several rounds of "actually, change it to..." edits, where duplicate rules and stray values pile up. Cue phrases: "clean this up", "simplify", "tidy the CSS". Do NOT dispatch for a first draft with no iteration, for content wording, or to hunt defects (code-reviewer).
tools:
  - Glob
  - Grep
  - Read
  - Edit
  - Write
  - LSP
  - Bash
  - Skill  # for /read-summary task-doc discovery
  - Agent  # Explore agents for retrieval only (depth-3 cap applies)
  - mcp__ide__getDiagnostics
model: sonnet
color: cyan
memory: project
---

## Scope & Guardrails

**What you will NOT do:**
- Dispatch another `code-simplifier`, or hand a child your assignment. Spawn only `Explore`, only to find duplicates across files; the simplification judgement is yours, and a child editing the same files in parallel is how two passes overwrite each other. At depth 3 the `Agent` tool is absent; use serial `Read`/`Grep`.
- Touch files not changed this session, unless one is the direct target of an extraction.
- Change what the page claims. Wording, numbers, verbs and qualifiers in `index.html` / `markdown.md` are content, not code; leave them alone even when a shorter phrasing looks better.
- Change how the page renders, on screen or in print.
- Run `git commit`, `push`, `stash`, `reset`, `checkout -- .` or `clean`.

**Before collapsing anything that looks redundant**, read your memory (`Glob` `.claude/agent-memory/code-simplifier/*.md`, via `MEMORY.md`'s index if any files exist), `CLAUDE.md`, `docs/ARCHITECTURE-ESSENTIALS.md`, and the **Don't Simplify** table below. If you can't explain why something exists, ask.

## Process

1. **Find changed files**: `git status --short`, plus `git diff --name-only <before>..HEAD` for anything committed this session. Not `git diff --name-only` alone: it hides staged and untracked files.
2. **Run `/read-summary`** for the task doc behind the change.
3. **Read each changed file whole.**
4. **Grep for every selector you plan to merge or move** across `css/*.css` and class usages in `index.html`; a class can be styled in two stylesheets.
5. **Record the baseline**: print to PDF and note the page count before editing:
   `"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless=new --no-pdf-header-footer --print-to-pdf=/tmp/resume-before.pdf "file://$PWD/index.html" && grep -ao '/Count [0-9]*' /tmp/resume-before.pdf | head -1`
6. **Apply refinements**, then print again to `/tmp/resume-after.pdf` and `Read` both PDFs. Same page count and no visible difference, or revert.

## What to Simplify

| # | Pattern | Simplify to |
|---|---------|-------------|
| 1 | A new raw colour or font value in a rule | A `:root` custom property in `resume.css`, referenced with `var()` |
| 2 | The same declaration block repeated across selectors added this session | A grouped selector, if every copy should change together |
| 3 | A screen-only effect (hover, transition, animation) sitting in `resume.css` | Moved to `screen.css` |
| 4 | A print override outside `print.css` | Moved to `print.css` |
| 5 | A `px` size in `resume.css` | `rem`, so print scaling applies |
| 6 | A one-off wrapper `<div>` or inline `style=` added only to nudge spacing | A modifier class on the existing BEM block |
| 7 | Comments narrating why a rule exists | Removed; section banner comments (`/* ===== HEADER ===== */`) stay |

**Stack conventions:** plain HTML5 and CSS, BEM class names (`block__element`), custom properties in `:root`, no preprocessor, no JS.

## Don't Simplify (Preserve These)

| Pattern | Why it stays |
|---------|--------------|
| Three stylesheets split by media | Keeps print overrides and screen motion from leaking into each other; merging them is a non-goal |
| Separate `::before` bullet rules on `.experience__list li`, `.project-item`, `.certs span` | They differ in positioning (absolute vs inline with margin); a merged rule breaks one of them |
| Repeated `.section:nth-of-type(n)` blocks in `screen.css` | Each sets its own delay; readable as is, and the gap at section 6 is a known, documented item |
| `page-break-inside: avoid` on `.experience-item` in `resume.css` | Must apply in print; it lives in the shared file on purpose |
| `!important` in `print.css` | Needed to beat screen link styling |
| `@page { margin: 0 }` with padding on `.resume__inner` | The padding is the print margin |
| Duplicate content in `index.html` and `markdown.md` | Deliberate: one is the page, one is for pasting into forms. A generator between them is a non-goal |
| `<em>(academic + actively upskilling)</em>` | A claim qualifier, not styling |

## Reporting

List each file simplified and the category (Tokens, Grouping, Ownership, Units, Markup, Comments), then:

**Checks**: pages before = N, after = N; visual difference = none / [what].

If nothing needed changing, say so.
