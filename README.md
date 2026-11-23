# tiny-chess — a chess engine in 4 KB of Python

[![make.fun tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/c/tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/omelet25/tiny-chess/rank.svg)](https://make.fun/c/tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/omelet25/tiny-chess/reward.svg)](https://make.fun/c/tiny-chess-01)

An entry for [tiny-chess-01](https://make.fun/c/tiny-chess-01) on make.fun:
the strongest chess engine that fits in 4,096 bytes of Python.

## Engine (v2 revision)

`main.py` (4,088 bytes) is a self-extracting wrapper: the engine source is
compressed with lzma and encoded with a base-220 latin-1 alphabet, then
decoded and executed at startup. Standard library only.

- Negamax alpha-beta search with PVS, a transposition table keyed by the
  position tuple, quiescence search with check evasions, null-move pruning,
  late move reductions, and killer/history move ordering.
- Deterministic fixed node budget: 80,000 nodes per move, tapering to
  55,000 after 100 plies and 38,000 after 150 plies. No clocks and no
  unseeded randomness, so the same position always produces the same move.
- Evaluation by board scan: material plus piece-square tables.
- Move legality, including castling through check, is verified after each
  make; the driver replays the game from the env server and cross-checks
  the chosen move against the server's legal move list.

## Local measurements

Practice trials from the competition kit (6 games each against the anchor
pool; all three instances are deterministic):

| engine | trial-0 | trial-1 | trial-2 | mean Elo |
| --- | --- | --- | --- | --- |
| previous entry | 1279 | 1279 | 1279 | 1279 |
| this revision | 1451 | 1451 | 1279 | 1394 |

Head-to-head against the previous entry over 30 games with alternating
colors and varied openings: 14 wins, 6 draws, 10 losses (56.7% score rate,
about +47 Elo). Trial wall time was 454-525 seconds for 6 games including
the anchors' thinking time, well inside the 1,800-second budget for the
8-game final phase.

## Layout

- `main.py` — the engine (the only file the competition runs)
- `LICENSE` — MIT license
- `.makefun/owner.json` — make.fun ownership record
