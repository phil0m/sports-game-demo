# DECISIONS.md — Deep Field: Exoplanet Signal Array

Log of meaningful choices made while building `index.html`, a single
self-contained procedural space generator (HTML/CSS/JS inline, no
external libraries, fonts, or assets). This replaces the previous
"Ashworth & Vale" finance-chat build in this repo per the latest request.

## Concept
- Framed as a deep-space SETI-style "signal array" rather than a generic
  "random planet button." Each click is a "triangulation" of a new
  exoplanet signal — gives the randomization a diegetic reason to exist
  and a reason to show a scanning animation before the reveal.
- Generator produces a full **star system reading**, not just a planet:
  host star spectral class/temp, orbital position among N siblings,
  orbital period/distance, radius, mass, surface temp, atmosphere, ring/
  moon presence, a computed habitability index, and a one-off narrative
  "transmission log" sentence — so each result reads as a considered
  dossier, not a single random noun.
- 9 planet archetypes (scorched, molten, barren, tundra, ocean,
  terrestrial, toxic, ice giant, gas giant) x 6 stellar classes x
  continuous numeric ranges for every physical stat, so repeat clicks
  stay visually and texturally distinct rather than cycling a small set
  of canned combinations.

## Avoiding the generic "AI-generated" look
- **Palette**: near-black ink/navy background with a single amber accent
  (`--accent:#ffb454`) — explicitly not a purple-to-blue gradient. Green/
  red are reserved for functional status only (habitability meter ends),
  never used as a decorative gradient identity.
- **No glassmorphism** — panels are solid dark gradients with a thin
  1px hairline border; the only "frosted" surface is the scan overlay,
  which is opaque-dark by design (sensor static), not translucent glass.
- **Typography**: condensed/semibold system sans (`Segoe UI Semibold`/
  `Arial Narrow`) for display text, paired with a monospace stack
  (`Cascadia Code`/`SF Mono`/Consolas) for all data/readouts — a
  deliberate "mission-control telemetry" pairing instead of one generic
  sans doing everything. No Inter, no system-ui.
- **No emoji** — the only iconography is a hand-built inline SVG orbit
  mark in the header; HUD corner brackets (plain CSS borders) frame the
  viewer instead of a rounded card.
- **Asymmetric layout**: viewer/controls panel and data-readout panel
  are unequal widths (1.05fr/0.95fr), not a centered hero or two
  identical columns. Corners of the viewer frame are sharp HUD brackets,
  not uniform rounded corners.
- **Starfield background** is a live canvas of individually twinkling
  stars (phase-offset sine alpha per star), not a static image or CSS
  gradient standing in for "space."

## Delight / polish
- **Procedural canvas planet renderer**: real-time 2D canvas draws a
  shaded sphere (radial gradient + terminator shadow), type-specific
  surface texture (cloud bands for giants, continent/crater blotches for
  rocky/ocean worlds), optional ring system (two-tone, clipped
  front/behind the sphere), and orbiting moons — all procedurally seeded
  per result and animated continuously (slow rotation drift, moon
  orbit), so the output feels like a rendered object, not a static icon.
- **Scanning sequence**: clicking "Triangulate Signal" plays a
  descending synthesized sweep tone (Web Audio, no audio files), steps
  through five status labels ("Acquiring carrier" → "Locking") over a
  filling progress bar, then crossfades to the result with a two-note
  ascending "lock" chime — the moment of delight the brief asked for.
- Data rows fade/slide in with a staggered delay so the readout feels
  like it's populating live rather than appearing all at once.
- Habitability meter fills with an eased transition and a fixed
  red→amber→green gradient strip, scrubbed to the right position by
  background-position — functional color is earned, not decorative.
- "Recent Signals" history (last 6) gives the page a sense of session
  memory and texture without needing actual persistence.
- Hover/active states on the button (glow, color invert, press-scale)
  and on history rows (background tint) for interaction feedback
  throughout.

## Scope narrowed on purpose
- **2D canvas, not WebGL/3D** — a shaded-circle-plus-texture approach
  reads as a convincing procedural planet at this size without the
  performance cost of a 3D renderer, important given the low-spec
  laptop this runs on.
- **No true spherical projection for surface features** — blotches/bands
  are positioned and drifted in 2D polar coordinates against the clipped
  circle rather than projected from a 3D sphere. Visually convincing at
  this scale; a full projection wasn't worth the complexity for a demo.
- **Moon occlusion simplified** — moons always render in front of the
  planet rather than passing behind it. Acceptable simplification; real
  occlusion would need z-sorting per frame for little visible benefit.
- **History capped at 6 entries, session-only** — no localStorage/
  persistence; matches the "single self-contained file, no extra
  complexity" brief and keeps the panel from growing unbounded.
- **Narrative log is template-based** (2 hand-written variants per
  planet archetype, 18 total), not generative text — kept intentionally
  curated rather than a huge shallow template pool, per guidance to
  favor depth over breadth of canned content.

## Repo / deployment
- Built directly inside the existing `sports-game-demo` repo as
  instructed, overwriting `index.html` and `DECISIONS.md` in place
  rather than creating new files or a new repo.
- This repo's scoped `.claude/CLAUDE.md` explicitly allows `git push`
  here for deploying `index.html` to GitHub Pages for a class demo —
  that override is local to this repo only and does not change the
  global "never push" rule elsewhere.
- Committed and pushed to `main` so the live Pages site updates.
