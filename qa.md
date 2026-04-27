# /qa — Lint + Type Check

## What this command does
Stage 3 of the pipeline. Runs all quality checks before deploying.

## Steps Claude will follow

### Backend checks (run in order):
```bash
# 1. PHP lint — Laravel Pint
./vendor/bin/pint

# 2. Static analysis — Larastan / PHPStan
./vendor/bin/phpstan analyse --memory-limit=256M
```

### Frontend checks (run in order):
```bash
# 1. ESLint
npm run lint

# 2. TypeScript type check
npx tsc --noEmit
```

## Pass / Fail Rules
- ALL checks must pass before /deploy is allowed
- If any check fails: fix the issue, re-run, confirm green ✅
- Claude will show the output of each command

## Auto-fix mode
Claude can attempt to auto-fix lint issues:
- PHP: `./vendor/bin/pint` (auto-fixes on its own)
- JS/TS: `npm run lint -- --fix`

## Usage
Type: `/qa` — Claude runs all checks and reports status
