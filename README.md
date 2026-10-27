# Pocket Hours

> *"Your life has its own pace."*

A quiet, calm, personal time-tracking and study companion. Built as a warm,
minimal, single-user web app — not a pressuring productivity dashboard.

Pocket Hours keeps a prominent focus timer and stopwatch at the center of a
gentle daily workspace, with history, countdowns, and fully local settings.
All data lives in your browser; nothing is sent to any server.

---

## What it does

**Today** — the primary screen
- A prominent circular **focus timer** (25 / 45 / 60-minute presets + custom duration)
  with start, pause, resume, reset, short/long breaks, and auto phase advancement.
- A **stopwatch** that shares the same interface (toggle between Timer and Stopwatch).
- Timestamp-based timing — accurate even if you switch tabs or the browser is suspended.
- A subject/task selector and manual session logging.
- A compact **insights panel**: today's focused time, session count, hourly activity
  chart, subject distribution, today's session list, and a gentle streak.
- A **primary milestone** preview from your Countdowns.

**History** — patterns over time
- A selectable calendar with per-day focus time.
- Day / Week / Month / Year views with aggregate stats.
- Trend charts and subject breakdowns that respond to the selected range.
- Session records grouped by date — edit or delete any record.

**Countdowns** — milestones & horizons
- Add, edit, delete countdowns (exam, course, personal, milestone…).
- Choose an accent color, description, and mark one as **primary** (shown on Today).
- Past events are correctly labeled as completed — no misleading negative countdowns.

**Settings** — make it yours
- Light/dark theme, adjustable accent color, font size, profile name.
- Focus preferences: durations, break intervals, sounds (chime / bell / birdsong) + volume.
- Subject & task management with colors.
- **Export** backup (JSON), **export** sessions (CSV), **import** backup (merge or replace),
  and **reset all data** — all with confirmation.
- Privacy notes explaining that data stays on-device.

**Quiet Mode** — a real, functional toggle
- Hides decorative elements (rotating quotes, milestone preview, streak).
- Removes transition animations and reduces nonessential distractions.
- Keeps the timer and all core controls available.

---

## Design system

Built from the supplied reference (warm cream canvas, terracotta / sage / muted-blue
accents, walnut browns, charcoal ink) with a refined editorial feel:

- **Typography** — Newsreader (serif) for titles, timer numerals, and reflective text;
  Manrope (sans) for body, navigation, and controls.
- **Surfaces** — warm cream canvas, soft paper cards with hairline borders (no heavy shadows).
- **Components** — primary/secondary/outlined/ghost buttons, toggles, segmented controls,
  chips, badges, search inputs, progress bars, calendar cells, empty states, and dialogs.

The layout is deliberately **more compact and information-dense** than the references,
fitting a practical tablet/desktop viewport without shrinking text.

---

## Deploy to GitHub Pages (so anyone can open it)

The project is ready to push to GitHub and auto-deploy to GitHub Pages.

### One-time setup

1. **Create a GitHub repository** (e.g. `pocket-hours`):
   - On GitHub: **New repository** → name it `pocket-hours` → choose **Public** → click **Create repository**.
   - *Do not* initialize with a README (we already have one).

2. **Push this folder to GitHub** (from `/home/user/pocket-hours`):
   ```bash
   cd /home/user/pocket-hours
   git remote add origin https://github.com/YOUR-USERNAME/pocket-hours.git
   git branch -M main
   git push -u origin main
   ```
   (Replace `YOUR-USERNAME` with your GitHub username.)

3. **Enable GitHub Pages**:
   - On your repo page: **Settings** → **Pages** (left sidebar).
   - Under **Build and deployment** → **Source** → select **GitHub Actions**.
   - Save. The included workflow (`.github/workflows/deploy.yml`) will automatically
     deploy on every push to `main`.

4. **Open it**:
   - Wait ~30 seconds after the workflow finishes.
   - Your site will be at:
     `https://YOUR-USERNAME.github.io/pocket-hours/`

That's it — every future `git push` redeploys automatically.

### Local preview (same as GitHub Pages)
```bash
cd pocket-hours
python3 -m http.server 8080
# or: npx serve -l 8080 .
```
Open <http://localhost:8080>.

> The app uses ES modules, so it must be served over HTTP (not opened via `file://`).
> GitHub Pages and any static server both work fine.

---

## Project structure

```
pocket-hours/
├── index.html              # App shell + boot script
├── css/
│   └── styles.css          # Full design system + responsive layout
└── js/
    ├── app.js              # Bootstrap: builds shell, applies theme, starts router
    ├── router.js           # Hash-based client-side routing (no reloads)
    ├── store.js            # localStorage data layer (sessions, settings, CRUD)
    ├── timer.js            # Timestamp-based timer & stopwatch engine
    ├── stats.js            # Pure insight/aggregation functions
    ├── utils.js            # DOM helpers, formatting, icons, dialogs, toasts
    └── pages/
        ├── today.js        # Today dashboard: timer + insights
        ├── history.js      # History: calendar, stats, records
        ├── countdowns.js   # Countdowns: CRUD + primary milestone
        ├── settings.js     # Settings: appearance, focus, subjects, data, privacy
        └── milestone.js    # Primary milestone preview card
```

---

## Data & privacy

- All data is stored in **localStorage** under the `pockethours.v1` key.
- **No accounts, no network calls, no third-party servers.**
- Export a JSON backup or CSV before clearing browser data.
- If cloud sync is ever added, it will be optional and explicit.

---

## Technical notes

- **Accurate timing**: the timer computes remaining time from absolute timestamps
  (`endsAt`), not a running interval, so tab switches and browser suspension don't
  drift it. `visibilitychange` re-syncs on return.
- **No fabricated data**: every statistic is derived from saved session records.
- **Accessibility**: semantic buttons, `aria-label`s, keyboard-focusable controls,
  and `prefers-reduced-motion` support.
- **Responsive**: left sidebar on desktop, collapsible rail on tablet, drawer on mobile;
  single-column layouts and a sticky insights column where space permits.

---

## Testing

The project was verified with headless test suites (logic + DOM rendering +
interactions + persistence):

- **65** core-logic tests (store, stats, timer math, import/export, CRUD)
- **53** render tests (all four pages, navigation, timer start, stopwatch)
- **15** interaction tests (quiet mode, countdown/subject CRUD, theme, accent, font)
- **9** persistence tests (data survives a full reload)

All pass with zero runtime errors.

---

*Pocket Hours — a quiet companion for your time.*
