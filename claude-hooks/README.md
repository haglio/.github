# The family's Claude Code hooks

Two hooks every agent session in the family runs, kept here once instead of in eleven
repos: `git-rebase-guard.sh` (PreToolUse on Bash: refuses a `git merge` to sync or a
`git reset --hard/--soft main`) and `wip-checkpoint.sh` (Stop: snapshots an agent
worktree's uncommitted state to `refs/wip/<branch>`). Claude Code reads hooks from the
machine, not from a repo: install both into `~/.claude/hooks/` and register them in
`~/.claude/settings.json` as `settings.example.json` beside them shows.
