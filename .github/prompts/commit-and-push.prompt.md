---
description: "Analyze changes, generate commit message, and push to feature branch"
tools: ['grep', 'read', 'terminal', 'todo']
---

# Commit and Push Changes

Analyze current changes, generate a conventional commit message, and push to a feature branch.

## Branch Name

${input:branch-name:Enter the feature branch name (e.g., feature/add-delete-endpoint)}

## Instructions

You are committing and pushing changes using established Git workflow practices.

### Step 1: Validate Branch Name

**Check if branch name was provided**:
- If provided: Use it
- If NOT provided: Stop and ask the user for a branch name

**Branch naming conventions**:
- `feature/<descriptive-name>` - For new features
- `fix/<descriptive-name>` - For bug fixes
- Example: `feature/add-delete-endpoint` or `fix/todo-update-validation`

### Step 2: Analyze Changes

Run git diff to understand what changed:

```bash
git status
git diff
```

Review the changes to understand:
- What files were modified
- What functionality was added/changed
- Whether changes are features, fixes, tests, or refactoring

### Step 3: Generate Conventional Commit Message

Based on the changes, create a commit message following **conventional commit format**:

**Format**: `<type>: <description>`

**Types**:
- `feat:` - New features
- `fix:` - Bug fixes
- `test:` - Adding or updating tests
- `refactor:` - Code refactoring without behavior changes
- `chore:` - Build process, dependencies, tooling
- `docs:` - Documentation updates
- `style:` - Code formatting, linting fixes

**Examples**:
```bash
feat: add delete todo endpoint
fix: correct todo update validation
test: add integration tests for todo routes
style: fix eslint errors in app.js
refactor: extract findTodoById helper function
```

**Guidelines**:
- Keep description concise (50 chars or less)
- Use imperative mood ("add" not "added")
- Don't capitalize first letter
- No period at the end

### Step 4: Create or Switch to Branch

**Check if branch exists**:

```bash
git branch --list ${branch-name}
```

**If branch does NOT exist**:
```bash
git checkout -b ${branch-name}
```

**If branch exists**:
```bash
git checkout ${branch-name}
```

**CRITICAL**: NEVER commit to `main` branch. Always use the user-provided branch name.

### Step 5: Stage All Changes

Stage all modified and new files:

```bash
git add .
```

Verify what will be committed:

```bash
git status
```

### Step 6: Commit Changes

Commit with the generated conventional commit message:

```bash
git commit -m "<type>: <description>"
```

### Step 7: Push to Branch

Push the committed changes to the remote branch:

```bash
git push origin ${branch-name}
```

**If this is the first push to a new branch**, you may need:

```bash
git push --set-upstream origin ${branch-name}
```

### Step 8: Confirm Success

After successful push, inform the user:

```
✅ Changes committed and pushed

Branch: ${branch-name}
Commit: <type>: <description>

Files changed:
- <file1>
- <file2>

Next steps:
- Continue with next step, OR
- Create a pull request if work is complete
```

## Error Handling

**If git operations fail**:
- Check if you're in a git repository
- Verify branch name is valid (no spaces, special chars)
- Ensure you have git credentials configured
- Provide clear error message and suggested fix

**If no changes to commit**:
- Inform user: "No changes detected. Working directory is clean."
- Suggest: "Make changes first, then run /commit-and-push"

## Safety Checks

Before pushing:
- ✅ Confirm you're NOT on `main` branch
- ✅ Verify commit message follows conventional format
- ✅ Ensure all changes are staged with `git add .`

---

**Remember**: Always use the provided branch name. Never commit directly to main. Follow conventional commit format.
