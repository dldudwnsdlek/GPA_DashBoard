# CLAUDE.md — GPA Dashboard

## Project Overview

A single-page academic performance dashboard for a student at Kangnam University (강남대학교). The entire application lives in one file: `index.html`. There is no build system, no backend, no package manager, and no test suite.

## Repository Structure

```
GPA_DashBoard/
└── index.html     # The entire application (HTML + CSS + JS, ~415 lines)
```

## Technology Stack

| Layer      | Technology                               |
|------------|------------------------------------------|
| Markup     | HTML5                                    |
| Styling    | CSS3 (custom properties, Grid, Flexbox)  |
| Logic      | Vanilla JavaScript (ES6+)                |
| Charts     | Chart.js 4.4.1 (loaded via CDN)          |
| Fonts      | Google Fonts CDN (Noto Sans KR, DM Mono) |
| Build tool | None                                     |
| Backend    | None                                     |
| Database   | None — all data is hardcoded             |

## Running the Application

Open `index.html` directly in a browser, or serve it with any static HTTP server:

```bash
# Python
python3 -m http.server 8080

# Node.js (npx)
npx serve .
```

No installation, compilation, or environment setup is required.

## File Layout Inside index.html

| Lines     | Section                          |
|-----------|----------------------------------|
| 1–8       | `<head>` — meta, CDN links       |
| 9–90      | `<style>` — all CSS              |
| 92–215    | `<body>` — HTML markup           |
| 217–413   | `<script>` — all JavaScript      |

## Key UI Sections

### Header
- Student name (이영준 / Lee Young-jun) and degree info (Business + Data Science double major)
- Overall credit count and GPA badge

### KPI Cards (`.kpi-grid`)
- Five animated metric cards; values animate in with a count-up effect
- Staggered entrance animations driven by `data-delay` attributes

### Tab Navigation (`.tabs`)
Three panels switched via `data-tab` / `data-target` attributes:

| Tab label         | Panel ID         | Content                                |
|-------------------|------------------|----------------------------------------|
| 📈 GPA Trend      | `#panel-trend`   | Multi-line GPA chart across semesters  |
| 🧬 DS Major       | `#panel-ds`      | Bar chart of DS courses + gauge        |
| 📊 Composition    | `#panel-comp`    | Credit stacked bar + grade comparison  |

### Charts (Chart.js instances)

| Variable      | Type            | Purpose                               |
|---------------|-----------------|---------------------------------------|
| `chartTrend`  | Line            | Semester GPA for Overall / Business / DS |
| `chartDS`     | Horizontal Bar  | Per-course score for 14 DS courses    |
| `chartCredit` | Stacked Bar     | Credit distribution by semester       |
| `chartGrade`  | Grouped Bar     | A+/A/B+/Below grade split by major    |

## CSS Conventions

- **CSS custom properties** defined in `:root` — always modify colors/spacing here, never hardcode values inline.
- **Dark theme** design system:
  - `--bg` `#0B1120` — page background
  - `--surface` `#111827` — card background
  - `--text` `#E2E8F0` — primary text
  - `--blue` — Business major accent
  - `--green` — Data Science accent
  - `--orange` — highlight/accent
- **Naming**: kebab-case for classes (`.kpi-grid`, `.chart-container`, `.tab-btn`)
- Layout uses CSS Grid for the KPI grid and composition sections; Flexbox elsewhere.
- Animations via `@keyframes fadeUp`; entrance timing controlled by inline `--delay` variables.

## JavaScript Conventions

- **No frameworks** — vanilla JS only.
- **Data arrays** are declared at the top of the `<script>` block and prefixed by subject: `dsNames`, `dsScores`, `dsGrades`, etc.
- **camelCase** for all JS identifiers.
- Tab switching: click handler reads `data-target` attribute to show/hide panels.
- Count-up animation uses `requestAnimationFrame` with cubic-bezier easing.
- Chart.js custom plugins (reference lines, average markers) are defined inline next to the chart they belong to.

## Data Updates

All academic data is hardcoded inside the `<script>` block. To update:

1. Locate the relevant array near the top of the `<script>` section (e.g., `dsScores`, `semesterLabels`, `gpaOverall`).
2. Edit the values in place.
3. Update KPI card text in the HTML (`.kpi-value` elements) if summary numbers change.
4. No build step — save the file and refresh the browser.

## Git Workflow

- Main development branch: `master`
- Feature / AI-generated branches follow the pattern: `claude/<session-id>`
- Commit messages have historically been short and descriptive (e.g., "Update index.html").
- There is no CI/CD pipeline; changes go live by updating the file on the hosting target.

## What This Project Does NOT Have

- No package manager (`npm`, `pip`, etc.)
- No build pipeline (Webpack, Vite, Parcel, etc.)
- No TypeScript
- No test suite
- No linter / formatter config
- No backend or API calls
- No environment variables
- No Docker or deployment scripts

Do not attempt to add a build step or framework unless explicitly requested — the single-file approach is intentional.
