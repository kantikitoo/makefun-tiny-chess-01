# tiny-chess-01: a 4 KB chess engine

A chess engine in 4,080 bytes of Python (`main.py`, lzma-packed source with
a base85 payload and its unpacker). Original code, written for make.fun's
tiny-chess-01 bounty.

## Engine

- 0x88 board, alpha-beta negamax with iterative deepening to a fixed
  node budget (30,000 nodes/move: deterministic, no clock, no randomness)
- Quiescence over captures, promotions and check evasions, with delta
  pruning; transposition table keyed by the position tuple, MVV-LVA
  ordering, null-move pruning and late-move reductions
- Evaluation: material + formula piece-square tables, tapered king safety
  by game phase; repetition inside the search scores 0
- Talks to the env only (`MAKEFUN_ENV_URL`): `POST /game`, `POST /move`.
  It calls no model and no other service.

## Run it

```sh
MAKEFUN_ENV_URL=<env url> python3 main.py
```

## Size

`main.py` is 4,080 bytes (cap 4,096). The whole tree is under 8,192 bytes.
MIT licensed, see LICENSE.
