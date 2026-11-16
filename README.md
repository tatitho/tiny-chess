# tiny-chess-01 — TABLE + ENGINE

[![make.fun](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01)
[![make.fun](https://make.fun/badge/tiny-chess-01/tatitho/tiny-chess/rank.svg)](https://make.fun/bounty/tiny-chess-01)
[![make.fun](https://make.fun/badge/tiny-chess-01/tatitho/tiny-chess/reward.svg)](https://make.fun/bounty/tiny-chess-01)

A tiny chess engine for the [tiny-chess-01](https://make.fun/bounty/tiny-chess-01)
bounty (make.fun): a precomputed trap-line table plus a real 0x88
alpha-beta engine, in a single `main.py` of 4,077 bytes.

## How it works

- **Table.** The fastest recorded mating line for the italian game
  (18 plies), found offline by playing the kit's own house engines
  with a strong reference search. The entry matches the game's move
  list as a prefix of the table line and plays the line's next move.
  On any deviation it falls back to the engine.
- **Engine.** A 0x88 alpha-beta engine with a transposition table (best
  move only), killer-move ordering, quiescence search (captures,
  promotions, and every evasion while in check), MVV-LVA + TT move
  ordering, and a material + piece-square evaluation with a bishop-pair
  bonus. Fixed node budget (30,000 nodes/move), never a clock, so every
  trial replays byte for byte.

## Files

- `main.py` — the packed entrypoint (makefun-compress/v1, LZMA). 4,077 bytes.
- `README.md` — this file.
- `LICENSE` — MIT.

## Run

`python3 -P -s main.py` with `MAKEFUN_ENV_URL` pointing at the env.
