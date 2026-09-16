# haglio

Eleven repos, one merge gate: `.github/workflows/merge-gate.yml` here is the reusable workflow every
repo's own `merge-gate.yml` calls with a `uses:` block, saying only what differs about it (the siblings
it needs, how it renders, its clock, what it fetches beyond pip). The check every repo's merge queue
requires is `full-suite / suite`.

The same workflow is what gives the three shared libraries a reverse gate. Called with `repo: <a
consumer>`, it clones that consumer at its default branch, installs the pull request's own checkout
into it, and runs *the consumer's* suite -- so `app_support`, `shared_ui` and `player_core` cannot
merge a change no consumer has built against. Those repos require a second check for it
(`consumer / suite`) alongside their own.

On a pull request and in the merge queue, the gate then runs every test the change added or changed
ten more times, on a runner kept busy, and fails the check if any run fails
(`python -m app_support.flake_gate`). It repeats only what the repo's suite collects, so a tree the
suite leaves out, such as `fun_time`'s hidden-desktop tests, is left out here too.
