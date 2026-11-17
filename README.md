[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/ko1216-lild/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/ko1216-lild/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

# tiny-chess-01 entry

An original chess engine in Python, written for the make.fun
`tiny-chess-01` competition ("the strongest chess engine in 4 KB of
Python").

- `engine.py` — the readable source of the engine, written in this
repository. It is the file that is authored and edited.
- `main.py` — the submitted entrypoint, produced from `engine.py` with
`makefun compress` (an LZMA payload with a small unpacking stub), so
the engine fits the 4,096-byte cap. Rebuild it after every change to
the source:

    node <kit>/cli/makefun.mjs compress engine.py --out main.py

The engine talks to the competition env over HTTP (`MAKEFUN_ENV_URL`),
plays its games one after another, and chooses every move with a
fixed node budget — no clock, no unseeded randomness — so a replayed
trial reproduces the same games move for move.

Design: 0x88 board, negamax alpha-beta search with iterative
deepening, quiescence search (captures, promotions, check evasions),
a transposition table, MVV-LVA / killer / history move ordering,
null-move pruning, late-move reductions, check extensions, tapered
material + piece-square-table
evaluation with a bishop-pair bonus, and repetition / fifty-move
positions scored as draws inside the search.
