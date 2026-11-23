# tiny-chess-4k

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/kkshell/tiny-chess-4k/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/kkshell/tiny-chess-4k/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A 4 KB chess engine in Python: `main.py` (3,514 bytes) is the
whole engine — a 0x88-board alpha-beta search with
quiescence, a transposition table, MVV-LVA + killer +
piece-square move ordering, iterative deepening to depth 8
under a fixed node budget (200,000 nodes a move, 100,000
after 80 plies, 50,000 after 140), null-move pruning
(R=3), and an incremental material + piece-square
evaluation with a bishop-pair bonus and phase-interpolated
endgame king centralisation. Promotions are to queen or
knight only.

It plays through the env at `MAKEFUN_ENV_URL` (`/game`,
`/move`), one game after another until the trial is done.
Every move is derived from the position and a fixed node
budget — no clock, no unseeded randomness — so a replay
plays the same moves.

`main.py` is the `makefun compress` packing of the readable
source, an LZMA payload with its unpacker; it reads,
imports or execs no other file in this repository. The
whole snapshot is at most 8,192 bytes, no file over 4,096.
MIT licence.

Practice trials (6 games each, kit scorer, on the
compressed `main.py`): trial-0 1451, trial-1 1364,
trial-2 1545 Elo — mean 1453, above the 1154 floor and
the house baseline's ~1365.

## Run it

```sh
MAKEFUN_ENV_URL=http://127.0.0.1:18081 python3 -P -s main.py
```

---

<sub>Entered on [make.fun](https://make.fun/?ref=d5a50dzy&utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
