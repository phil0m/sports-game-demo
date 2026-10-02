# DECISIONS.md — Apex: The Sports Trivia Championship

Log of meaningful choices made while building `index.html`, a single self-contained
file with no external libraries, fonts, or assets. This replaces the previous
"clutch-shot" mini-game in this repo per the latest request.

## Scope
- **10 questions per playthrough**, drawn from a pool of 24 across 8 sports
  (basketball, soccer, tennis, American football, baseball, golf, boxing,
  Olympics, hockey, F1, cricket). Narrowed from "build a huge question bank"
  to a curated, well-written set — quality of each question over sheer volume.
- **One game mode** (multiple choice, single round, 3 difficulty presets:
  Rookie / Mixed / Legend) rather than multiple modes (timed, survival,
  categories-select). Keeps the experience tight and polished rather than
  spreading effort thin across half-built modes.
- **Difficulty presets reshuffle the same pool** (easy-weighted, mixed, or
  hard-weighted) instead of maintaining three fully separate question sets —
  gives replay variety without tripling content-writing time.

## Visual style
- Palette: near-black charcoal background with a warm gold (#d4af37) accent,
  cream text — a "championship trophy room" feel rather than generic
  dark-mode-with-a-blue-accent.
- Typography: system serif (Georgia) for headings/question text for a
  classic, engraved-plaque feel; a sans system stack (Optima/Candara/Segoe UI)
  for labels and UI chrome, for contrast. **No Google Fonts link** — kept
  fully offline/self-contained per the "no external files" rule, and it
  removes a network dependency for a demo that may run without wifi.
- Gilded corner brackets, gradient-text headings, and a soft inner/outer
  shadow frame to read as "fancy" without relying on images.

## Delight / polish
- **Confetti burst** (small, DOM-based — no canvas library) fires from the
  selected answer on every correct response, and a larger celebratory burst
  fires on the results screen for a score of 60%+.
- **Synthesized sound effects** via the Web Audio API (no audio files):
  a bright ascending triangle-wave chime for correct answers, a low sawtooth
  buzz for wrong answers, and a four-note fanfare on the results screen.
  Audio context is unlocked on the "Begin" button click (user gesture) to
  satisfy browser autoplay policies.
- Results screen assigns a **rank title** (Rookie Season → The Legend) based
  on score percentage, with bespoke copy per tier, plus an inline SVG trophy
  that animates in with a spring-like pop.
- "Copy Result" button lets the user copy a shareable score line to the
  clipboard — a small extra touch, not a full social-share integration
  (which would require external SDKs/popups, out of scope for a
  self-contained file).

## Interaction / responsiveness
- Options lock and reveal correct/incorrect state immediately on click, with
  a pulse animation on the correct answer and a shake on the wrong pick, so
  feedback is instant and readable at a glance.
- All tap targets (options, buttons, difficulty chips) sized generously for
  touch; `touch-action: manipulation` and disabled tap-highlight for a
  native-feeling mobile interaction.
- Layout is a single centered card that reflows via `clamp()` typography and
  a mobile breakpoint (≤480px) — tested conceptually against phone and
  laptop widths; no separate mobile template needed given the simple
  single-column structure.

## Repo / deployment
- Built directly inside the existing `sports-game-demo` repo as instructed,
  overwriting the prior `index.html` and `DECISIONS.md` rather than creating
  new files or a new repo.
- This repo's scoped `.claude/CLAUDE.md` explicitly allows `git push` here
  for the purpose of deploying `index.html` to GitHub Pages for a class
  demo — that override does not change the global "never push" rule, and
  was only exercised within this repo, for this purpose.
- Committed and pushed to `main` so the live Pages site updates.
