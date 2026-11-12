# OEIS A398580: triangle of k-element no-three-in-line subsets of the n X n grid

[A398580](https://oeis.org/A398580): the triangle T(n,k), 0 <= k <= 2n, read by rows: the number of k-element subsets of the n X n grid with no three collinear points. Row sums are A398172.

This repository holds the programs, data and checks behind the terms we contributed to this sequence. It concerns
A398580 only; the related sequences have their own repositories ([oeis-A398172](https://github.com/iwasborninbali/oeis-A398172), [oeis-A398184](https://github.com/iwasborninbali/oeis-A398184)).

Rows 1–8 were in the entry (rows 1–7 from the original submission, row 8 from Sean A. Irvine); rows 9 and 10 are our contribution (b-file with terms 1..120, submitted 12 Nov 2026). Row 10:

T(10,k), k = 0..20: 1, 100, 4950, 157252, 3507553, 56978440, 682686652, 6030207624, 38914424892, 180609371888, 589914482452, 1318594983248, 1947408104470, 1818668844204, 1016152523214, 316379847124, 49986648002, 3526996436, 92734158, 690236, 1135.

## How the terms were computed

- **n ≤ 7** (September 2026): two independent exhaustive Python programs (`python/`), sharing no code.
- **n = 8**: first computed by Sean A. Irvine (September 2026); reproduced here by both C programs below.
- **n = 9** (3 November 2026) and **n = 10** (5 November 2026): two independently written exhaustive C programs in
  [`programs/`](programs/) (method in `programs/method.md`):
  - `line_rows.c`: a row-by-row search over row patterns (empty, one or two points), with occupancy counters on every
    lattice line through at least three grid points, analytic completion of the last row and a justified reflection reduction;
  - `determinant_check.c`: a point-by-point traversal that tests every triple with an integer determinant and uses no
    symmetry weights (adapted from the September program `tri.c`, credited as such; `original_*.c` are the earlier versions).
  Both split the search by the first two rows into deterministic frontiers; frontier i goes to shard i mod S, so every
  subset is counted in exactly one shard. For n = 10 each program completed 512 of 512 shards and they agree in every cell
  (see [`n10/`](n10/)). Through n = 9 they also match `programs/reference/`.

Build and run one shard (any C compiler):

```sh
cd programs && ./build.sh
./line_rows N --shard i --shards S --split-rows R
./determinant_check N i S R
```

## Contents

| Path | What |
|---|---|
| [`b398580.txt`](b398580.txt) | rows 1–10 flattened (terms 1..120) |
| [`python/triangle_program.py`](python/triangle_program.py) | the short September program for rows 1–5 (also in the entry) |
| [`programs/`](programs/) | the two exhaustive C programs, build script, collector and auditor, method, small-n references |
| [`n10/`](n10/) | the n = 10 profile and the 1,024 shard outputs with receipts, and how to recheck them |

## Author and licence

Aleksei Kudriashov (ORCID 0009-0006-8885-5338), Athanor lab, with AI assistance (OpenAI Codex cores; Claude Code as the
lab's guide). Code: MIT; data and text: CC BY 4.0 (see `LICENSE.md`). The same computation is also part of the lab's
broader archive [no3-results](https://github.com/iwasborninbali/no3-results).
