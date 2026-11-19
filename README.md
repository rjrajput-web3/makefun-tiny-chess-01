# tiny-chess-01

A chess engine in 4,096 bytes of Python, built for the make.fun
"Build the strongest chess engine in 4 KB of Python" competition.

`main.py` (4,051 bytes) is the whole engine: a 0x88-board engine with a
tapered piece-square-table evaluation (material + classic simplified
tables, interpolated between middlegame and endgame king tables),
principal-variation search with alpha-beta, a Zobrist transposition
table, null-move pruning, quiescence search (captures and promotions;
all evasions when in check, delta-pruned), aspiration windows,
repetition avoidance, and mate-distance pruning. Moves are ordered by
transposition-table move, MVV-LVA captures, killer moves and history.
It searches to a fixed 120,000 nodes a move (deterministic: no clock,
no unseeded randomness) and plays through the make.fun env over HTTP
(`$MAKEFUN_ENV_URL`, routes `/game`, `/move`, `/resign`). Python 3.13,
standard library only. No opening book (the search picks its own
opening moves); no bishop-pair term (ablation showed it cost Elo on
local trials).

Local testing: perft 20/400/8902/197281 from the start position,
97,862 at depth 3 in the Kiwipete position, 43,238 at depth 4 in an
en-passant test position, and make/unmake state (board, hash) verified
over a 60-move walk. Determinism verified: identical moves on two
back-to-back runs (start position, Kiwipete) at the full node budget,
and identical moves and node counts between the readable source and
the packed entry on 8 test positions.
Practice trials (sealed local env + scorer, 2026-11-20):
trial-0 Elo 1451 (4W-0D-2L, spare 444), trial-1 Elo 1364
(3W-1D-2L, spare 339), trial-2 Elo 1451 (4W-0D-2L, spare 310);
mean Elo 1422, above the prior version's 1278 and above the house
baseline. Trial walls ~690-810 s for 6 games; slowest move ~3.5 s,
well under the 10 s move limit (a 200,000-node budget was tried first
and dropped: it lost games on time under CPU contention).

Entry: Rohit Rajput. License: MIT.

Referral code: 9hqpawrx
