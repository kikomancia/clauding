# /intent — Capture Feature Intent

## What this command does
Starts Stage 1 of the pipeline. Captures what needs to be built BEFORE any code is written.

## Steps Claude will follow

1. Ask the developer to describe the feature in plain English
2. Identify:
   - Which Laravel routes/controllers are affected
   - Which React components are affected
   - Which DB tables or migrations are needed
3. Write an intent doc to: `.claude/intent/YYYY-MM-DD-<feature-slug>.md`
4. Present the doc and ask: "Does this match what you want? (yes / revise)"
5. Only proceed to /engineer after confirmation

## Intent Doc Template

```markdown
# Intent: <Feature Name>
Date: YYYY-MM-DD

## Summary
<One paragraph describing what this feature does>

## Affected Areas
- **Backend:** <controllers, models, routes>
- **Frontend:** <React components, pages>
- **Database:** <tables, migrations>

## Acceptance Criteria
- [ ] <criterion 1>
- [ ] <criterion 2>
- [ ] <criterion 3>

## Out of Scope
- <anything explicitly NOT being built>
```

## Usage
Just type: `/intent` and describe your feature
