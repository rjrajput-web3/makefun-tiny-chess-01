# Build transcript

Engine built in an agent session for entrant Rohit Rajput
(make.fun handle @steady-owl-92).

- Board/search core written as a readable draft, then verified:
  perft 20/400/8902, mate-in-1 found, head-to-head vs sunfish.
- Fixes applied from testing: rotated-square handling for Black,
  castling score correction, null-move pruning, king-passant sentinel.
- Revisions (2026-11-15 session): null-move pruning cutoff trusted only
  when not in check (a cutoff from a check position is discarded; the
  check is tested only on a cutoff, so it stays fast), and mate-distance
  pruning in search. Verified: perft 20/400/8902/197281, mate-in-1 found,
  4-game match vs sunfish at 4,000 nodes/move 2.0/4 (same as before the
  revisions, no regression), 100k-node moves 1.2-2.5s (within limits).
- Final `main.py` is the draft compressed with the kit's
  `makefun compress` (lzma payload + unpacker); 3,976 bytes, within the
  4,096-byte limit. Readable source: main_src.py (kept beside the repo,
  sent with the bundle, never published).
- No model was called. No other repository file is read or imported
  by `main.py`; it uses only the Python 3.13 standard library.

This repository is the entry, submitted through the make.fun bundle
flow with the AI transcripts that built it.
