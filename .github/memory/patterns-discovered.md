# Patterns Discovered

This file documents reusable code patterns learned during development. Each pattern includes context, problem, solution, and examples.

**Purpose**: Maintain consistency by documenting proven patterns
**Updated**: When new patterns are discovered or anti-patterns identified
**Git Status**: Committed to repository

---

## Pattern Template

Use this template when adding new patterns:

```markdown
## [Pattern Name]

**Context**: When does this pattern apply?

**Problem**: What issue does this pattern solve?

**Solution**: What is the recommended approach?

**Example**:
```[language]
// Code example demonstrating the pattern
```

**Related Files**: 
- path/to/file.js
- path/to/another-file.js

**Tags**: #category #type #scope
```

---

## Service Initialization Pattern

**Context**: When initializing data structures in service classes or API responses

**Problem**: Inconsistent initialization can lead to errors when consumers expect arrays but receive null or undefined values. This creates defensive code throughout the application checking for null/undefined before array operations.

**Solution**: Always initialize collections (arrays) as empty arrays instead of null or undefined. Use null only for optional singular values that semantically represent "no value."

**Example**:
```javascript
// ✅ GOOD: Initialize with empty array
class TodoService {
  constructor() {
    this.todos = [];  // Always iterable, safe for .map(), .filter(), etc.
  }
}

// ❌ AVOID: Initialize with null
class TodoService {
  constructor() {
    this.todos = null;  // Requires null checks before iteration
  }
}

// ✅ GOOD: API response with empty array
app.get('/api/todos', (req, res) => {
  const todos = getTodos() || [];  // Ensure array even if getTodos fails
  res.json({ todos });  // Always an array
});

// ❌ AVOID: API response with null
app.get('/api/todos', (req, res) => {
  const todos = getTodos();  // Might be null
  res.json({ todos });  // Frontend must handle null
});
```

**Related Files**: 
- packages/backend/src/app.js
- packages/frontend/src/App.js

**Tags**: #initialization #arrays #defensive-coding #api-design

---

## [Your Next Pattern]

[Document patterns as you discover them during development]
