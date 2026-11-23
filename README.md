# tiny-chess-01 — a 4 KB chess engine

`main.py` (3,514 bytes) is the whole engine: a 0x88-board
alpha-beta search with quiescence, a transposition table,
MVV-LVA + killer + piece-square move ordering, iterative
deepening to depth 8 under a fixed node budget
(200,000 nodes a move, 100,000 after 80 plies, 50,000 after
140), null-move pruning (R=3), and an incremental
material + piece-square evaluation with a bishop-pair
bonus and phase-interpolated endgame king centralisation.
Promotions are to queen or knight only.

It plays through the env at `MAKEFUN_ENV_URL` (`/game`,
`/move`), one game after another until the trial is done.
Every move is derived from the position and a fixed node
budget — no clock, no unseeded randomness — so a replay
plays the same moves.

## Size

- `main.py`: at most 4,096 bytes as committed. It is the
  `makefun compress` packing of the readable source, an
  LZMA payload with its unpacker; it reads, imports or
  execs no other file in this repository.
- The whole snapshot (this README, LICENSE, `main.py`)
  is at most 8,192 bytes, no file over 4,096. MIT licence.

## Run it

    MAKEFUN_ENV_URL=http://127.0.0.1:18081 python3 -P -s main.py

Python 3.13, standard library only. Practice trials
(6 games each, kit scorer, on the compressed `main.py`):
trial-0 1451, trial-1 1364, trial-2 1545 Elo — mean 1453,
above the 1154 floor and the house baseline's ~1365.
