# Project: IGCSE 2026 Study Planner

**Last Updated:** 2026-02-23

## Overview

A single-file static web app for IGCSE May/June 2026 exam preparation. Covers 8 subjects with topic checklists, exam timetables, paper breakdowns, and study strategies. No build step — open `index.html` directly in a browser.

## Technology Stack

- **Single file:** `index.html` (all HTML, CSS, JS inline, ~1550 lines)
- **Fonts:** Google Fonts (DM Serif Display, DM Sans, JetBrains Mono) via CDN
- **Persistence:** `localStorage` key `igcse-checked` (topic completion state)
- **No frameworks, no build tools, no package manager**

## Subjects Covered

ICT (0417), Computer Science (0478), Business Studies (0450), English First Language (0500), English Literature (0475), Combined Science (0653), Additional Maths (0606), Global Perspectives (0457)

## Architecture

All content lives in `index.html`. Structure:

```
<head>          CSS custom properties + all styles
<body>
  .nav-bar      Tab navigation (overview, exam-tracker, 8 subject sections)
  #overview     Subject grid with countdown timer
  #exam-tracker Per-subject exam date countdown grid
  #ict … #gp   Subject sections (each has detail tabs: Papers, Topics, Strategy)
<script>
  subjects{}    Exam data (name, code, exams array with iso dates)
  topicData{}   Topic lists keyed by element ID (e.g. 'ict-topics')
  updateCountdown()   Live countdown to 2026-04-01 (first ICT practical)
  renderTopics()      Renders checkable topic lists from topicData
  toggleCheck()       Saves/loads checked state via localStorage
  renderTracker()     Renders exam countdown grid from subjects{}
```

## Key Patterns

- **Adding a topic:** Add `[num, name]` tuple to the right `topicData` array
- **Adding an exam date:** Add entry to `subjects[key].exams` with `iso: 'YYYY-MM-DD'`
- **Colours:** Use CSS custom properties from `:root` (e.g. `var(--accent)`, `var(--green)`)
- **Dark theme:** Background `#0a0a0f`, surface layers `--surface`, `--surface2`, `--surface3`
- **File size limit:** File is ~70KB / 1550 lines — keep additions concise

## Development Commands

- **View:** Open `index.html` directly in a browser (no server needed)
- **Test UI:** `playwright-cli open file:///Users/harvey/Desktop/StudyPlanner/index.html`
- **Deploy:** `git push` to `https://github.com/Toramiyuu/StudyPlanner` (main branch)
