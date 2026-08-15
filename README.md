# Carnet

A personal, self-contained web app for prepping for 1L Fall 2026 at Brooklyn Law School — key dates, curriculum, IRAC/case-briefing reference material, a pre-semester reading list, a task/event tracker, and a growing set of full case pages with timed practice questions.

No build step, no framework, no dependencies. Every page is a single static HTML file with its CSS and JS inline. Open `index.html` directly in a browser, or serve the folder with any static file server.

## Structure

```
carnet/
├── index.html                  Home page — dates, curriculum, IRAC guide, reading list, schedule, prep, resources
└── pages/
    ├── tracker.html             Task & event tracker
    ├── professors.html          Professors & reading-prep guide
    ├── vosburg_case.html        Vosburg v. Putney — full case page
    ├── vosburg_practice.html    Vosburg v. Putney — timed practice question
    ├── vosburg_history.html     Vosburg v. Putney — background/history reading
    ├── palsgraf_case.html       Palsgraf v. Long Island Railroad — full case page
    ├── palsgraf_practice.html   Palsgraf v. Long Island Railroad — timed practice question
    ├── byrne_case.html          Byrne v. Boadle — full case page
    ├── byrne_practice.html      Byrne v. Boadle — timed practice question
    ├── byrne_bonusreading.html  Byrne v. Boadle — bonus reading (res ipsa loquitur)
    ├── pierson_case.html        Pierson v. Post — full case page
    └── pierson_practice.html    Pierson v. Post — timed practice question
```

## Home page (`index.html`)

- **Fall 2026 – key dates** — Convocation, orientation, and semester dates
- **Your 1L curriculum** — Fall 2026 course list (professors, room numbers) and a note on what's Spring 2027
- **The semester in phases** — how the semester breaks down over time
- **IRAC framework** + **IRAC worked example**
- **Case brief structure**
- **Pre-semester reading** — the case reading list, organized into priority tiers (which cases to read first, and which are already covered by on-site practice materials)
- **Model weekly schedule**
- **Pre-semester prep**
- **BLS resources**
- Links out to the tracker, the professors/reading-prep guide, and every built-out case page

## Case pages

Each case that gets built out follows the same pattern, so navigation stays predictable:

1. **`<case>_case.html`** — the full opinion (holding summary, procedural posture, majority/dissent), styled to match the site theme
2. **`<case>_practice.html`** — a timed IRAC practice exam on that case: a new fact pattern, a textarea for the answer, and a model answer + graded rubric revealed on submit
3. Optional **`<case>_bonusreading.html`** or **`<case>_history.html`** for extra background reading, linked from the case page's footer

Cases currently built out: Vosburg v. Putney, Palsgraf v. Long Island Railroad, Byrne v. Boadle, Pierson v. Post. Additional cases from the reading list get the same three-file treatment as they're added.

## Theming

All pages share one light/dark CSS-variable system (`--bg`, `--text`, `--border`, `--card-bg`, plus teal/purple/amber/coral/blue/gray accent families for each subject — Torts=teal, Contracts=coral, Civil Procedure=blue, Criminal Law=amber, Property=purple). Theme is toggled with the sun/moon button on every page and persisted via `localStorage`, defaulting to the OS preference on first visit.

## Navigation

Back/forward arrows on each page use real browser history (`history.back()`/`history.forward()`), with a `sessionStorage` guard so a page opened directly still falls back to a working link to the home page instead of navigating into empty history.
