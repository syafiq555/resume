# Architecture essentials {#essentials}

Rules that can be broken in a single line without anything visibly failing. Read all of it before editing. Cite rules by name, not number. Background and reasoning: `docs/ARCHITECTURE.md`; scope: `docs/PRD.md`.

## 1. Public repo: no job-search context in committed files {#public-repo}

`github.com/syafiq555/resume` is public, so everything committed (including `docs/`, `tasks/` and commit messages) is readable by any employer. Commit subjects predate this rule, so don't cite commits by hash in docs. Target roles, active applications, company names being applied to, and positioning notes go in the gitignored `CLAUDE.local.md` only. Per-application cover notes are working files; committing one publishes it.

## 2. Every number must be defensible in an interview {#defensible-numbers}

A figure stays only if the owner can explain how they'd back it up. Prefer a smaller true number or a qualitative claim to a bigger one nobody can source.

## 3. Verbs match the real role {#verbs-match-role}

"Owned", "Architected", "Led" and "Drove" claim specific responsibility. Use "Built" or "Developed" for work done as one developer on a team. Check strong verbs against the role, not just the numbers.

## 4. Skill qualifiers are content {#qualifiers}

A qualifier such as "(academic + actively upskilling)" is part of the claim. Moving a skill out of the Familiar row, or deleting the qualifier, changes what the resume asserts.

## 5. index.html and markdown.md change together {#parity}

Any claim edited in one is edited in the other in the same change. When they've drifted, rebuild `markdown.md` from `index.html`, never the reverse: the HTML holds the corrected claims.

## 6. No em dashes in text {#no-em-dash}

Use a hyphen, a colon or brackets. Date ranges use the en dash already in place. CSS `content:` glyphs count too, because they land in the PDF text an ATS reads; the list bullets are a hyphen. Check both forms, the character and the CSS escape (written as escapes so the character stays out of this file):

`grep -c "$(printf '\342\200\224')" index.html markdown.md css/*.css; grep -c '\\2014' css/*.css`

Every count must be 0.

## 7. Check the printed page after every content edit {#print-check}

One added bullet can add a page or split an entry, and nothing on screen shows it. Two pages is the target and three is acceptable, so a new page should be a choice, not an accident. Print preview at A4 before calling a change done, or from the shell (macOS):

`"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless=new --no-pdf-header-footer --print-to-pdf=/tmp/resume-check.pdf "file://$PWD/index.html" && grep -ao '/Count [0-9]*' /tmp/resume-check.pdf | head -1`

`/Count N` is the page count. Then open the PDF to check no entry splits. Sizes in `resume.css` belong in `rem` so they shrink with `print.css`'s `10.5pt` root; a `px` size won't.

## 8. Colours and fonts come from `:root` {#tokens}

New colour or font values are added as custom properties in `css/resume.css` and referenced with `var()`. Existing exceptions (body gradient, shadows, the hover tint in `screen.css`) are listed under risks in `ARCHITECTURE.md`; don't add to them.

## Not built, on purpose {#not-built}

No build step, no package manager, no JavaScript, no hosting, no generator between HTML and markdown, no per-application variants in the repo. Reasons in `docs/PRD.md#non-goals`.
