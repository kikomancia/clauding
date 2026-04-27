# /engineer — Implement the Feature

## What this command does
Stage 2 of the pipeline. Writes the actual code based on the approved intent doc.

## Steps Claude will follow

1. Read the latest `.claude/intent/*.md` file
2. Confirm which intent doc is being implemented
3. Scaffold files using `php artisan make:` where applicable:
   - `php artisan make:controller`
   - `php artisan make:model`
   - `php artisan make:migration`
   - `php artisan make:request`
   - `php artisan make:resource`
4. Implement backend logic (Laravel)
5. Implement frontend logic (React)
6. Update `.claude/log.md` with a summary

## Laravel Conventions
- Use Form Requests for all input validation
- Use API Resources for all JSON responses
- Use Eloquent ORM — no raw SQL in controllers
- Follow PSR-12 coding standard

## React Conventions
- Functional components only
- Use TypeScript (`.tsx` files)
- Props must be typed with interfaces
- No inline styles — use CSS modules or Tailwind

## Usage
Type: `/engineer` — Claude will read the intent and start coding
