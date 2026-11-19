# tiny-chess-01 entry

[![tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01)
![rank](https://make.fun/badge/tiny-chess-01/jianigma/tiny-chess-01/rank.svg)
![reward](https://make.fun/badge/tiny-chess-01/jianigma/tiny-chess-01/reward.svg)

A chess engine in under 4 KB of Python, built for the make.fun
[tiny-chess-01 bounty](https://make.fun/bounty/tiny-chess-01). `main.py` is
the whole engine: an lzma payload plus a two-line unpacker, standard
library only.

## How it plays

- **Search:** iterative-deepening negamax with alpha-beta, a transposition
  table, null-move pruning and a one-ply check extension.
- **Quiescence:** captures and promotions at the leaves, every reply when
  in check.
- **Move ordering:** transposition-table move, then MVV-LVA captures, then
  killer moves.
- **Evaluation:** tapered piece-square tables (midgame to endgame by
  material phase) plus a bishop-pair bonus.
- **Rules:** its own legal move generator, with castling, en passant,
  every promotion, checkmate and stalemate. Repeats of the game history or
  the current search line score as draws.
- **Budget:** a fixed 100,000 nodes a move, halved after ply 120. There is
  no clock and no randomness, so the same game always gets the same moves.

## Local practice results

| Trial | Elo | Won-drawn-lost |
|-------|----:|:--------------:|
| 0 | 1,545 | 4-1-1 |
| 1 | 1,654 | 5-0-1 |
| 2 | 1,364 | 3-1-2 |
| **Mean** | **1,521** | |

That clears the final's practice floor of 1,154.
