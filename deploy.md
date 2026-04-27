# /deploy — Commit + Push + CI Trigger

## What this command does
Stage 4 of the pipeline. Commits changes, pushes to GitHub, and triggers the CI workflow.

## Pre-flight checklist (Claude confirms before running)
- [ ] /qa passed with zero errors
- [ ] No `.env` files staged
- [ ] No `dd()` or `var_dump()` left in code
- [ ] Branch name is descriptive (not just "main")

## Steps Claude will follow

1. Show staged files: `git status`
2. Stage all changes: `git add .`
3. Commit with conventional message:
   ```bash
   git commit -m "<type>(<scope>): <description>"
   ```
4. Push to current branch:
   ```bash
   git push origin <current-branch>
   ```
5. Print a deploy summary

## Commit Message Format
```
feat(auth): add JWT login endpoint
fix(ui): correct form validation error display
chore(db): add users table migration
refactor(api): extract UserResource class
```

Types: `feat` | `fix` | `chore` | `refactor` | `docs` | `style`

## After Push
GitHub Actions will automatically run `.github/workflows/ci.yml`:
- Backend: Pint lint + Larastan + DB migrations
- Frontend: ESLint + TypeScript check + build

Claude will remind you to open a Pull Request on GitHub if targeting `main` or `develop`.

## Usage
Type: `/deploy` — Claude checks the preflight list then commits and pushes
