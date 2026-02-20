# Working Memory System

## Purpose

This memory system helps track patterns, decisions, and lessons learned during development. It serves as a bridge between individual coding sessions and the project's permanent knowledge base.

## Memory Types

### Persistent Memory
- **Location**: `.github/copilot-instructions.md`
- **Purpose**: Foundational principles, workflows, and standards that remain constant
- **Updated**: Rarely, only when core practices change
- **Git Status**: Always committed

### Working Memory
- **Location**: `.github/memory/` directory
- **Purpose**: Accumulate discoveries, patterns, and session learnings
- **Updated**: Frequently during and after development sessions
- **Git Status**: Mixed (see below)

## Directory Structure

```
.github/memory/
├── README.md                    # This file - explains the system
├── session-notes.md             # Historical session summaries (committed)
├── patterns-discovered.md       # Accumulated code patterns (committed)
└── scratch/
    ├── .gitignore               # Ignores all scratch files
    └── working-notes.md         # Active session notes (NOT committed)
```

### File Purposes

#### `session-notes.md` (Committed)
- **What**: Summaries of completed development sessions
- **When**: Written at the END of a session
- **Content**: Key accomplishments, findings, decisions, and outcomes
- **Why Committed**: Historical record for future reference and context

#### `patterns-discovered.md` (Committed)
- **What**: Reusable code patterns learned during development
- **When**: Updated when discovering new patterns or anti-patterns
- **Content**: Pattern name, context, problem, solution, examples
- **Why Committed**: Helps maintain consistency across the codebase

#### `scratch/working-notes.md` (NOT Committed)
- **What**: Active, real-time notes during development
- **When**: Written DURING active development
- **Content**: Current task, approach, findings, blockers, next steps
- **Why Not Committed**: Ephemeral working space; insights get promoted to session-notes.md

## When to Use Each File

### During TDD Workflow

**While Writing Tests** (use `scratch/working-notes.md`):
- Document the expected behavior you're testing
- Note any edge cases discovered
- Track which tests are failing and why
- Record decisions about test structure

**After Completing Feature** (update `session-notes.md`):
- Summarize what was implemented
- Document key testing decisions
- Note any patterns that emerged

**If Pattern Emerges** (update `patterns-discovered.md`):
- Document the testing pattern (e.g., "Always mock external services")
- Provide example from the code

### During Linting/Code Quality Workflow

**While Fixing Issues** (use `scratch/working-notes.md`):
- Categorize lint errors by type
- Note any patterns in the errors (e.g., "Consistent missing PropTypes")
- Track which fixes might need tests updated

**After Completing Fixes** (update `session-notes.md`):
- Summarize categories of issues fixed
- Document any standards clarified

**If Pattern Emerges** (update `patterns-discovered.md`):
- Document recurring code quality patterns
- Example: "Always validate req.body before processing"

### During Debugging Workflow

**While Investigating** (use `scratch/working-notes.md`):
- Document symptoms and hypotheses
- Track what you've tried and results
- Note any unexpected behaviors

**After Resolving Bug** (update `session-notes.md`):
- Document root cause
- Explain the fix
- Note preventive measures taken

**If Pattern Emerges** (update `patterns-discovered.md`):
- Document the bug pattern and how to avoid it
- Example: "Service initialization: Always use empty array, never null"

## AI Usage of Memory System

### How AI Reads These Files

When GitHub Copilot or other AI assistants work on this project:

1. **Copilot Instructions**: Always active, provides foundational context
2. **Session Notes**: Referenced to understand recent changes and decisions
3. **Patterns Discovered**: Applied to ensure consistency with established patterns
4. **Working Notes**: Read to understand current session context

### How AI Applies Patterns

When you ask AI to implement a feature:
1. AI checks `patterns-discovered.md` for relevant patterns
2. AI suggests implementation following those patterns
3. AI references specific pattern names in explanations

Example:
> "I'll initialize the items array following the **Service Initialization Pattern** documented in patterns-discovered.md, using an empty array instead of null."

### Keeping AI Context Fresh

**Start of Each Session**:
- Review `session-notes.md` to recall recent work
- Check `patterns-discovered.md` for relevant patterns
- Start fresh notes in `scratch/working-notes.md`

**During Session**:
- AI can read `scratch/working-notes.md` for current context
- Update notes as you discover new information

**End of Session**:
- Promote key findings from `scratch/working-notes.md` to `session-notes.md`
- Add any new patterns to `patterns-discovered.md`
- Clear or archive `scratch/working-notes.md` for next session

## Workflow Summary

### Active Development
```
1. Open scratch/working-notes.md
2. Document current task and approach
3. Work on implementation
4. Record findings and decisions in real-time
5. Note any patterns or anti-patterns observed
```

### Session Close
```
1. Review scratch/working-notes.md for key insights
2. Add session summary to session-notes.md
3. Update patterns-discovered.md with any new patterns
4. Clear scratch/working-notes.md (or let it be overwritten next session)
```

### Next Session
```
1. Read session-notes.md to recall recent context
2. Review patterns-discovered.md for relevant patterns
3. Start fresh notes in scratch/working-notes.md
```

## Benefits

- **Continuity**: Maintain context across sessions
- **Learning**: Accumulate patterns and best practices
- **Consistency**: Apply proven patterns throughout codebase
- **AI Enhancement**: Provide richer context for AI assistance
- **Documentation**: Automatic historical record of development journey

## Best Practices

1. **Be Concise**: Notes should be scannable and actionable
2. **Be Specific**: Include file names, line numbers, and code snippets
3. **Be Timely**: Write notes during work, not from memory later
4. **Be Selective**: Promote only significant findings to committed files
5. **Be Consistent**: Use the templates provided in each file

---

*This memory system is designed to work with GitHub Copilot and other AI assistants to provide better context-aware suggestions throughout development.*
