---
description: "Validate that all success criteria for the current step are met"
agent: 'code-reviewer'
tools: ['codebase', 'search', 'grep', 'read', 'terminal', 'fetch', 'todo']
---

# Validate Step Success Criteria

Verify that all success criteria for a specific step have been met.

## Step Number

${input:step-number:Enter the step number (e.g., 5-0, 5-1, 5-2)}

## Instructions

You are working in **code review mode** to validate that step success criteria are met.

### Step 1: Locate the Exercise Issue

Find the main exercise issue using GitHub CLI:

```bash
gh issue list --state open
```

Look for an issue with "Exercise:" in the title. Note the issue number.

### Step 2: Get Issue Content with All Steps

Retrieve the full issue with all comments:

```bash
gh issue view <issue-number> --comments
```

Steps are posted as comments on the main issue.

### Step 3: Find Target Step

Search through the issue output to find the specific step:

```
# Step ${step-number}: [Title]
```

For example, if step-number is "5-1", look for:
```
# Step 5-1: [Title]
```

### Step 4: Extract Success Criteria

From the step content, locate the **Success Criteria** section:

```
Success Criteria:
- Criterion 1
- Criterion 2
- Criterion 3
```

Extract ALL criteria listed for this step.

### Step 5: Validate Each Criterion

For each success criterion, check the current workspace state:

**Common validation checks**:

1. **File exists**: Verify using file system
   ```bash
   ls -la <file-path>
   ```

2. **Code implementation**: Read file and verify logic
   - Check that functions/endpoints exist
   - Verify correct behavior

3. **Tests exist and pass**: Run test suite
   ```bash
   npm test
   ```
   - Verify specific test cases mentioned
   - Ensure all tests pass

4. **No lint errors**: Run linter
   ```bash
   npm run lint
   ```
   - Check for zero errors
   - Verify code quality

5. **API endpoints work**: Check implementation
   - Verify routes are defined
   - Check request/response handling
   - Validate status codes

6. **Component behavior**: Verify frontend changes
   - Check component exists
   - Verify props and state management
   - Test user interactions (if specified)

### Step 6: Report Validation Results

Provide a detailed report for each criterion:

```
# Validation Report for Step ${step-number}

## Success Criteria Checklist

### Criterion 1: [Description]
Status: ✅ PASS / ❌ FAIL / ⚠️ PARTIAL
Details: [Specific findings]
[Evidence: file location, test output, etc.]

### Criterion 2: [Description]
Status: ✅ PASS / ❌ FAIL / ⚠️ PARTIAL
Details: [Specific findings]

...

## Overall Status

✅ All criteria met - Step complete!
OR
⚠️ Some criteria need attention - See details above
OR
❌ Step incomplete - Address failed criteria

## Next Steps

[If complete]: Ready for /commit-and-push to save your work
[If incomplete]: Address the following items:
- [Specific action needed for failed criterion 1]
- [Specific action needed for failed criterion 2]
```

### Step 7: Provide Specific Guidance

For any **FAILED** or **PARTIAL** criteria:

1. **Explain what's missing**:
   - Be specific about what doesn't meet the requirement
   - Reference exact file locations and line numbers

2. **Suggest how to fix**:
   - Provide actionable steps
   - Reference relevant documentation or patterns
   - Recommend following TDD workflow if implementation needed

3. **Prioritize issues**:
   - Critical issues first (test failures, missing functionality)
   - Then code quality issues (lint errors, missing PropTypes)
   - Then optional improvements

## Validation Examples

### Example: Test Criterion

**Criterion**: "Tests for DELETE endpoint pass"

**Validation**:
```bash
npm test -- app.test.js
```

**Report**:
```
✅ PASS
All DELETE endpoint tests passing:
- DELETE returns 404 for non-existent todo ✓
- DELETE returns 200 for successful deletion ✓
- DELETE removes todo from array ✓

Evidence: packages/backend/__tests__/app.test.js (lines 45-67)
```

### Example: Implementation Criterion

**Criterion**: "DELETE /api/todos/:id endpoint implemented"

**Validation**:
- Read `packages/backend/src/app.js`
- Search for `app.delete('/api/todos/:id'`
- Verify handler logic

**Report**:
```
✅ PASS
DELETE endpoint implemented at packages/backend/src/app.js:89-102
- Validates todo existence ✓
- Returns 404 if not found ✓
- Removes todo from array ✓
- Returns deleted todo in response ✓
```

### Example: Quality Criterion

**Criterion**: "No ESLint errors"

**Validation**:
```bash
npm run lint
```

**Report**:
```
❌ FAIL
ESLint found 3 errors:
- packages/backend/src/app.js:95 - Unexpected console statement (no-console)
- packages/frontend/src/App.js:23 - Unused variable 'data' (no-unused-vars)
- packages/frontend/src/App.js:45 - Missing PropTypes validation

Action needed: Run code-reviewer agent to fix these issues systematically
```

## Output Format

Always provide:
1. Clear status for each criterion (✅ / ❌ / ⚠️)
2. Specific evidence (file paths, line numbers, test results)
3. Overall status summary
4. Actionable next steps

---

**Remember**: Be thorough but specific. Reference exact locations. Provide actionable guidance for any issues found.
