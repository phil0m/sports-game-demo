# DECISIONS.md — Ashworth & Vale: Private Financial Counsel

Log of meaningful choices made while building `index.html`, a single
self-contained chat-style finance assistant (HTML/CSS/JS inline, no
external libraries, fonts, or assets). This replaces the previous
"Apex" sports trivia build in this repo per the latest request.

## Concept & persona
- Framed as correspondence with a named private financial counsel —
  **Edmund Vale** of **Ashworth & Vale** — rather than a generic
  "AI assistant" chat box. A persona with a voice (measured, old-money,
  slightly formal) reads as considered rather than templated, and gives
  the scripted responses a reason to sound the way they do.
- Scripted response engine uses **keyword/regex rule matching** against
  11 finance topics (investing, budgeting, debt, retirement, tax,
  business/startup, market/economy, savings, greetings, thanks,
  farewell), each with 2–3 hand-written variations so repeat questions
  don't feel robotic, plus a fallback that asks a clarifying question
  in-voice rather than a dead "I don't understand." No backend/API —
  all canned, as the brief allowed, but tuned to sound specific
  (interest-rate ranking for debt, cash-conversion cycle for business,
  three-to-six-month reserve language) rather than vague filler.

## Avoiding the generic "AI-generated" look
- **Palette**: deep forest/ink green + aged brass + burgundy, on a warm
  parchment text color — explicitly not a purple-to-blue gradient.
  Brass is used as the single accent color throughout (ticker, borders,
  seals, send button) instead of a gradient "hero" identity.
- **No glassmorphism** — panels are solid, layered dark greens with thin
  brass hairline borders (a ledger/leather-bound-book feel), not frosted
  translucent cards.
- **Typography**: Palatino/Iowan Old Style/Georgia serif stack for all
  prose (distinctive, not Inter/system-ui), paired with Courier New
  monospace for all numeric/ticker data — a deliberate "ledger" pairing
  rather than one generic sans font doing everything.
- **No emoji** anywhere; iconography is hand-built inline SVG (a wax-seal
  monogram crest, a shield "seal" mark next to the advisor's name, a
  quill-nib send arrow).
- **Asymmetric layout**: fixed-width sidebar (advisor card + prompt list
  + house motto) beside a wider chat column — not a centered hero. Chat
  bubbles use mixed corner radii (sharp corner on the "origin" side,
  rounded elsewhere) rather than uniform pill shapes, echoing a folded
  letter/stamped card rather than a default chat-app bubble.
- **Scrolling stock ticker** across the top (randomized fake symbols with
  a live random-walk price update every ~2.6s) adds texture and motion
  that's thematically load-bearing, not decorative gradient noise.

## Delight / polish
- **Wax-seal stamp animation + sound** on the send button: a quick
  scale/rotate "thump" synced to a synthesized noise-burst + low sine
  thud (Web Audio API, no audio files) — stands in for the satisfying
  "stamping a letter shut" moment when a message is sent.
- A soft two-note **chime** (Web Audio) plays when Edmund's reply lands,
  and a typing indicator (three breathing dots, styled as pen taps)
  shows during the scripted "thinking" delay (700–1400ms, randomized so
  it doesn't feel metronomic).
- Quick-start prompt chips (sidebar "Begin With" list + composer
  "quick topics" row) insert and auto-send a relevant question — lets a
  first-time visitor see the persona respond immediately without typing.
- Textarea auto-grows with content; Enter sends, Shift+Enter breaks line,
  consistent with real chat-app conventions despite the bespoke visuals.

## Scope narrowed on purpose
- **Rule-based matching, not a full NLU/intent system** — a small,
  curated set of finance topics with strong, specific copy beats a huge
  shallow keyword list. Kept to ~11 categories that cover the most
  common personal/business finance questions.
- **No persistence** (chat resets on reload) — a session-only demo chat
  doesn't need local storage or accounts; added complexity wasn't
  justified for a single self-contained file.
- **Sidebar collapses to a horizontal scroll strip under 860px** rather
  than a hamburger menu/off-canvas drawer — simpler to implement well
  and keeps the advisor card and prompts reachable on phone without
  extra interaction chrome.

## Repo / deployment
- Built directly inside the existing `sports-game-demo` repo as
  instructed, overwriting `index.html` and `DECISIONS.md` in place
  rather than creating new files or a new repo.
- This repo's scoped `.claude/CLAUDE.md` explicitly allows `git push`
  here for deploying `index.html` to GitHub Pages for a class demo —
  that override is local to this repo only and does not change the
  global "never push" rule elsewhere.
- Committed and pushed to `main` so the live Pages site updates.
