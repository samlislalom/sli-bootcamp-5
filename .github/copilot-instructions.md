# Copilot Instructions for TODO Application

## Project Context

This is a full-stack TODO application with a React frontend and Express backend. Development follows an iterative, feedback-driven approach with emphasis on test coverage and incremental improvements.

**Current Phase**: Backend stabilization and frontend feature completion

**Tech Stack**:
- Frontend: React with React Testing Library
- Backend: Express with Jest and Supertest
- Monorepo structure using npm workspaces

## Documentation References

The project includes comprehensive documentation to guide development:

- [docs/project-overview.md](../docs/project-overview.md) - Architecture, tech stack, and project structure
- [docs/testing-guidelines.md](../docs/testing-guidelines.md) - Test patterns and standards
- [docs/workflow-patterns.md](../docs/workflow-patterns.md) - Development workflow guidance

Always reference these documents when working on the project to maintain consistency with established patterns.

## Development Principles

Follow these core principles for all development work:

- **Test-Driven Development**: Follow the Red-Green-Refactor cycle for all feature work
- **Incremental Changes**: Make small, testable modifications rather than large refactors
- **Systematic Debugging**: Use test failures as guides to identify and fix issues
- **Validation Before Commit**: Ensure all tests pass and no lint errors exist before committing

## Testing Scope

This project uses **unit tests and integration tests ONLY**. Understanding this scope is critical:

**What We Use**:
- Backend: Jest + Supertest for API testing
- Frontend: React Testing Library for component unit/integration tests
- Manual browser testing for full UI verification

**What We DO NOT Use**:
- ❌ E2E test frameworks (Playwright, Cypress, Selenium)
- ❌ Browser automation tools
- ❌ Visual regression testing tools

**Reason**: This lab focuses on unit and integration testing patterns without the added complexity of end-to-end test infrastructure.

**Testing Approach by Context**:

- **Backend API changes**: Write Jest tests FIRST, then implement (RED-GREEN-REFACTOR)
  1. Write a failing test for the new behavior
  2. Run tests and confirm the failure (RED)
  3. Implement minimal code to pass the test (GREEN)
  4. Refactor while keeping tests green (REFACTOR)

- **Frontend component features**: Write React Testing Library tests FIRST for component behavior, then implement (RED-GREEN-REFACTOR)
  1. Write a failing test for the component behavior
  2. Run tests and confirm the failure (RED)
  3. Implement minimal code to pass the test (GREEN)
  4. Refactor while keeping tests green (REFACTOR)
  5. Follow with manual browser testing for full UI flows

**This is true TDD**: Always write the test first, then write code to pass the test.

## Workflow Patterns

Follow these established workflows for different types of work:

### 1. TDD Workflow (Test-Driven Development)

```
Write/Fix Test → Run Tests → Observe Failure (RED) → Implement Code → 
Tests Pass (GREEN) → Refactor → Validate → Commit
```

- Start with a failing test that defines desired behavior
- Implement only what's needed to make the test pass
- Refactor with confidence knowing tests will catch regressions

### 2. Code Quality Workflow (Lint Fixes)

```
Run Lint → Categorize Issues → Fix Systematically → 
Run Lint Again → Re-validate → Commit
```

- Group similar lint errors and fix them in batches
- Run tests after fixing lint errors to ensure no behavioral changes
- Use the code-reviewer agent for guidance on code quality improvements

### 3. Integration Workflow (Bug Fixes)

```
Identify Issue → Debug with Tests → Write/Update Test → 
Fix Implementation → Verify End-to-End → Commit
```

- Always add or update a test that captures the bug
- Fix the implementation to make the test pass
- Verify the fix resolves the original issue

## Agent Usage

This project uses specialized agents for specific workflows. Use the appropriate agent for each task:

### `tdd-developer` Agent

Use for:
- Writing new tests (unit or integration)
- Implementing features using TDD workflow
- Debugging test failures
- Following Red-Green-Refactor cycles
- Test infrastructure improvements

**When to use**: Any work involving tests or test-driven implementation

### `code-reviewer` Agent

Use for:
- Addressing lint errors and warnings
- Code quality improvements
- Refactoring existing code
- Ensuring adherence to code standards
- Code structure and organization

**When to use**: Any work focused on code quality, linting, or refactoring

## Memory System

This project uses a two-tier memory system to maintain context across development sessions:

### Persistent Memory
- **Location**: This file (`.github/copilot-instructions.md`)
- **Content**: Foundational principles, workflows, and standards
- **Usage**: Always active, provides core project context

### Working Memory
- **Location**: `.github/memory/` directory
- **Content**: Development discoveries, patterns, and session learnings
- **Structure**:
  - `session-notes.md` - Historical session summaries (committed)
  - `patterns-discovered.md` - Documented code patterns (committed)
  - `scratch/working-notes.md` - Active session notes (NOT committed)

### How to Use

**During Active Development**:
- Take real-time notes in `.github/memory/scratch/working-notes.md`
- Document current task, approach, findings, decisions, and blockers
- This file is ephemeral and not committed to git

**At End of Session**:
- Summarize key findings into `.github/memory/session-notes.md`
- Document any recurring patterns in `.github/memory/patterns-discovered.md`
- Clear or archive `scratch/working-notes.md` for next session

**When Providing AI Assistance**:
- Reference `session-notes.md` for recent development context
- Apply patterns from `patterns-discovered.md` to ensure consistency
- Read `scratch/working-notes.md` for current session context
- Suggest implementations that follow documented patterns

For complete details, see [.github/memory/README.md](.github/memory/README.md).

## Workflow Utilities

The project uses GitHub CLI for workflow automation. These commands are available in all modes:

### Issue Management

```bash
# List all open issues
gh issue list --state open

# Get details for a specific issue
gh issue view <issue-number>

# Get issue with all comments (useful for steps)
gh issue view <issue-number> --comments
```

### Exercise Workflow

- The main exercise issue has "Exercise:" in the title
- Individual steps are posted as comments on the main issue
- Use `/execute-step` prompts to work on specific steps
- Use `/validate-step` prompts to verify completed work

**Example workflow**:
1. Find the exercise issue: `gh issue list --state open`
2. View all steps: `gh issue view <issue-number> --comments`
3. Execute a specific step using the appropriate agent
4. Validate before moving to the next step

## Git Workflow

### Conventional Commits

Use conventional commit format for all commits:

- `feat:` - New features
- `fix:` - Bug fixes
- `test:` - Adding or updating tests
- `refactor:` - Code refactoring without behavior changes
- `chore:` - Build process, dependencies, tooling
- `docs:` - Documentation updates
- `style:` - Code formatting, linting fixes

**Examples**:
```bash
git commit -m "feat: add delete todo endpoint"
git commit -m "fix: correct todo update validation"
git commit -m "test: add integration tests for todo routes"
git commit -m "style: fix eslint errors in app.js"
```

### Branch Strategy

- `main` - Stable branch, all tests passing
- `feature/<descriptive-name>` - Feature development branches
- `fix/<descriptive-name>` - Bug fix branches

### Commit Process

Always follow this sequence:

```bash
# 1. Stage all changes
git add .

# 2. Commit with conventional commit message
git commit -m "feat: descriptive message"

# 3. Push to the correct branch
git push origin <branch-name>
```

**Important**: Always verify you're on the correct branch before committing and pushing.

---

*Last updated: February 20, 2026*
