# Decisions — Buzzer // Clutch Shot

- **Game concept scaled to one core loop:** a basketball free-throw timing meter (watch a moving marker, tap once to start it, tap again to release in the zone). Reason: a single, well-tuned interaction reads as "finished" in a few minutes; a full multi-sport game would not.
- **Dark/techy look:** near-black background, cyan + orange neon accents, glowing borders, subtle CRT scanline overlay, tabular-number scoreboard digits. Reason: matches the requested dark-mode/techy aesthetic without relying on any image assets or external fonts.
- **Scoring zones:** center "SWISH" zone = 3 pts, wider "GOOD" zone = 2 pts, outside = miss (costs a life). Reason: gives quick positive feedback (most taps score something) while still rewarding precision.
- **Difficulty ramp:** meter speed increases slightly after each make. Reason: keeps the loop engaging without adding extra mechanics.
- **Lives/game over:** 3 misses ends the run, with a retry overlay and a localStorage high score. Reason: gives the mini-game a clear win/lose loop and a reason to replay, using zero backend.
- **Input model:** single button (`SHOOT` → `RELEASE`) rather than drag/swipe gestures. Reason: identical behavior on mouse click and touch tap with no extra event-handling complexity, and it's easy to hit on small phone screens.
- **No external libraries/fonts/images:** everything (ball, hoop, net, glow effects) is drawn with CSS gradients/shapes. Reason: keeps the file single, self-contained, and fast to load on a low-spec machine.
- **Scope cut:** no sound effects, no multiple sports/modes, no settings. Reason: out of scope for a 4-minute build; the brief asked for one focused, polished interaction over broad feature coverage.
- **Not pushed to git:** built and saved locally only. Reason: (1) no git repository was found in the expected project locations on this machine, and (2) the user's global Claude Code rules explicitly forbid running `git push` under any circumstance — that rule overrides the task's push instruction.
