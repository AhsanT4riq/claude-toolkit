# Claude Code Toolkit

A collection of production-ready Claude Code commands and utilities for building modern applications with AI assistance. Perfect for Expo/React Native projects, web development, and general development workflows.

![License](https://img.shields.io/badge/license-MIT-blue)
![Node Version](https://img.shields.io/badge/node-18%2B-green)

## What is Claude Code?

[Claude Code](https://claude.com/claude-code) is an AI-powered development environment from Anthropic. This toolkit extends Claude Code with reusable slash commands and utilities to accelerate common development tasks.

## Features

✨ **Smart Commands** - Slash commands that automate repetitive development tasks
🛠️ **Project Scaffolding** - Quickly set up new projects with proper structure and configuration
🎨 **Component Generation** - Generate production-ready UI components with testing
🧪 **Testing Setup** - Configure Jest and testing libraries automatically
📝 **Code Quality** - Integrated linting, formatting, and commit workflows
🚀 **Zero Configuration** - Works out of the box with sensible defaults

## Quick Start

### 1. Clone the toolkit

```bash
git clone https://github.com/AhsanT4riq/claude-toolkit .claude-toolkit
```

### 2. Symlink commands to your project

Choose which components you want to use:

```bash
# All commands
ln -s $(pwd)/.claude-toolkit/commands/* .claude/commands/

# Or individual commands
ln -s $(pwd)/.claude-toolkit/commands/setup-nativewind.md .claude/commands/
ln -s $(pwd)/.claude-toolkit/commands/setup-prettier.md .claude/commands/
ln -s $(pwd)/.claude-toolkit/commands/rn-ui-components.md .claude/commands/
```

### 3. Use in Claude Code

Open Claude Code in your project and run:

```
/setup-nativewind bun
/feature-structure
/setup-prettier bun
```

## Available Commands

### Project Setup

- **`/feature-structure`** - Create a feature-based folder structure with TypeScript path aliases
  - Sets up `src/features/` and `src/shared/` with organized subdirectories
  - Configures tsconfig.json with intelligent path aliases
  - Perfect for Expo Router projects

- **`/setup-nativewind`** - Install and configure NativeWind (Tailwind CSS for React Native)
  - Configures Tailwind CSS with Expo projects
  - Sets up Metro bundler and Babel configuration
  - Argument: package manager (bun/npm/pnpm/yarn)

- **`/setup-prettier`** - Configure ESLint and Prettier with import ordering
  - Adds linting and formatting with enforced import order
  - Creates configuration files with sensible defaults
  - Argument: package manager (bun/npm/pnpm/yarn)

- **`/setup-jest`** - Install Jest and React Native Testing Library
  - Configures testing infrastructure for Expo projects
  - Sets up Jest with proper transformations for React Native

### Component Development

- **`/rn-ui-components`** - Generate production-ready UI components
  - Creates component file, tests, and barrel exports
  - Uses NativeWind for styling with theme support
  - Includes WCAG AA accessibility features
  - Arguments: Component name and summary

### Git Workflows

- **`/git-commit`** - Automate commit and push workflow
  - Analyzes changes and generates conventional commit messages
  - Validates no sensitive files are included
  - Handles first-time branch pushes

## Project Structure

```
claude-toolkit/
├── commands/              # Slash commands (the main content)
│   ├── feature-structure.md
│   ├── setup-nativewind.md
│   ├── setup-prettier.md
│   ├── setup-jest.md
│   ├── rn-ui-components.md
│   └── git-commit.md
├── CLAUDE.md             # Claude Code guidance for this repo
└── README.md            # This file
```

## Use Cases

### Starting a New Expo Project

```bash
# 1. Create project structure
/feature-structure

# 2. Set up styling with NativeWind
/setup-nativewind bun

# 3. Configure linting and formatting
/setup-prettier bun

# 4. Set up testing
/setup-jest

# 5. Start building components
/rn-ui-components Button
/rn-ui-components Card
```

### Adding to Existing Project

Symlink only the commands you need. Commands are independent and won't conflict with existing setups.

### CI/CD Integration

Commands are designed for interactive use with Claude Code, not for automation scripts. However, you can reference the command documentation for manual integration into CI/CD pipelines.

## Architecture Highlights

### Feature-Based Structure

Commands set up projects using a scalable feature-based architecture:
- `src/features/` - Isolated feature modules
- `src/shared/` - Reusable components, hooks, utilities, and stores

### TypeScript Path Aliases

Clean imports without relative paths:

```typescript
import { Button } from '@ui/Button'
import { useAuth } from '@hooks/useAuth'
import { formatDate } from '@utils/date'
import { User } from '@types/User'
```

### NativeWind Styling

Modern Tailwind CSS for React Native:

```typescript
<View className="flex-1 bg-gray-100 p-4">
  <Text className="text-xl font-bold text-gray-900">Hello World</Text>
</View>
```

## Documentation

- **[CLAUDE.md](./CLAUDE.md)** - Architecture guide and best practices for working with Claude Code on this repo
- **[commands/README.md](./commands/README.md)** - Detailed command documentation
- Individual command files include complete task specifications and rules

## Requirements

- Claude Code (available at [claude.com/claude-code](https://claude.com/claude-code))
- Node.js 18+ (for most projects)
- A supported package manager: bun, npm, pnpm, or yarn
- Git (for version control)

## Installing Commands

### All Commands

```bash
ln -s $(pwd)/.claude-toolkit/commands/* .claude/commands/
```

### Specific Commands Only

```bash
# Setup commands only
ln -s $(pwd)/.claude-toolkit/commands/setup-*.md .claude/commands/

# Or pick individual commands
ln -s $(pwd)/.claude-toolkit/commands/feature-structure.md .claude/commands/
ln -s $(pwd)/.claude-toolkit/commands/rn-ui-components.md .claude/commands/
```

### Windows Users

Use `mklink` instead of `ln -s`:

```powershell
mklink .claude\commands\feature-structure.md ..\claude-toolkit\commands\feature-structure.md
```

## Contributing

We welcome contributions! Areas for expansion:

- New commands for other frameworks (Next.js, Vue, etc.)
- Additional UI component templates
- Skills for specialized workflows
- MCP plugin integrations
- Improved documentation and examples

### How to Contribute

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-command`)
3. Add your command following the existing format (see [commands/README.md](./commands/README.md))
4. Test thoroughly with Claude Code
5. Submit a pull request

### Command Guidelines

- Use clear, step-by-step instructions
- Include validation steps
- Document all important rules and constraints
- Test the complete workflow
- Support multiple package managers where relevant
- Avoid dependencies on other commands

## FAQ

**Q: Do I need to install this globally?**
A: No, symlink it into your project's `.claude/commands/` directory. You can have different versions per project.

**Q: Can I use individual commands or must I use all of them?**
A: Completely independent! Pick and choose what you need.

**Q: Does this work with non-Expo projects?**
A: Most commands are Expo/React Native focused, but the architecture patterns apply broadly. Custom commands for other frameworks are welcome contributions.

**Q: Will this interfere with my existing setup?**
A: Commands don't modify your project unless you run them. Symlinks are safe to add and remove.

**Q: How do I update the toolkit?**
A: Pull the latest changes: `cd .claude-toolkit && git pull`

## License

MIT - Feel free to use this in personal and commercial projects.

## Acknowledgments

Built for [Claude Code](https://claude.com/claude-code) and the open source community. Inspired by modern development tooling and best practices from the Expo and React Native ecosystems.

## Support

- 📖 Read the [CLAUDE.md](./CLAUDE.md) for detailed architecture documentation
- 🔍 Check individual command files for complete specifications
- 💬 Open an issue on GitHub for bugs or feature requests
- 🌟 Star the repo if you find it useful!

---

**Made with ❤️ for developers using Claude Code**
