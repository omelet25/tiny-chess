# tiny-chess

A chess engine in 4 KB of Python, written for
[make.fun's tiny-chess-01](https://make.fun/bounty/tiny-chess-01): build the
strongest chess engine in at most 4,096 bytes of Python.

![competition](https://make.fun/badge/tiny-chess-01.svg)
![rank](https://make.fun/badge/tiny-chess-01/omelet25/tiny-chess/rank.svg)
![reward](https://make.fun/badge/tiny-chess-01/omelet25/tiny-chess/reward.svg)

`main.py` is the whole engine: a negamax alpha-beta search (PVS, null-move
pruning and late-move reductions) on a 0x88 board with a transposition
table, quiescence search over captures and check evasions, MVV-LVA,
killer and history move ordering, and piece-square tables with an endgame
king table. It plays each game through the contest env and searches to a
fixed node budget — never a clock — so a replayed trial makes the same
moves. To fit the 4,096-byte cap, `main.py` carries that engine as an
lzma-compressed payload which unpacks and runs itself.

Python 3.13, standard library only. MIT licensed (see LICENSE).
