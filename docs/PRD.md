# PRD: Resume page {#prd}

Frame: the standard PRD table (problem, personas, metrics, scope, acceptance, non-goals, roadmap, open questions), trimmed to a one-page product. Tags: `[SOURCED]` traces to the repo or its history, `[INFERRED]` is derived and worth confirming, `[TBD]` means nobody has decided. Tags are content; a tidy-up pass must not strip them.

> This repo is **public**: job-search context never goes in this file. See the public-repo rule in `ARCHITECTURE-ESSENTIALS.md`.

## Problem and positioning {#problem}

A senior full-stack developer needs one resume that reads well in two places: as a PDF attached to applications, and as a page a recruiter can open from a link. Word-processor resumes drift between copies and render differently per machine; a single HTML source printed through the browser gives one layout for both. `[INFERRED]` from the repo's shape (HTML + print stylesheet + markdown source) and `CLAUDE.md`.

## Personas {#personas}

| Persona | Goal | Pain | Success for them |
|---|---|---|---|
| Recruiter / talent screener | Decide in under a minute whether to pass the candidate on | Dense layouts, unclear seniority, keywords hidden in prose | Role, years, core stack and current employer visible in the first screen `[INFERRED]` |
| Applicant tracking system (ATS) | Extract text and keywords from the PDF | Text in images, odd reading order, decorative glyphs mixed into content | Selectable text in document order `[INFERRED]` |
| Hiring manager / interviewer | Find things to probe in an interview | Claims that can't be backed up, buzzword lists | Every bullet is a concrete system plus an outcome they can ask about `[SOURCED]` honesty rules in `ARCHITECTURE-ESSENTIALS.md` |
| The owner (editor) | Retune content per application quickly | Two copies drifting, layout breaking after an edit | Edit `index.html`, print, done `[SOURCED]` `CLAUDE.md` |

## Success metrics {#metrics}

| Metric | Target | Status |
|---|---|---|
| Printed length | 2 A4 pages preferred; 3 acceptable | `[SOURCED]` owner decision 04/11/2026. Prints at 2 today |
| Interview callback rate per application | `[TBD - no target recorded]` | Not tracked in the repo |
| Claims the owner can defend in an interview | All of them | `[SOURCED]` honesty rule, see `ARCHITECTURE-ESSENTIALS.md` |

## Scope: what it does today {#scope}

`[SOURCED]` from `index.html`:

- Header: name, title, location, phone, email, GitHub, LinkedIn.
- Summary paragraph.
- Experience: five roles, newest first, each with role, period, company, location and bullets.
- Side projects, skills grid (label + value rows, including a "Familiar" row carrying a qualifier), education, certifications.
- Screen view: centred paper card, hover states, fade-in on load, reduced-motion respected.
- Print view: A4, zero page margin with inner padding, links rendered as plain text colour.
- `markdown.md`: the same content as markdown, for pasting into forms and job sites.

## Acceptance criteria {#acceptance}

A content or style change is done when:

1. Print preview (Ctrl+P / Cmd+P, A4) shows no experience entry split across pages, and any change in page count is noticed and intended. `[SOURCED]` `page-break-inside: avoid` on `.experience-item`; page target in metrics.
2. `markdown.md` carries the same claims as `index.html`. `[SOURCED]` `CLAUDE.local.md` parity rule.
3. Every number and every strong verb (Architected, Led, Drove) passes the honesty rule. `[SOURCED]` `ARCHITECTURE-ESSENTIALS.md`.
4. No em dash character appears in rendered text. `[SOURCED]` commit `681b472` for text; CSS bullets switched to a hyphen 04/11/2026.
5. The page opens from `file://` with no console errors and no missing font or stylesheet. `[INFERRED]`

## Out of scope {#non-goals}

| Not built | Why |
|---|---|
| Build step, bundler, framework, package manager | One HTML file and three stylesheets are the whole product; a toolchain adds upkeep for no reader-visible gain `[SOURCED]` `CLAUDE.md` "no build tools or dependencies" |
| Hosting / custom domain / Herd site | Opened from `file://`; `resume.test` deliberately does not resolve `[SOURCED]` `CLAUDE.md` |
| Generating `index.html` from `markdown.md` (or the reverse) | Kept as two hand-edited files; when re-syncing, markdown is rebuilt from the HTML `[SOURCED]` `CLAUDE.local.md` |
| Per-application resume variants in the repo | Tuning happens on the one page; per-application cover notes are disposable working files `[SOURCED]` `CLAUDE.local.md` |
| JavaScript | Nothing on the page needs it `[SOURCED]` no `<script>` in `index.html` |
| Photo, icons, skill-level bars | `[INFERRED]` absent by design: they add nothing an ATS can read and cost print space |

## Roadmap {#roadmap}

`[TBD - nothing scheduled]`. Changes are driven by applications as they come up.

## Open questions {#open-questions}

To close one: write the answer where it applies (a metrics row, an acceptance criterion, an essentials rule), then delete its row here.

| Question | Who decides | What it blocks |
|---|---|---|
| `[TBD - none open]` | | |

Closed 04/11/2026: page length (2 is the target, 3 is acceptable; see metrics) and skill-row qualifiers (owner kept the current rows).
