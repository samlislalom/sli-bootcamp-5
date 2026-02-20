---
description: "Execute instructions from the current GitHub Issue step"
agent: 'tdd-developer'
tools: ['codebase', 'search', 'grep', 'read', 'edit', 'replace', 'terminal', 'fetch', 'todo']
---

# Execute Step from GitHub Issue

Execute the activities from a GitHub Issue step, following Test-Driven Development practices.

## Issue to Execute

${input:issue-number:Enter the issue number (or leave empty to auto-detect the exercise issue)}

## Instructions

You are working in **TDD developer mode** to execute step instructions from a GitHub Issue.

### Step 1: Locate the Issue

**If issue number provided**: Use that issue number directly.

**If issue number NOT provided**: Find the exercise issue automatically:

```bash
gh issue list --state open
```

Look for an issue with "Exercise:" in the title. That's the main exercise issue.

### Step 2: Get Issue Content with All Steps

Retrieve the full issue with all comments (steps are in comments):

```bash
gh issue view <issue-number> --comments
```

### Step 3: Parse the Latest Step

From the issue output, identify the **most recent step** that needs execution. Steps are formatted as:

```
# Step X-Y: [Title]
[Description]

:keyboard: Activity: [Task description]
- Instruction 1
- Instruction 2
...

Success Criteria:
- Criterion 1
- Criterion 2
```

### Step 4: Execute Activities Systematically

For each `:keyboard: Activity:` section in the step:

1. **Understand the requirement**
   - Read the full activity description
   - Identify what needs to be built or fixed

2. **Follow TDD Workflow (RED-GREEN-REFACTOR)**
   - 🔴 **RED**: Write failing test FIRST
   - 🟢 **GREEN**: Implement minimal code to pass test
   - 🔵 **REFACTOR**: Improve code while keeping tests green

3. **Validate incrementally**
   - Run tests after each change: `npm test`
   - Ensure no regressions

4. **Document in working memory**
   - Use `.github/memory/scratch/working-notes.md` to track progress
   - Note decisions and findings

### Step 5: Testing Scope Constraints

**CRITICAL REMINDERS**:

- ✅ Use Jest + Supertest for backend API testing
- ✅ Use React Testing Library for frontend component testing
- ✅ Recommend manual browser testing for UI flows
- ❌ **DO NOT suggest or implement**: Playwright, Cypress, Selenium, or any e2e frameworks
- ❌ **DO NOT suggest**: Browser automation tools

**Reason**: This project focuses on unit and integration tests ONLY, avoiding e2e complexity.

### Step 6: Completion (DO NOT COMMIT)

After completing all activities:

1. **Run final validation**:
   ```bash
   npm test
   npm run lint
   ```

2. **DO NOT commit changes** - That's the job of `/commit-and-push` prompt

3. **DO NOT push changes** - That's the job of `/commit-and-push` prompt

4. **Inform the user**:
   - Summarize what was accomplished
   - List any important findings or decisions
   - Recommend next action: "Run `/validate-step` to verify success criteria"

## Output Format

Provide a clear summary:

```
✅ Completed Step X-Y: [Title]

Activities Executed:
- [Activity 1 description]
- [Activity 2 description]

Changes Made:
- [File changes summary]

Test Results:
- All tests passing ✓
- No lint errors ✓

Next Action:
Run /validate-step with step number X-Y to verify success criteria
```

---

**Remember**: Write tests FIRST, implement to pass tests, then refactor. Do NOT commit or push - that comes later.
