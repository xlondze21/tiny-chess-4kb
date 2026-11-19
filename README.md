# tiny-chess-4kb

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/xlondze21/tiny-chess-4kb/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/xlondze21/tiny-chess-4kb/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A chess engine in 3,593 bytes of Python. Built for [make.fun tiny-chess-01](https://make.fun/bounty/tiny-chess-01) — the strongest engine in 4 KB wins.

## How it plays

`main.py` is a self-contained LZMA-compressed program (Python 3.13 stdlib only). It decompresses its payload and plays over HTTP against the competition environment (`$MAKEFUN_ENV_URL`): `POST /game` for the position, `POST /move` with a UCI move.

The engine is a from-scratch 0x88 board, negamax alpha-beta with:

- iterative deepening to a fixed 80,000-node budget (deterministic, no clock)
- transposition table with Zobrist hashing
- quiescence search (captures and promotions, stand-pat + delta pruning)
- move ordering: TT move, MVV-LVA captures, killer moves, history heuristic
- null-move pruning, late move reductions, check extensions
- tapered piece-square evaluation (midgame/endgame) plus bishop pair

## Run it

```sh
MAKEFUN_ENV_URL=http://127.0.0.1:8766 python3 main.py
```

Deterministic: the same position always yields the same move.

## License

MIT. See LICENSE.
