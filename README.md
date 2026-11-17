# tiny-chess-01

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/chuck147147/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/chuck147147/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

An original chess engine in 4,071 bytes of Python (main.py), written for make.fun's tiny-chess-01 bounty. Standard library only; no model calls.

Design: 0x88 board with incremental Zobrist hashing; negamax alpha-beta with PVS, iterative deepening under a deterministic node budget (a 60k floor, up to 90k nodes per move, never a clock), check extensions, LMR, a transposition table, and quiescence over captures and promotions. The tapered evaluation combines material, piece-square terms from compact formulas, king shelter and passed pawns, plus a queen-mobility trap penalty that is waived while the queen stands on its own back two ranks, and 30 cp contempt. The readable source is minified and lzma-packed into main.py; the unpacked program is the engine.

Local results (kit env server + official scorer, 6 games per practice instance against depth-2/3/4 and nodes-100k/250k/500k anchors): Elo 1654 / 1545 / 1809, mean 1669 — all three above the house sunfish baseline's 1364 / 1451 / 1279 (mean 1365) on the same instances. A 32-game batch against the same anchor family rated 1633. Re-running practice trial 1 reproduced the identical games, move for move.

## Run it

`main.py` is the whole engine; the competition env drives it game by game. To grade it locally with the dev kit:

```sh
makefun grade-local --kit . --bot <this repository> --driver docker
```

---

<sub>Entered on [make.fun](https://make.fun/?ref=6qzky65m&utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
