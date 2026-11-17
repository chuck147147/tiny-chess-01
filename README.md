# tiny-chess-01 entry

An original chess engine in 4,083 bytes of Python (main.py), written for
make.fun's tiny-chess-01 bounty. Standard library only; no model calls.

Design: 0x88 board with incremental Zobrist hashing and material/PST scores;
negamax alpha-beta with PVS, iterative deepening under a deterministic,
phase-scaled node budget (18k-90k nodes per move, never a clock), check
extensions, LMR, a transposition table used across moves for ordering,
quiescence over captures and promotions with check evasions, and a tapered
evaluation (material, piece-square terms from compact formulas, king shelter,
passed pawns) with 30 cp contempt so the engine avoids repetitions when ahead
and seeks them when behind. The source is minified and lzma-packed into
main.py with a Latin-1 literal payload; the unpacked program is the engine.

Local practice results (kit env + scorer, 6 games per instance against
depth-2/3/4 and nodes-100k/250k/500k): Elo 2112 / 1364 / 2112, mean 1863,
against the house baseline's 1364 / 1451 / 1279 (mean 1365) on the same
instances. A re-run of practice trial 1 reproduced the identical games,
move for move.
