---
description: Commit and push all changes to remote branch
---

## Task

Automate the git commit and push workflow:

1. **Check Changes**: Run `git status` and `git diff` to understand all modifications
2. **Review Commits**: Run `git log` to understand the repository's commit message style
3. **Analyze Changes**: Examine staged and unstaged changes to determine the nature of modifications
4. **Draft Commit Message**: Create an appropriate commit message following the repository's standards
   - Use conventional commit format (type: description)
   - Focus on the "why" rather than the "what"
   - Keep the message concise (1-2 sentences)
   - Common types: feat, fix, refactor, docs, test, chore, style
5. **Stage Files**: Add all relevant untracked and modified files to staging
6. **Create Commit**: Commit with the drafted message
7. **Push to Remote**: Push the commit to the remote branch using `git push`
8. **Verify**: Run `git status` to confirm the push was successful

## Rules

- Do NOT commit files containing secrets (.env, credentials.json, etc.)
- Do NOT force push or use destructive git commands
- Skip committing if there are no relevant changes
- If pre-commit hooks modify files, verify the changes are safe before amending
