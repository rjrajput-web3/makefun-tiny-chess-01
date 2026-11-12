# tiny-chess-01

A chess engine in 4,096 bytes of Python, built for the make.fun
"Build the strongest chess engine in 4 KB of Python" competition.

`main.py` (4,065 bytes) is the whole engine: a sunfish-style 10x12
rotating-board engine with alpha-beta search, a transposition table,
null-move pruning, killer/history move ordering and quiescence search.
It searches to a fixed 100,000 nodes a move (deterministic: no clock,
no unseeded randomness) and plays through the make.fun env over HTTP
(`$MAKEFUN_ENV_URL`, routes `/game`, `/move`, `/resign`).

Local testing: perft 20/400/8902 from the start position, mate-in-1
found, and 1.0/2 vs sunfish at 4,000 nodes a move (draw + draw).
At 100,000 nodes a move it reaches depth 5-6 in the middlegame.

Entry: Rohit Rajput. License: MIT.
