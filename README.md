# tiny-chess-01

A chess engine in 4,096 bytes of Python, built for the make.fun
"Build the strongest chess engine in 4 KB of Python" competition.

`main.py` (3,780 bytes) is the whole engine: a 0x88-board engine with a
tapered PeSTO evaluation (material + piece-square tables, interpolated
between middlegame and endgame), principal-variation search with
alpha-beta, a Zobrist transposition table, null-move pruning, late-move
reductions, check extensions, futility and mate-distance pruning, and
quiescence search (captures; all moves when in check). Moves are ordered
by transposition-table move, MVV-LVA captures, killer moves and history.
It searches to a fixed 120,000 nodes a move (deterministic: no clock,
no unseeded randomness) and plays through the make.fun env over HTTP
(`$MAKEFUN_ENV_URL`, routes `/game`, `/move`, `/resign`). Python 3.13,
standard library only. Two small opening-book lines (slav-defence,
philidor-defence) cover known weak spots; no bishop-pair term (ablation
showed it cost Elo on local trials).

Local testing: perft 20/400/8902 from the start position, 97,862 at
depth 3 in the Kiwipete position, mate-in-1 found, and make/unmake
state (board, hash, eval) verified over hundreds of random moves.
Determinism verified: identical moves on two back-to-back runs
(start position, Kiwipete), and a full practice trial-0 re-run
reproduced games 1-5 exactly.
Practice trials (sealed local env + scorer, 2026-11-19):
trial-0 Elo 1364 (3W-1D-2L, spare 303), trial-1 Elo 1191
(2W-1D-3L, spare 215), trial-2 Elo 1279 (2W-2D-2L, spare 198);
mean Elo 1278, above the 1154 practice floor and above the prior
entry's 1191. Trial walls ~700-810 s for 6 games.

Entry: Rohit Rajput. License: MIT.

Referral code: 9hqpawrx
