# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static HTML resume/CV page for Syafiq Bin Shamsuddin. No build tools or dependencies - just vanilla HTML/CSS.

## Files

| File | Purpose |
|------|---------|
| `index.html` | Main resume page (links external CSS) |
| `css/resume.css` | Core styles, variables, components, responsive |
| `css/print.css` | Print-specific overrides (A4 optimized) |
| `css/screen.css` | Screen-only: hover effects, animations |
| `markdown.md` | Resume content source (markdown) |

## Development

Open `index.html` directly in the browser (`file://` path). This project lives under `~/Herd/` but is a plain static directory - it is **not** a Herd-linked site, so `resume.test` does not resolve. No dev server needed.

## Print to PDF

Use browser's print function (Ctrl+P) → Save as PDF. Page is optimized for A4 with proper print styles.

## CSS Architecture

| File | Media | Contains |
|------|-------|----------|
| `resume.css` | all | Variables, reset, typography, components |
| `print.css` | print | Font size, spacing, @page rules |
| `screen.css` | screen | Hover states, fade-in animations |

## Design System

| Element | Value |
|---------|-------|
| Serif font | Cormorant Garamond (display/headings) |
| Sans font | Outfit (body text) |
| Accent | `#8b7355` (warm bronze) |
| Ink | `#0f0f0f` (near-black) |
