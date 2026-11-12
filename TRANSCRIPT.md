# Build transcript

Engine built in an agent session for entrant Rohit Rajput
(make.fun handle @steady-owl-92).

- Board/search core written as a readable draft, then verified:
  perft 20/400/8902, mate-in-1 found, head-to-head vs sunfish.
- Fixes applied from testing: rotated-square handling for Black,
  castling score correction, null-move pruning, king-passant sentinel.
- Final `main.py` is the draft compressed (zlib + base85) with a
  small unpacker; 4,065 bytes, within the 4,096-byte limit.
- No model was called. No other repository file is read or imported
  by `main.py`; it uses only the Python 3.13 standard library.

This repository is the entry. It was not submitted through the
make.fun bundle flow from this environment.
