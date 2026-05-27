# Decisions so far

Working notes from the brainstorming session. Not the final spec — once Sections 2–6 of the design walkthrough are approved, a proper spec lands at `docs/superpowers/specs/YYYY-MM-DD-battle-line-phase-1-design.md`. Until then, this file is the record.

## Project

Browser-based clone of Reiner Knizia's *Battle Line*. Plays on desktop and on a mobile phone in the browser. For personal use, no public release. Custom art comes later.

## Roadmap (decomposed into phases)

1. **Phase 1 — local pass-and-play.** Two humans, one device. Base game rules only. This spec covers Phase 1 only.
2. **Phase 2 — online multiplayer.** Same game, two devices, server, lobbies, real-time sync.
3. **Phase 3 — AI opponent.** Bot you can play against (in either local or online mode).
4. **Phase 1.5 (parallel-ish) — tactics deck.** Added later as a toggle once Phase 1 is solid.

Phase 1 designs must not block Phase 2 or 3. In practice that means a pure, serialisable rules engine kept separate from the UI.

## Decisions locked

| # | Decision | Choice |
|---|----------|--------|
| 1 | Rules scope for Phase 1 | Base game only. Engine designed so tactics cards can be bolted on as Phase 1.5 without ripping it apart. |
| 2 | Audience | Personal use. Placeholder art now, custom art later. |
| 3 | Tech stack | React + TypeScript + Vite + Tailwind (handled by Claude — user delegated tech choices). |
| 4 | Game logic architecture | Pure functional rules engine, immutable state, separate from UI. Enables Phase 2 (server reuse) and Phase 3 (AI simulation) cheaply. |
| 5 | Mobile layout | On phones in portrait, the board rotates 90°. Flags stack vertically down the screen, one per row. Hand pinned at bottom, opponent's face-down hand at top. Desktop keeps the classic horizontal arrangement. |
| 6 | Claim flag UX | Manual claim with validation. Player taps "Claim" on a flag, game checks deductively (deck + opponent hand). No hint toggle — purist Knizia. |
| 7 | Pass-the-device handoff | Between every turn, a full-screen "Pass to [Name] — Ready" card hides the board so the wrong player can't peek. |
| 8 | Save / resume | Browser auto-saves after every action. Single in-progress game, no save slots. Refresh-safe. |
| 9 | End-of-game | Winner screen overlays the board, with "New game" and "Review final board" buttons. |
| 10 | Interactions | Both drag-and-drop *and* tap-card-then-tap-flag. Discard pile visible to both players. |
| 11 | Match structure | Single games only. No best-of-3. (Best-of-X only earns its keep once tactics-card carry-over exists.) |
| 12 | Visual style | Modern geometric. Six colour/shape pairs: Red◆, Blue▲, Green⬢, Yellow★, Purple●, Orange■. Numbers 1–10 large in centre, corner icons top-left + bottom-right (rotated) for colourblind accessibility. |
| 13 | Draw mechanic | Tap the deck to draw (not auto-draw). One intentional beat before the device passes. |
| 14 | Setup flow | Two name fields (defaults pre-filled), one Start button. Random first player, single coin-flip animation. No colour pick, no first-player pick. |

## Design walkthrough — section status

- **Section 1 — Game flow start to finish.** Approved.
- **Section 2 — Layout (desktop + mobile + card design + claim button placement).** Static mockup at `mockups/layout-preview.html`. Awaiting feedback on the mockup.
- **Section 3 — Rules behaviour** (formations, claim validation, win conditions). Not yet drafted.
- **Section 4 — Save/resume + edge cases.** Not yet drafted.
- **Section 5 — Under-the-hood architecture** (in plain English). Not yet drafted.
- **Section 6 — Testing approach.** Not yet drafted.
- **Section 7 — Out of scope.** Not yet drafted.

## Where to pick up next session

Open `mockups/layout-preview.html` in a browser, decide whether the layout reads well. If yes, move on to Section 3 (Rules behaviour). If anything needs revising, call it out and revise Section 2 first.

After all sections are approved, the spec gets written to `docs/superpowers/specs/2026-MM-DD-battle-line-phase-1-design.md` and committed. Then we hand off to the `superpowers:writing-plans` skill to produce an implementation plan. No code gets written before that.

## Out of scope for Phase 1 (explicitly)

- Tactics cards (Leaders, Mud, Fog, Scout, Redeploy, Deserter, Traitor).
- Online multiplayer.
- AI opponent.
- Match wrapper (best-of-3).
- Player accounts, profiles, history.
- Custom art assets.
- Sound.
- Animations beyond the basics (card placement, flag claim).
