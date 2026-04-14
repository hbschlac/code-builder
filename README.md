# code-builder

A Claude Code skill that raises the floor of code quality by generating 5 parallel implementations of the same dev task, self-scoring them against a measurable rubric, and merging the winner.

Auto-activates on coding tasks (build, fix, feature, refactor). For trivial work it does a single pass; for anything meaningful it spawns 5 isolated git worktrees in parallel, scores each draft against a 100-point rubric (correctness, tests, typecheck, lint, minimal diff, no new deps, reuses utilities, conventions, scope), merges the winner, and cherry-picks gaps from the rejected drafts.

Every run logs to `runs/{date}-{slug}.md`. A weekly sync mines those logs + post-merge diffs to update the skill's `## Current learnings` section (hard-capped at 30 bullets) so it gets sharper over time.

## Install

Drop `SKILL.md` into `~/.claude/skills/code-builder/SKILL.md`. That's it — Claude Code will auto-discover it.

To enable the weekly learning sync, also create a scheduled task that runs `code-builder-sync` on your cadence of choice (mine is Sunday 6pm).

## Credit

Built by [@hbschlac](https://github.com/hbschlac). Fork freely.
