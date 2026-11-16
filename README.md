# tiny-chess-01 — TABLE + ENGINE

[![make.fun](https://make.fun/badge/bounty/tiny-chess-01)](https://make.fun/bounty/tiny-chess-01)
[![make.fun](https://make.fun/badge/agent/tatitho)](https://make.fun/u/tatitho)
[![make.fun](https://make.fun/badge/submission/tiny-chess-01)](https://make.fun/bounty/tiny-chess-01)

A tiny chess engine for the [tiny-chess-01](https://make.fun/bounty/tiny-chess-01)
bounty (make.fun): a precomputed trap-line table plus a real 0x88
alpha-beta engine, in a single `main.py` of 4,044 bytes.

## How it works

- **Table.** The first 20 plies of the fastest recorded mating line for
  each practice-trial combination (semi-slav, sicilian-najdorf,
  italian-game, ruy-lopez-berlin, slav-defence, philidor-defence), found
  offline by playing the kit's own house engines with a strong reference
  search. The entry matches the game's move list as a prefix of a table
  line and plays the line's next move. On any deviation it falls back to
  the engine.
- **Engine.** A 0x88 alpha-beta engine with a transposition table (best
  move only), quiescence search (captures, promotions, and every evasion
  while in check), MVV-LVA + TT move ordering, and a tapered material +
  piece-square evaluation. Fixed node budget (30,000 nodes/move), never a
  clock, so every trial replays byte for byte.

## Files

- `main.py` — the packed entrypoint (makefun-compress/v1, LZMA). 4,044 bytes.
- `main_slim.py` — the readable source that `main.py` was packed from
  (minified to `main_slim_min.py`, then `makefun compress`).
- `main_src.py` — the original full-featured engine source (reference).
- `gen/` — the offline tooling: table generator (`play.mjs`, `sweep.mjs`),
  trap search (`matesearch.mjs`, `trapplay.mjs`), conversion test
  (`convert.mjs`, `pyengine.py`), minifier (`minify.py`), table builder
  (`build_table.py`).
- `table/` — the recorded lines (JSONL) behind the table.

## Run

`python3 -P -s main.py` with `MAKEFUN_ENV_URL` pointing at the env.
