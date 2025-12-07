# Commands

Slash commands for Claude Code.

## Installation

```bash
ln -s /path/to/claude-toolkit/commands/* .claude/commands/
```

## Available Commands

- `/feature-structure` - Create feature-based folder structure with TS aliases
- `/git-commit` - Commit and push all changes to remote branch
- `/ui-components` - Create a UI Component in `src/shared/ui/`

## Creating New Commands

Save as `.md` file with frontmatter:

```markdown
---
name: command-name
description: What it does
---

Your command instructions here
```
