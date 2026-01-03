# Template: Git Commit Message

**Category**: Git Workflow
**Use Case**: Creating professional, descriptive commit messages
**Format**: Standard Git commit format

---

## Template

```
{{SHORT_SUMMARY}}

- {{CHANGE_1}}
- {{CHANGE_2}}
- {{CHANGE_3}}

{{OPTIONAL_ADDITIONAL_CONTEXT}}

🤖 Generated with Claude Code
```

---

## Structure Breakdown

### Line 1: Short Summary (50 characters max)
- **Format**: Imperative mood ("Add", "Fix", "Update", not "Added" or "Adds")
- **Content**: What changed at a high level
- **Examples**:
  - `Add user authentication system`
  - `Fix rate limiting bug in API`
  - `Update documentation for deployment`
  - `Refactor service layer for testability`

### Line 2: Blank Line
- **Required**: Separates title from body

### Lines 3+: Detailed Bullets
- **Format**: Start with `-` or `*`
- **Content**: Specific changes, why they were made
- **Be specific**: Not just "updated files" but "Updated UserService to handle edge case"

### Optional: Additional Context
- **When to use**: Breaking changes, migration notes, related issues
- **Examples**:
  - `Breaking: API endpoint /v1/users renamed to /v2/users`
  - `Closes #123`
  - `See docs/MIGRATION.md for upgrade instructions`

### Footer: Attribution (Optional)
- `🤖 Generated with Claude Code`
- `Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>`

---

## Examples

### Example 1: Feature Addition

**Filled template:**
```
Add user authentication system

- Implement JWT-based authentication with refresh tokens
- Add login and registration endpoints
- Create auth middleware for protected routes
- Store hashed passwords using bcrypt
- Add unit tests for auth service

🤖 Generated with Claude Code
```

### Example 2: Bug Fix

**Filled template:**
```
Fix rate limiting bypass vulnerability

- Correct IP extraction from X-Forwarded-For header
- Add validation for malformed IP addresses
- Implement sliding window rate limiter
- Add integration tests for rate limiting

Security: Addresses CVE-2024-XXXXX

🤖 Generated with Claude Code
```

### Example 3: Refactoring

**Filled template:**
```
Refactor service layer for dependency injection

- Extract interfaces for all services
- Implement constructor-based injection
- Update tests to use mocked dependencies
- Add service container for lifecycle management

Breaking: Service initialization signature changed
See docs/MIGRATION.md for details

🤖 Generated with Claude Code
```

### Example 4: Initial Commit

**Filled template:**
```
Initial project structure

- Backend Go directory layout (clean architecture)
- Frontend placeholder for Next.js
- Comprehensive .gitignore
- CI/CD workflow directories
- Project documentation

🤖 Generated with Claude Code
```

### Example 5: Documentation

**Filled template:**
```
Add lecture notes for Lectures 0 and 1A

- Lecture 0: MCP Fundamentals (14KB)
  - MCP architecture and concepts
  - Transport types (stdio, http, sse)
  - Installation and configuration
  - Self-assessment questions

- Lecture 1A: Project Scaffolding (20KB)
  - Golden rules of AI-assisted development
  - Effective prompting strategies
  - TodoWrite usage patterns
  - Practical exercises

- Course Index (14KB)
  - Complete course overview
  - Progress tracking

Total: 46KB of comprehensive course material

🤖 Generated with Claude Code
```

---

## Placeholder Reference

| Placeholder | Description | Example |
|-------------|-------------|---------|
| `{{SHORT_SUMMARY}}` | One-line description | `Add user authentication system` |
| `{{CHANGE_N}}` | Specific change detail | `Implement JWT authentication` |
| `{{OPTIONAL_ADDITIONAL_CONTEXT}}` | Breaking changes, notes | `Breaking: API v1 deprecated` |

---

## Best Practices

### ✅ Do
- Use imperative mood ("Add", "Fix", "Update")
- Keep title under 50 characters
- Add blank line after title
- Use bullets for details
- Explain WHY, not just WHAT
- Include breaking change warnings
- Reference issue numbers if applicable

### ❌ Don't
- Use past tense ("Added", "Fixed")
- Write vague titles ("Update stuff", "Fix bug")
- Skip the blank line
- Write paragraphs (use bullets)
- Commit without running tests
- Include sensitive information
- Use generic messages ("WIP", "temp")

---

## Commit Message Categories

Use these prefixes for consistent categorization:

| Prefix | Use Case | Example |
|--------|----------|---------|
| `Add` | New feature or file | `Add payment processing` |
| `Fix` | Bug fix | `Fix memory leak in handler` |
| `Update` | Enhancement to existing feature | `Update error messages for clarity` |
| `Refactor` | Code restructuring | `Refactor auth middleware` |
| `Remove` | Delete feature or code | `Remove deprecated API v1` |
| `Docs` | Documentation only | `Docs: Add API usage examples` |
| `Test` | Test additions/changes | `Test: Add integration tests for API` |
| `Chore` | Maintenance tasks | `Chore: Update dependencies` |
| `Style` | Code style changes | `Style: Format with gofmt` |
| `Perf` | Performance improvements | `Perf: Optimize database queries` |

---

## GitCommit Command

**Direct prompt to Claude:**
```
Create a git commit with the following changes:
{{DESCRIBE_WHAT_CHANGED}}

Use a professional commit message format with:
- Imperative mood title (50 chars max)
- Blank line
- Bullet points explaining changes
- Attribution footer

Run git status and git diff first to see all changes.
```

---

## Verification Checklist

Before committing:
- [ ] Ran tests (`go test ./...`, `npm test`)
- [ ] Ran linter (`golangci-lint`, `eslint`)
- [ ] No debug code (console.log, print statements)
- [ ] No sensitive data (.env files, API keys)
- [ ] Commit message is descriptive
- [ ] Breaking changes documented

---

**Related Templates**:
- [Pull Request Description](../git/pull-request.md)
- [Branch Naming Convention](../git/branch-naming.md)
- [Changelog Entry](../git/changelog.md)
