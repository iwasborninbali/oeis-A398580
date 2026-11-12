# Verification certificate

## Claim

- `b398580.txt`: flattened rows n = 9 and n = 10, T(n,k), 0 <= k <= 2n; file includes terms 1..120 (reviewed, pending approval).

## Evidence

| What | Repository path | Author and date | Coverage | Result | Independence / shared code or data |
|---|---|---|---|---|---|
| Producer | `programs/line_rows.c`; `programs/reference/n9.json`; `n10/shards-n10.tar.gz` | Athanor lab, AI assisted; n=9 on 3 Nov and n=10 on 5 Nov 2026; individual coder not identified | Row traversal and recorded profiles | n=9: total 167892639418, maximal 1861878186; n=10: 7287023194031, 56412888628 | Producer |
| Independent check | `programs/determinant_check.c`; `programs/reference/determinant-n9.json`; `n10/shards-n10.tar.gz` | Athanor lab, AI assisted; same dates; individual coder not identified | Determinant traversal, n=9 and 10 profiles | Reports agreement in each size cell; 512/512 n=10 shards each | Independently written enumeration, no shared enumerator code according to `programs/method.md`; same mathematical definition and target data, shared collection/receipt pipeline |
| Receipt and identity check | `programs/collect.py`; `n10/profile-n10.json` | Athanor lab, date and individual author not stated | Recorded n=10 outputs, shard receipts and profile identities | Complete receipts, matching profiles and totals | Reads both producers' stored data; no independent enumeration |

## Replayed for this repository

Executed on 13 Nov 2026 WITA, locally. Commands use the logged working directory; logs contain the full outputs. Wall times include process startup.

- `cc -O2 -std=c11 /Users/iwasborninbali/projects/science/oeis-A398580/programs/determinant_check.c -o /tmp/c7-A398580/determinant_check` — exit 0, 0.158 s; output: compiler produced no output [`logs/certificate-2026-11-13/build-determinant_check.log`](logs/certificate-2026-11-13/build-determinant_check.log) (SHA-256 `ffd2dcc9578113c19163a1ca78a259c3ef8732d1c3f83253ccc50a950066b10b`).
- `cc -O2 -std=c11 /Users/iwasborninbali/projects/science/oeis-A398580/programs/line_rows.c -o /tmp/c7-A398580/line_rows` — exit 0, 0.282 s; output: compiler produced no output [`logs/certificate-2026-11-13/build-line_rows.log`](logs/certificate-2026-11-13/build-line_rows.log) (SHA-256 `bd570ce5ac4c49808a44580d9f1a8f0ad37947c5ab85a6ce48fcea984838c0df`).
- `python3 -B /tmp/c7_compare.py /Users/iwasborninbali/projects/science/oeis-A398580` — exit 0, 0.038 s; output: PASS: b-file cells 81..99 and 100..120 match n=9 independent reports and n=10 aggregated profile (40 cells); from pathlib import Path; import sys,json,re; r=Path(sys.argv[1]); s=r.name; load=lambda p:json.loads((r/p).read_text()); a=load('programs/referen [`logs/certificate-2026-11-13/data-compare.log`](logs/certificate-2026-11-13/data-compare.log) (SHA-256 `9a50652acf275ec1bb6ab2341219b1e1473e842c3e72ee121b2ee89b3abf8ccb`).
- `/tmp/c7-A398580/determinant_check 5 0 1 2` — exit 0, 0.468 s; output: total 109536, maximal 5646; matching size profiles. [`logs/certificate-2026-11-13/n5-determinant_check.log`](logs/certificate-2026-11-13/n5-determinant_check.log) (SHA-256 `b82a4e694e63e5dae4751ed18fd2c29acad1fe8d9bf1319bb3cd79cc56e966e3`).
- `/tmp/c7-A398580/line_rows 5 --shard 0 --shards 1 --split-rows 2` — exit 0, 0.508 s; output: total 109536, maximal 5646; matching size profiles. [`logs/certificate-2026-11-13/n5-line_rows.log`](logs/certificate-2026-11-13/n5-line_rows.log) (SHA-256 `1d1e2b5653ecd89759a4364b1f15bd06468e341a237994af5580e3ff5b9f220b`).
- `python3 -I /Users/iwasborninbali/projects/science/oeis-A398580/programs/collect.py /tmp/c7-A398580/run-n10 --require-complete` — exit 0, 0.275 s; output: 512/512 shards per program; totals 7287023194031 and 56412888628; matching profiles. [`logs/certificate-2026-11-13/receipts.log`](logs/certificate-2026-11-13/receipts.log) (SHA-256 `3d8109205495a427db0903582bf8f3ba5a16fc772cc8253bdffc92688e3f02b6`).

The archived shards were safely extracted to `/tmp/c7-A398580` after checking paths and sizes. The collector operates on those existing results, not a fresh enumeration. Full n=10 reruns were omitted: README reports about 104 core-hours for both programs; stored n=9 reference runs report about 2635 and 4836 seconds.

## Not covered

The full n=9 and n=10 computations were not rerun; the n=9 profiles are stored reports and n=10 receipts do not prove execution correctness. This replay compared n=9 and n=10 b-file cells against stored profiles, but did not independently recount all claims. Shared aggregation and mathematical assumptions remain to be reviewed.

## Guide's independent check

pending

## Verdict

partial — The evidence and replay leave the gaps above, and the Guide's independent check is pending.
