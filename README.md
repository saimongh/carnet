# Carnet

A personal, self-contained web app for 1L Fall 2026 at Brooklyn Law School. `index.html` is a **directory** — it holds the semester calendar and links out to everything else. All the substantive material lives on dedicated pages.

No build step, no framework, no dependencies. Every page is a single static HTML file with its CSS and JS inline. Open `index.html` directly in a browser, or serve the folder with any static file server. The only external asset is the Font Awesome icon stylesheet, loaded from cdnjs.

## Structure

```
carnet/
├── index.html                      Directory + semester calendar + weekly timetable
└── pages/
    ├── case_guide.html              IRAC framework, IRAC worked example, case brief structure
    │
    ├── crimlaw_readings.html        ── one reading page per class ──
    ├── property_readings.html
    ├── torts_readings.html
    ├── gateway_readings.html
    ├── isl_readings.html
    ├── contracts_readings.html      Spring 2027 preview
    ├── civpro_readings.html         Spring 2027 preview
    │
    ├── tracker.html                 Task & event tracker
    ├── orientation_guide.html       Orientation walkthrough (Thu, Aug 20)
    ├── professors.html              Professors & reading-prep guide
    ├── isl_study_companion.html     Full ISL packet companion
    │
    ├── crimlaw_process_reading.html      ── assigned reading pages ──
    ├── crimlaw_legality_reading.html
    ├── crimlaw_punishment_reading.html
    ├── crimlaw_culpability_reading.html
    ├── just_mercy_reading.html
    ├── kerr_reading.html
    ├── slocum_reading.html
    │
    ├── vosburg_case.html            ── case pages ──
    ├── vosburg_practice.html
    ├── vosburg_history.html
    ├── palsgraf_case.html
    ├── palsgraf_practice.html
    ├── byrne_case.html
    ├── byrne_practice.html
    ├── byrne_bonusreading.html
    ├── pierson_case.html
    ├── pierson_practice.html
    ├── benjamin_case.html
    └── benjamin_practice.html
```

## Home page (`index.html`)

Deliberately thin. It carries:

- **Readings by class** — a card per class, each linking to that class's reading page
- **Spring 2027 preview** — Contracts and Civil Procedure, same format, marked as not urgent
- **Guides & tools** — case guide, tracker, professors, orientation guide, ISL companion
- **Fall 2026 key dates** — the full Aug–Jan timeline
- **Weekly class timetable** — the fixed Mon–Fri grid with times, professors, and rooms
- **Your 1L curriculum**, **the semester in phases**, **model weekly schedule**, **pre-semester prep**, **BLS resources**

Everything that used to sit inline on the home page (IRAC, briefing, the reading lists) now lives on its own page.

## Reading pages

Every class gets one page, and every page has the same three sections in the same order:

1. **Assigned readings** — casebook chapters, packet excerpts, background material
2. **Case readings** — primary-source opinions
3. **Completed readings** — anything finished

Each entry can be moved between sections:

| From | To | Button |
| --- | --- | --- |
| Assigned | Case readings | *Move to case readings* |
| Assigned | Completed | *Mark complete* |
| Case readings | Assigned | *Move to assigned readings* |
| Completed | Assigned | *Reopen as assigned* |

A case reading can't be marked complete directly — move it to assigned first. That's intentional: the assigned list is the "this is what I actually owe" list.

### Persistence

Moves are saved to `localStorage` under the single key `carnetReadings`, shaped as `{ classId: { itemId: bucket } }`. State is per browser, per device.

- **Export status** downloads `carnet-readings-YYYY-MM-DD.json` containing every class, not just the one you're on
- **Import status** merges an exported file back in
- **Reset this class** clears the overrides for the current page only

## Case pages

Each case that gets built out follows the same pattern:

1. **`<case>_case.html`** — the full opinion (holding summary, procedural posture, majority/dissent)
2. **`<case>_practice.html`** — a timed IRAC practice exam: a new fact pattern, a textarea, and a model answer + graded rubric revealed on submit
3. Optional **`<case>_bonusreading.html`** / **`<case>_history.html`** for background

Built out so far: Vosburg v. Putney, Palsgraf v. Long Island Railroad, Byrne v. Boadle, Pierson v. Post, Benjamin v. Lindner Aviation.

## Theming

All pages share one light/dark CSS-variable system (`--bg`, `--text`, `--border`, `--card-bg`, plus per-subject accent families — Torts=teal, Property=purple, Criminal Law=amber, Contracts=coral, Civil Procedure & Gateway=blue). Theme is toggled with the sun/moon button and persisted via `localStorage`, defaulting to the OS preference on first visit.

## Navigation

Every page carries the same chrome in the same place:

- **Hamburger (top left)** — the full directory, identical on every page, with the current page highlighted. Closes on scrim click or `Esc`.
- **Back / forward arrows** — real browser history, with a `sessionStorage` guard so a page opened directly falls back to a working link home instead of navigating into empty history.
- **Home button** — direct link to `index.html` on every sub-page.
- **Sun/moon (top right)** — theme toggle.

`isl_study_companion.html` keeps its own layout and gets a lighter top-right nav (Back / ISL readings / Home) instead, since its own left sidebar would collide with the shared one.
