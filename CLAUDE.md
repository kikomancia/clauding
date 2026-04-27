# CLAUDE.md — Laravel + PostgreSQL + React Project

## 🧠 Project Context
This is a full-stack web application:
- **Backend:** PHP Laravel (API)
- **Database:** PostgreSQL
- **Frontend:** React
- **CI/CD:** GitHub Actions
- **QA Style:** Lint + Type Check

Claude should always follow the pipeline below when working on features.

---

## 🔁 Pipeline: Intent → Engineer → QA → Deploy

Every task follows this 4-stage flow. Do NOT skip stages.

```
/intent   →   /engineer   →   /qa   →   /deploy
```

---

## 📋 Stage Definitions

### Stage 1 — /intent
**Goal:** Understand and document what needs to be built before writing any code.

Claude must:
1. Ask clarifying questions if the requirement is vague
2. Write a short spec to `.claude/intent/YYYY-MM-DD-<feature-slug>.md` with:
   - Feature name
   - What it does (in plain English)
   - Affected files/areas (Laravel controllers, React components, DB tables)
   - Acceptance criteria (what "done" looks like)
3. Confirm with the developer before proceeding

---

### Stage 2 — /engineer
**Goal:** Implement the feature based on the approved intent doc.

Claude must:
1. Read the latest intent doc from `.claude/intent/`
2. Follow these conventions:
   - **Laravel:** PSR-12, use Form Requests for validation, use Resource classes for API responses
   - **PostgreSQL:** Use Laravel migrations, never raw SQL in controllers
   - **React:** Functional components only, TypeScript preferred, no class components
3. Create or edit only the files relevant to the intent
4. Write clean, readable code with inline comments where logic is non-obvious
5. Update `.claude/log.md` with a summary of changes made

---

### Stage 3 — /qa
**Goal:** Run lint and type checks. Fix all issues before deploy.

Claude must run (in order):

**Backend (Laravel):**
```bash
./vendor/bin/pint          # Laravel Pint (PHP linter)
php artisan code:analyse   # Larastan/PHPStan static analysis
```

**Frontend (React):**
```bash
npm run lint               # ESLint
npm run type-check         # TypeScript compiler check (tsc --noEmit)
```

If any check fails:
- Fix the issue immediately
- Re-run the check to confirm it passes
- Do NOT proceed to /deploy until all checks are green ✅

---

### Stage 4 — /deploy
**Goal:** Push to GitHub and trigger the CI pipeline.

Claude must:
1. Confirm all QA checks passed
2. Stage and commit changes:
   ```bash
   git add .
   git commit -m "<type>(<scope>): <short description>"
   ```
   Commit message format: `feat(auth): add login endpoint` | `fix(ui): correct button alignment`
3. Push to the feature branch:
   ```bash
   git push origin <branch-name>
   ```
4. Remind the developer to open a Pull Request on GitHub
5. GitHub Actions will automatically run `.github/workflows/ci.yml`

---

## 📁 Key File Locations

| What | Where |
|------|-------|
| Intent docs | `.claude/intent/` |
| Change log | `.claude/log.md` |
| Laravel routes | `routes/api.php` |
| Laravel controllers | `app/Http/Controllers/` |
| Laravel models | `app/Models/` |
| DB migrations | `database/migrations/` |
| React source | `resources/js/` (or `frontend/src/`) |
| GitHub Actions | `.github/workflows/ci.yml` |

---

## ⚙️ Environment Notes

- PHP version: 8.2+
- Node version: 18+
- PostgreSQL: use `DB_CONNECTION=pgsql` in `.env`
- Run `php artisan migrate` after any migration changes
- Run `npm install` if new packages are added

---

## 🚫 Rules

- Never commit `.env` files
- Never use `dd()` or `var_dump()` in production code
- Never skip the `/qa` stage even for "small" changes
- Never write raw PostgreSQL queries outside of migrations or query builders
- Always use `php artisan make:` commands to scaffold new files

---

## 🧠 Claude Behavior

- Be concise in responses — no fluff
- When asked to do a task, state which pipeline stage you're in
- If something is unclear, ask ONE focused question before proceeding
- Always show the commands you ran and their output during /qa
- After /deploy, summarize what was shipped in one paragraph
