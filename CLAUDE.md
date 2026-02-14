# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Ce Citim Azi** is a static HTML educational platform for family medicine residents in Romania. It contains medical theory summaries, multiple-choice quizzes, and interactive clinical cases. No build tools, frameworks, or external dependencies — everything is plain HTML5, CSS3, and vanilla JavaScript embedded inline in each file.

## Running Locally

```bash
python3 -m http.server 8000
# Then open http://localhost:8000
```

No build, lint, or test commands exist. All testing is manual in a browser.

## Architecture

**Hub-and-spoke navigation:** `index.html` is the entry point. Each chapter has three pages:

- `*_rezumat.html` — structured medical theory with color-coded info boxes
- `*_grile.html` — 10 multiple-choice questions with live scoring and explanations
- `*_caz_clinic.html` — multi-step interactive clinical scenario with progress tracking

**Current chapters:**
- `tranzit_*` — Tulburări de Tranzit (diarrhea & constipation)
- `cefalee_*` — Cefaleea (headaches)

**Planned chapters** (linked as "coming soon" in index.html): Durerea Toracică, Hipertensiunea Arterială, Diabetul Zaharat

## Design System

All pages share a consistent CSS custom property palette defined inline per file:
- `--dark-blue: #1a365d` — primary headers
- `--teal: #319795` — accent / teal info boxes
- `--purple: #6b46c1`, `--orange: #dd6b20`, `--red: #e53e3e` — content type differentiation
- Responsive breakpoint at `max-width: 600px`

## Adding a New Chapter

1. Create three files: `<slug>_rezumat.html`, `<slug>_grile.html`, `<slug>_caz_clinic.html` — copy an existing chapter as template.
2. Add the chapter card in `index.html` inside the appropriate specialty section, following the existing `chapter-card` HTML pattern.
3. Quiz pages use `selectOption(questionIndex, optionIndex, correctIndex)` in JS — keep the same function signature.
4. Clinical case pages manage a `currentStep` state variable and call `showStep(n)` to advance the scenario.
