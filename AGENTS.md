## Project Overview

This repository contains `French Telex`, a custom [Keyman](https://keyman.com/) keyboard for typing French with Telex-style postfix sequences on macOS, Windows, and Linux.

The project is intentionally small and source-driven:

- `source/french_telex.kmn` is the main keyboard source.
- `source/french_telex.kps` contains the package source metadata.
- `source/readme.htm` and `source/welcome.htm` are package-facing HTML docs.
- `french_telex.kpj` is the Keyman Developer project file.
- `README.md` and `README.fr.md` document installation and typing behavior.
- Build output is expected under `build/`, with the package installed from `build/french_telex.kmp`.

The keyboard is designed for users who already have Vietnamese Telex muscle memory and want to type French accents without switching to a positional French layout.

Common typing rules documented in this repo:

- Acute accents via postfix `s`
- Grave accents via postfix `f`
- Circumflex via doubled vowels
- Diaeresis via postfix `w`
- Cedilla via `cw`
- Ligatures via `o/` and `a/`
- Literal trigger sequences escaped with backslash

Typical local workflow:

```bash
kmc build /Users/kylepham/Code/keyman-french-telex
```

If you change keyboard rules or packaging content, update the relevant docs so the README, package HTML, and keyboard behavior stay aligned.

<!-- BEGIN BEADS INTEGRATION v:1 profile:full hash:f65d5d33 -->
## Issue Tracking with bd (beads)

**IMPORTANT**: This project uses **bd (beads)** for ALL issue tracking. Do NOT use markdown TODOs, task lists, or other tracking methods.

### Why bd?

- Dependency-aware: Track blockers and relationships between issues
- Git-friendly: Dolt-powered version control with native sync
- Agent-optimized: JSON output, ready work detection, discovered-from links
- Prevents duplicate tracking systems and confusion

### Quick Start

**Check for ready work:**

```bash
bd ready --json
```

**Create new issues:**

```bash
bd create "Issue title" --description="Detailed context" -t bug|feature|task -p 0-4 --json
bd create "Issue title" --description="What this issue is about" -p 1 --deps discovered-from:bd-123 --json
```

**Claim and update:**

```bash
bd update <id> --claim --json
bd update bd-42 --priority 1 --json
```

**Complete work:**

```bash
bd close bd-42 --reason "Completed" --json
```

### Issue Types

- `bug` - Something broken
- `feature` - New functionality
- `task` - Work item (tests, docs, refactoring)
- `epic` - Large feature with subtasks
- `chore` - Maintenance (dependencies, tooling)

### Priorities

- `0` - Critical (security, data loss, broken builds)
- `1` - High (major features, important bugs)
- `2` - Medium (default, nice-to-have)
- `3` - Low (polish, optimization)
- `4` - Backlog (future ideas)

### Workflow for AI Agents

1. **Check ready work**: `bd ready` shows unblocked issues
2. **Claim your task atomically**: `bd update <id> --claim`
3. **Work on it**: Implement, test, document
4. **Discover new work?** Create linked issue:
   - `bd create "Found bug" --description="Details about what was found" -p 1 --deps discovered-from:<parent-id>`
5. **Complete**: `bd close <id> --reason "Done"`

### Quality

- Use `--acceptance` and `--design` fields when creating issues
- Use `--validate` to check description completeness

### Lifecycle

- `bd defer <id>` / `bd supersede <id>` for issue management
- `bd stale` / `bd orphans` / `bd lint` for hygiene
- `bd human <id>` to flag for human decisions
- `bd formula list` / `bd mol pour <name>` for structured workflows

### Auto-Sync

bd automatically syncs via Dolt:

- Each write auto-commits to Dolt history
- Use `bd dolt push`/`bd dolt pull` for remote sync
- No manual export/import needed!

### Important Rules

- ✅ Use bd for ALL task tracking
- ✅ Always use `--json` flag for programmatic use
- ✅ Link discovered work with `discovered-from` dependencies
- ✅ Check `bd ready` before asking "what should I work on?"
- ❌ Do NOT create markdown TODO lists
- ❌ Do NOT use external issue trackers
- ❌ Do NOT duplicate tracking systems

For more details, see README.md and docs/QUICKSTART.md.

## Session Completion

**When ending a work session**, you MUST complete ALL steps below. Work is NOT complete until `git push` succeeds.

**MANDATORY WORKFLOW:**

1. **File issues for remaining work** - Create issues for anything that needs follow-up
2. **Run quality gates** (if code changed) - Tests, linters, builds
3. **Update issue status** - Close finished work, update in-progress items
4. **PUSH TO REMOTE** - This is MANDATORY:
   ```bash
   git pull --rebase
   bd dolt push
   git push
   git status  # MUST show "up to date with origin"
   ```
5. **Clean up** - Clear stashes, prune remote branches
6. **Verify** - All changes committed AND pushed
7. **Hand off** - Provide context for next session

**CRITICAL RULES:**

- Work is NOT complete until `git push` succeeds
- NEVER stop before pushing - that leaves work stranded locally
- NEVER say "ready to push when you are" - YOU must push
- If push fails, resolve and retry until it succeeds

<!-- END BEADS INTEGRATION -->

### Project-Specific Beads Notes

- For automation in this repo, prefer `--json` on `bd` commands.
- If `bd` reports false git-repo errors under Codex, use `tools/bd-safe ...` so Beads bypasses the AI guard `git` wrapper on `PATH`.
- Store AI-generated planning and design docs in `history/` to keep the repo root clean.
- If `.beads/issues.jsonl` changes alongside code, commit it with the related code changes.

## Overall rule

- Delete unused or obsolete files when your changes make them irrelevant (refactors, feature removals, etc.), and revert files only when the change is yours or explicitly requested. If a git operation leaves you unsure about other agents' in-flight work, stop and coordinate instead of deleting.
- **Before attempting to delete a file to resolve a local build or packaging failure, stop and ask the user.** Other agents are often editing adjacent files; deleting their work to silence an error is never acceptable without explicit approval.
- NEVER edit `.env` or any environment variable files. This repo is not expected to need them.
- Coordinate with other agents before removing their in-progress edits; don't revert or delete work you didn't author unless everyone agrees.
- Moving or renaming files is allowed.
- ABSOLUTELY NEVER run destructive git operations (for example `git reset --hard`, `rm`, `git checkout`, or `git restore` to an older commit) unless the user gives an explicit, written instruction in the task thread.
- Never use `git restore` or similar commands to revert files you didn't author.
- Always double-check `git status` before any commit.
- Keep commits atomic: commit only the files you touched and list each path explicitly.
- Quote any git paths containing brackets or parentheses so the shell does not treat them as globs or subshells.
- When running `git rebase`, avoid opening editors by using `GIT_EDITOR=:` and `GIT_SEQUENCE_EDITOR=:` or `--no-edit`.
- Never amend commits unless you have explicit written approval in the task thread.
- Run long-running tasks with `tmux` when appropriate, and monitor logs regularly.
- Do not define functions or variables whose names start with an underscore unless they are Python dunder methods.
- Before changing keyboard behavior, read this entire file and the repo README so packaging, docs, and examples remain consistent.
- When editing keyboard behavior, prefer validating with a local `kmc build /Users/kylepham/Code/keyman-french-telex` before wrapping up.

## Agent Coordination

If you are working as one of multiple agents on this repository:

- Introduce yourself to the other agents before taking large or overlapping tasks.
- Coordinate ownership of files before editing shared areas like `source/french_telex.kmn`, package docs, or top-level READMEs.
- Check for new messages at the start and end of your session and after major updates.
- Share concise status updates when you begin, when scope changes, and when you finish.

Use any available agent-mail or coordination tooling in the current environment if it exists; otherwise coordinate through the user-visible task thread.
