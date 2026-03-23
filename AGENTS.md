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

## Issue Tracking with bd (beads)

**IMPORTANT**: This project uses **bd (beads)** for ALL issue tracking. Do NOT use markdown TODOs, task lists, or other tracking methods.

### Why bd?

- Dependency-aware: Track blockers and relationships between issues
- Git-friendly: Auto-syncs to JSONL for version control
- Agent-optimized: JSON output, ready work detection, discovered-from links
- Prevents duplicate tracking systems and confusion

### Quick Start

**Check for ready work:**

```bash
bd ready --json
```

**Create new issues:**

```bash
bd create "Issue title" -t bug|feature|task -p 0-4 --json
bd create "Issue title" -p 1 --deps discovered-from:bd-123 --json
```

**Claim and update:**

```bash
bd update bd-42 --status in_progress --json
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
2. **Claim your task**: `bd update <id> --status in_progress`
3. **Work on it**: Implement, test, document
4. **Discover new work?** Create linked issue:
   - `bd create "Found bug" -p 1 --deps discovered-from:<parent-id>`
5. **Complete**: `bd close <id> --reason "Done"`
6. **Commit together**: Always commit the `.beads/issues.jsonl` file together with the code changes so issue state stays in sync with code state

### Auto-Sync

bd automatically syncs with git:

- Exports to `.beads/issues.jsonl` after changes (5s debounce)
- Imports from JSONL when newer (e.g., after `git pull`)
- No manual export/import needed!

### MCP Server (Recommended)

If using Claude or MCP-compatible clients, install the beads MCP server:

```bash
pip install beads-mcp
```

Add to MCP config (e.g., `~/.config/claude/config.json`):

```json
{
  "beads": {
    "command": "beads-mcp",
    "args": []
  }
}
```

Then use `mcp__beads__*` functions instead of CLI commands.

### Managing AI-Generated Planning Documents

AI assistants often create planning and design documents during development:

- PLAN.md, IMPLEMENTATION.md, ARCHITECTURE.md
- DESIGN.md, CODEBASE_SUMMARY.md, INTEGRATION_PLAN.md
- TESTING_GUIDE.md, TECHNICAL_DESIGN.md, and similar files

**Best Practice: Use a dedicated directory for these ephemeral files**

**Recommended approach:**

- Create a `history/` directory in the project root
- Store ALL AI-generated planning/design docs in `history/`
- Keep the repository root clean and focused on permanent project files
- Only access `history/` when explicitly asked to review past planning

**Example .gitignore entry (optional):**

```gitignore
# AI planning documents (ephemeral)
history/
```

**Benefits:**

- Clean repository root
- Clear separation between ephemeral and permanent documentation
- Easy to exclude from version control if desired
- Preserves planning history for archeological research
- Reduces noise when browsing the project

### Important Rules

- Use bd for ALL task tracking
- Always use `--json` flag for programmatic use
- Link discovered work with `discovered-from` dependencies
- Check `bd ready` before asking "what should I work on?"
- Store AI planning docs in `history/` directory
- Do NOT create markdown TODO lists
- Do NOT use external issue trackers
- Do NOT duplicate tracking systems
- Do NOT clutter repo root with planning documents

For more details, see `README.md` and project docs.

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
