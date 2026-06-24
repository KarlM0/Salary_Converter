# Changelog

All notable changes to this project will be documented in this file.

The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).
This project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [1.1.0] — 2026-06-25

### Added
- **Version number** displayed in the page subtitle area, below the usage hint.
- **"View on GitHub" link** displayed below the version number, pointing to the
  project repository at `https://github.com/KarlM0/Salary_Converter/`.
- **Multi-source FX fetching with automatic fallback.** All three rate sources
  (Frankfurter/ECB, open.er-api.com, Currency API via jsDelivr) are queried in
  parallel on every load and refresh. The highest-priority source that succeeds
  is used; the others serve as silent fallbacks.
- **Rate status panel** above the grid, showing: active source name and data
  date when live; a per-source success/failure indicator (✓/✗) for every
  source tried; current EUR→CZK/USD/GBP values; and a warning state
  (amber border) when only fallback rates are in use.
- **Manual *Refresh rates* button** that re-queries all sources and, if a cell
  is already filled, immediately recomputes the grid with the updated rates.
- **Hardcoded fallback rates** (EUR 1 : CZK 25.20 : USD 1.08 : GBP 0.85) used
  when every source fails, so the tool remains usable offline.
- **Cache-busting** on every FX request (`_=<timestamp>` query parameter +
  `cache: "no-store"`) to ensure the Refresh button always retrieves fresh data.
- **Recompute-after-refresh** — if a cell was filled before rates were updated,
  the grid recalculates automatically once new rates arrive.
- **Comma decimal-separator support** — input parser normalises `,` to `.`
  before parsing, in addition to ignoring whitespace used as thousands
  separators.
- **Thousands separator in output** — displayed numbers use a space as a
  thousands separator (e.g. `1 234 567.89`) for readability.
- **On-blur normalisation** — when a user leaves an input cell, their raw entry
  is reformatted to the standard truncated 2-decimal display format.
- **HTML-escape helper** (`escapeHtml`) applied to all dynamic content inserted
  into the status panel to prevent injection from API responses.

### Changed
- Calculation engine now uses **EUR per hour** as the single intermediate unit,
  making any cell the unambiguous source of truth and ensuring cross-cell
  consistency regardless of which cell is edited.
- Output values are now **truncated** (cut, not rounded) to 2 decimal places,
  consistent with the footer note.
- Status panel replaces a simple text label with a structured three-row layout
  (active source / rate values / sources breakdown).

---

## [1.0.0] — 2026-05-07

### Added
- Initial release.
- Single-file HTML app with no external dependencies.
- Grid of 5 periods × 4 currencies (CZK, EUR, USD, GBP) with live
  bidirectional recalculation on every keystroke.
- Dark-themed UI with a CSS custom-property colour system.
- Single FX rate source (Frankfurter/ECB) fetched on page load.
- Footer noting working-time assumptions (8 h/day, 5 days/week,
  21.5 days/month, 260 days/year).
