---
name: commit-push
description: Commit and push all changes to remote branch with smart message generation
---

## Task

Automate the git commit and push workflow:

1. **Check Changes**: Run `git status` and `git diff` to understand all modifications

2. **Review Commits**: Run `git log -10 --oneline` to understand the repository's commit message style

3. **Analyze Changes**:

   - Examine staged and unstaged changes
   - Determine the nature and scope of modifications
   - Group related changes together
   - Identify the primary purpose of the changes

4. **Draft Commit Message**: Create an appropriate commit message following best practices:

   - Use conventional commit format: `type(scope): description`
   - Common types: `feat`, `fix`, `refactor`, `docs`, `test`, `chore`, `style`, `perf`, `ci`
   - Optional scope: feature or module name (e.g., `feat(auth):`, `fix(api):`)
   - Keep description concise and imperative (e.g., "add login form" not "added login form")
   - Focus on the "why" and business value, not just the "what"
   - If changes are complex, add a blank line and bullet points with details
   - Match the existing repository's commit style if it differs from conventional commits
   - **CRITICAL: DO NOT include any Claude Code attribution, emoji, or co-author tags**

5. **Security Check**:

   - Verify no sensitive files are being committed (.env, .env.local, credentials.json, etc.)
   - Check for API keys, tokens, or passwords in diffs
   - Exclude files that should be in .gitignore

6. **Stage Files**: Add all relevant untracked and modified files to staging

```bash
   git add .
```

7. **Create Commit**: Commit with the drafted message

```bash
   git commit -m "your generated message"
```

8. **Push to Remote**: Push the commit to the current branch

```bash
   git push
```

- If this is the first push and branch doesn't exist remotely, use:

```bash
   git push -u origin HEAD
```

9. **Verify**: Run `git status` to confirm everything is clean and pushed

10. **Summary**: Show the commit hash and provide a brief summary of what was pushed

## Rules

- **CRITICAL: NO Claude Code mentions, emojis, or "Co-Authored-By" tags in commit messages**
- Commit message must be plain text only, no attribution or generated-by tags
- DO NOT include "Generated with Claude Code" or similar phrases
- DO NOT include robot emoji or any emojis in commit messages
- DO NOT add "Co-Authored-By: Claude" footer
- DO NOT mention Claude Code or AI anywhere in the commit
- DO NOT commit sensitive files (.env*, *credentials*, *secrets*, *.pem, \*.key, etc.)
- DO NOT force push or use destructive git commands (no --force, no reset --hard)
- DO NOT proceed if there are merge conflicts
- Skip committing if there are no relevant changes
- If pre-commit hooks modify files, review changes and amend the commit if needed
- If there are untracked files that look like dependencies or build artifacts, ask before committing
- If commit message is longer than 72 characters, ask user if they want to shorten it

## Error Handling

- If push fails due to remote changes, inform user to pull first
- If there are unstaged changes after pre-commit hooks, ask before proceeding
- If .gitignore is missing common patterns, suggest adding them
