# tiny-chess-01

A chess engine in 4,096 bytes of Python, built for the make.fun
"Build the strongest chess engine in 4 KB of Python" competition.

`main.py` (3,469 bytes) is the whole engine: a 0x88-board engine with a
tapered PeSTO evaluation (material + piece-square tables, interpolated
between middlegame and endgame), principal-variation search with
alpha-beta, a Zobrist transposition table, null-move pruning, late-move
reductions, check extensions, futility and mate-distance pruning, and
quiescence search (captures; all moves when in check). Moves are ordered
by transposition-table move, MVV-LVA captures, killer moves and history.
It searches to a fixed 120,000 nodes a move (deterministic: no clock,
no unseeded randomness) and plays through the make.fun env over HTTP
(`$MAKEFUN_ENV_URL`, routes `/game`, `/move`, `/resign`). Python 3.13,
standard library only.

Local testing: perft 20/400/8902 from the start position, 97,862 at
depth 3 in the Kiwipete position, mate-in-1 found, and make/unmake
state (board, hash, eval) verified over hundreds of random moves.
Practice trial-0 (sealed local env + scorer): Elo 997, 1 win, 1 draw,
4 losses, 57 spare plies.

Entry: Rohit Rajput. License: MIT.

Referral code: 9hqpawrx
