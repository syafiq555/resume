# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview {#overview}

Static HTML resume/CV page for Syafiq Bin Shamsuddin. No build tools or dependencies - just vanilla HTML/CSS. **The GitHub repo is public**: job-search context stays in the gitignored `CLAUDE.local.md`.

## Docs {#docs}

| File | Read when |
|------|-----------|
| `docs/ARCHITECTURE-ESSENTIALS.md` | Before any edit. Short; read it whole |
| `docs/PRD.md` | Deciding whether something is in scope; open questions |
| `docs/ARCHITECTURE.md` | Changing styles, print layout or file structure |
| `tasks/project-docs/current.md` | Changing the doc set itself |

Project agents live in `.claude/agents/` and bootstrap from this file plus the three `docs/` files; a docs change reaches them without an agent edit. Their memory folder `.claude/agent-memory/` is gitignored because it can hold private context.

When they disagree: `index.html` wins over any doc (it is what ships), essentials wins over the other two docs, and `CLAUDE.local.md` wins on anything about the job search. The `[SOURCED]` / `[INFERRED]` / `[TBD]` tags in `docs/` are content; don't strip them in a cleanup.

## Files {#files}

| File | Purpose |
|------|---------|
| `index.html` | Main resume page (links external CSS) |
| `css/resume.css` | Core styles, variables, components, responsive |
| `css/print.css` | Print-specific overrides (A4 optimized) |
| `css/screen.css` | Screen-only: hover effects, animations |
| `markdown.md` | Same content in markdown, kept in parity with `index.html` |

## Development {#development}

Open `index.html` directly in the browser (`file://` path). This project lives under `~/Herd/` but is a plain static directory - it is **not** a Herd-linked site, so `resume.test` does not resolve. No dev server needed.

## Print to PDF {#print}

Use browser's print function (Ctrl+P) → Save as PDF. Page is optimized for A4 with proper print styles. Check the page count after every content edit (see the print-check rule in essentials for the headless-Chrome command). A headless *screenshot* of the screen view comes out blank because it fires mid fade-in; print to PDF and `Read` it instead. `pdftotext -layout` on that PDF shows what an ATS reads, CSS bullet glyphs included.

## CSS Architecture {#css}

| File | Media | Contains |
|------|-------|----------|
| `resume.css` | all | Variables, reset, typography, components |
| `print.css` | print | Font size, spacing, @page rules |
| `screen.css` | screen | Hover states, fade-in animations |

## Design System {#design-system}

| Element | Value |
|---------|-------|
| Serif font | Cormorant Garamond (display/headings) |
| Sans font | Outfit (body text) |
| Accent (`--accent-warm`) | `#8b7355` (warm bronze). `--accent` is a different token, `#1a1a1a` |
| Ink | `#0f0f0f` (near-black) |
