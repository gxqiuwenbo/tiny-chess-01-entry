# Sunfish 4KB Chess Engine — tiny-chess-01

A deterministic chess engine in 4 KB of Python. It adapts the Sunfish 2016
search core (120-square board, PST, MTD-bi with null move, killer and TT) to the
make.fun `tiny-chess-01` HTTP env protocol, with a fixed node budget
(`MAXNODES = 80000`) and no wall-clock or model calls.

[![make.fun bounty](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/gxqiuwenbo/tiny-chess-01-entry/rank.svg)](https://make.fun/bounty/tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/gxqiuwenbo/tiny-chess-01-entry/reward.svg)](https://make.fun/bounty/tiny-chess-01)

## Run

Python 3.13, standard library only:

    python main.py

The engine reads the game from `MAKEFUN_ENV_URL` and replies with UCI moves.

## Design notes

- Timing is deliberately absent: every move is chosen from the same node budget, so replayed games follow the same line.
- UCI output is checked against the env's legal-move list before it is sent.
- Castling rights and en-passant squares are mapped into the Sunfish board representation before each search.
- The committed entrypoint is produced by the kit's `compress` command from the readable source bundled with the transcripts.
- No provider key, file read or wall clock is used by the entrypoint.
- All scoring is deterministic, which is what the practice replay checks.

Submissions and prizes: https://make.fun/r/xzgr46f5
