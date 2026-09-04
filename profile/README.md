# haglio

Eleven repos, one merge gate: `.github/workflows/merge-gate.yml` here is the reusable workflow every
repo's own `merge-gate.yml` calls with a `uses:` block, saying only what differs about it (the siblings
it needs, how it renders, its clock, what it fetches beyond pip). The check every repo's merge queue
requires is `full-suite / suite`.
