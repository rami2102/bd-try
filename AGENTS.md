# Agent Instructions

This project uses **bd** (beads) for all issue tracking. Do not use markdown TODOs or other task systems.

## Workflow (every session)

```bash
bd ready                                  # Find unblocked work
bd show <id>                              # Read issue context
bd update <id> --status=in_progress       # Claim it
# ... do the work ...
bd close <id> --reason="what was done"    # Complete it
bd sync                                   # Sync to git (run at session end)
```

## Creating Issues

```bash
bd create --title="Fix X" --type=task --priority=2
```

- **Types:** task, bug, feature, epic
- **Priority:** 0=critical, 1=high, 2=medium, 3=low, 4=backlog (use numbers, not words)

## Updating Issues

```bash
bd update <id> --notes "COMPLETED: X. IN PROGRESS: Y. NEXT: Z."
bd update <id> --description "new description"
bd update <id> --design "design notes"
```

**Do NOT use `bd edit`** — it opens $EDITOR and will hang the agent.

## Dependencies

Direction is **"X needs Y"**:
```bash
bd dep add <issue> <depends-on>           # issue depends on depends-on
bd blocked                                # Show blocked issues
```

## Session Completion

Work is NOT complete until `git push` succeeds.

```bash
# 1. Close finished work
bd close <id> --reason="what was done"

# 2. Sync and push
bd sync
git pull --rebase
git push
git status  # MUST show "up to date with origin"
```

- File bd issues for any remaining work before ending
- Run quality gates if code changed (tests, linters)
- NEVER say "ready to push when you are" — YOU must push
