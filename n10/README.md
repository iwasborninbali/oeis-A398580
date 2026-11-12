# Exact n = 10 count (5 November 2026)

Both programs in `../programs/` completed 512 of 512 shards each and agree in every cell of the size profile T(10,k),
the maximal profile M(10,k) and the addable-point ledger: 7,287,023,194,031 safe subsets (empty set included) and
56,412,888,628 maximal ones. Labelled subsets are counted (rotations and reflections separately).

- `profile-n10.json`: all cells of the three profiles and the aggregate hashes.
- `shards-n10.tar.gz` (SHA-256 `ae416edb0856c8c08c01b781cd2919ab2664ef516b5eb07644b925b3243d6044`): the 1,024 JSON shard
  outputs with their SHA-256 receipts, the plan, the aggregate and the build manifest. Data only, no executables.

Recheck the stored outputs (Python 3.12+, standard library; extract into a new empty directory):

```sh
mkdir n10-check
python3 -I - <<'PY'
import pathlib, tarfile
root = pathlib.Path('n10-check')
with tarfile.open('shards-n10.tar.gz') as archive:
    members = archive.getmembers()
    assert all(m.isfile() and not m.name.startswith('/') and '..' not in pathlib.PurePosixPath(m.name).parts for m in members)
    archive.extractall(root, filter='data')
PY
python3 -I ../programs/collect.py n10-check/run-n10 --require-complete
```

The collector checks every receipt's hash, the build and plan identity, the frontier partition and the per-shard profiles,
then compares the two programs cell by cell. Independent re-enumeration means running the C programs on all shards
(about 104 core-hours for n = 10).
