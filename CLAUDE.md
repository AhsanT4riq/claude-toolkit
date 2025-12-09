# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Claude Toolkit** is a collection of reusable Claude Code commands, skills, plugins, and subagents for building and scaffolding projects. This is primarily a template/library repository meant to be cloned and symlinked into other projects rather than deployed as a standalone application.

## Directory Structure

```
claude-toolkit/
├── commands/          # Slash commands for Claude Code (*.md files)
├── skills/           # Custom skills for specialized workflows
├── plugins/          # MCP plugins and integrations
├── subagents/        # AI subagent configurations
├── .claude/          # Claude Code configuration (auto-generated)
└── README.md         # Project documentation
```

## Commands

These are the primary deliverables of this toolkit. Each is a `.md` file with YAML frontmatter that defines a slash command.

### Available Commands

- **`/feature-structure`** (feature-structure.md)
  - Creates a feature-based folder structure for Expo Router projects with TypeScript path aliases
  - Sets up directories for `src/features/`, `src/shared/` with subfolders for components, UI, hooks, utils, etc.
  - Configures `tsconfig.json` with path aliases (@ui/*, @hooks/*, @features/*, etc.)
  - Creates barrel export files for organized imports
  - Use this when scaffolding a new Expo project structure

- **`/setup-nativewind`** (setup-nativewind.md)
  - Installs NativeWind v4 with Tailwind CSS in Expo projects
  - Configures Tailwind, Metro bundler, Babel, and global CSS
  - Takes a `package_manager` argument (bun/npm/pnpm/yarn)
  - Run after feature structure setup but before component creation

- **`/setup-jest`** (setup-jest.md)
  - Installs Jest and React Native Testing Library for Expo projects
  - Adds Jest configuration to package.json
  - Sets up testing infrastructure for the project

- **`/setup-prettier`** (setup-prettier.md)
  - Configures ESLint and Prettier for code linting and formatting
  - Takes a `package_manager` argument (bun/npm/pnpm/yarn)
  - Adds `lint`, `lint:fix`, and `format` scripts
  - Configures import ordering rules (React → Expo → internal aliases → local imports)

- **`/rn-ui-components`** (rn-ui-components.md)
  - Creates production-ready UI components in `src/shared/ui/`
  - Takes arguments: Component name and summary
  - Generates component file, tests, and barrel exports
  - Uses NativeWind for styling with theme support
  - Follows standard variant structure (primary, secondary, success, error, warning, info)

- **`/git-commit`** (git-commit.md)
  - Automates git commit and push workflow
  - Analyzes changes and generates conventional commit messages
  - Validates no sensitive files are committed
  - Note: This project uses a different set of rules than the standard commit format (no Claude Code attribution)

## Command Format

All commands follow this structure:

```markdown
---
name: command-name
description: What it does
args:  # Optional
  - name: arg_name
    description: Description
    required: true
---

## Task
[Instructions for Claude to execute]

## Rules
[Constraints and important guidelines]
```

## Key Architecture Patterns

### Feature-Based Structure
Commands like `/feature-structure` set up projects using this pattern:
- **Features** (`src/features/`) - Isolated feature modules with their own components, hooks, and stores
- **Shared** (`src/shared/`) - Reusable components, utilities, and services used across features
  - `ui/` - UI primitives (Button, Card, Input, etc.)
  - `components/` - Shared React Native components
  - `hooks/` - Custom React hooks
  - `utils/` - Utility functions
  - `services/` - API clients, analytics
  - `store/` - State management (Zustand/Valtio)
  - `types/` - TypeScript interfaces
  - `constants/` - Colors, spacing, config values

### TypeScript Path Aliases
All Expo projects set up with these aliases for clean imports:
```typescript
@ui/Button
@components/Card
@hooks/useAuth
@utils/formatDate
@types/User
@constants
@services/api
@store/authStore
@features/auth
```

### NativeWind Styling
- Projects use NativeWind v4 (Tailwind CSS for React Native)
- All components built with `className` prop supporting Tailwind utilities
- Theme colors referenced from centralized theme configuration
- Supports light/dark mode through NativeWind theme system

### Testing & Linting
- Jest + React Native Testing Library for unit tests
- ESLint with custom import ordering rules
- Prettier for code formatting
- Commands validate setup and provide script aliases

## Common Development Tasks

### When to Use Each Command

1. **Starting a new Expo project:**
   - Run `/feature-structure` to scaffold directory structure and path aliases
   - Run `/setup-nativewind` for styling
   - Run `/setup-jest` for testing
   - Run `/setup-prettier` for linting/formatting

2. **Creating UI components:**
   - Use `/rn-ui-components Button` to create individual components
   - Components automatically go to `src/shared/ui/` with tests

3. **Making commits:**
   - Use `/git-commit` to analyze changes and create conventional commit messages
   - The command validates no sensitive data is included

### Important Notes on Rules

- **No Claude Code Attribution:** Unlike some AI-assisted commits, this toolkit explicitly requires NO "Generated with Claude Code" or "Co-Authored-By" tags in commits
- **Path Alias Support:** Expo SDK 50+ supports path aliases natively—no need for babel-plugin-module-resolver
- **Component Location:** Screens go in `app/` (Expo Router), components go in `src/shared/ui/`
- **Import Ordering:** Custom ESLint rules enforce: React → Expo → internal aliases → local imports
- **Theme System:** NativeWind handles theme-aware styling; components should support both light and dark modes

## Extending the Toolkit

### Adding New Commands

1. Create a `.md` file in `commands/` directory
2. Include YAML frontmatter with name and description
3. Document the task workflow clearly
4. List all important rules and constraints
5. Test the command workflow

### Command Guidelines

- Be explicit about package manager choices (bun/npm/pnpm/yarn) when relevant
- Provide step-by-step instructions that Claude can follow autonomously
- Include validation steps to confirm setup success
- Reference existing patterns in the project
- List hard constraints as "Rules" sections
- Avoid ambiguous instructions—be specific about file paths and configurations

## Git & Version Control

- This is a template repository meant to be cloned into other projects
- Users symlink specific commands/skills they want to use
- Commands provide guidance but don't manage the parent project's git
- The `/git-commit` command can be used standalone for git automation

## Notes for Future Claude Instances

- This repository is primarily a **library of commands and templates**, not a deployed application
- Users interact with this through Claude Code slash commands, not through running scripts directly
- Commands are designed to be used in the context of other projects (like Expo apps)
- The toolkit itself may change as React Native and Expo ecosystems evolve
- Path aliases and import ordering rules follow current Expo and TypeScript best practices (Expo SDK 50+)
