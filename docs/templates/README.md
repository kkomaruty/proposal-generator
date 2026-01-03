# Prompt Templates Library

**Purpose**: Reusable, generalizable prompts for AI-assisted development
**Maintainer**: Course students
**Usage**: Copy template, fill placeholders, prompt Claude

---

## 📚 Template Categories

### 1. [Scaffolding](./scaffolding/) - Project Setup
Initial project structure and boilerplate generation

| Template | Use Case | Language |
|----------|----------|----------|
| [Project Structure](./scaffolding/project-structure.md) | Create directory layout and initialize project | Any |

---

### 2. [Git Workflow](./git/) - Version Control
Git commands, commit messages, PR descriptions

| Template | Use Case | Language |
|----------|----------|----------|
| [Commit Message](./git/commit-message.md) | Professional commit message format | N/A |

---

### 3. [Code Generation](./code-generation/) - Writing Code
Handlers, services, models, and other code structures

| Template | Use Case | Language |
|----------|----------|----------|
| [HTTP Handler](./code-generation/http-handler.md) | RESTful API endpoint with service layer | Go |

---

### 4. [Architecture](./architecture/) - Planning & Design
Architecture planning, design decisions, Plan Mode

| Template | Use Case | Language |
|----------|----------|----------|
| [Plan Mode Prompt](./architecture/plan-mode-prompt.md) | Architectural planning for features | Any |

---

### 5. [Testing](./testing/) - Test Generation
Unit tests, integration tests, E2E tests

| Template | Use Case | Language |
|----------|----------|----------|
| *Coming in Lecture 4* | | |

---

### 6. [Deployment](./deployment/) - Infrastructure
Docker, CI/CD, deployment configurations

| Template | Use Case | Language |
|----------|----------|----------|
| *Coming in Lecture 5* | | |

---

## 🎯 How to Use Templates

### Step 1: Choose Template
Browse categories above and select the template that matches your need.

### Step 2: Read Template Documentation
Each template includes:
- **Description**: What it's for
- **Template**: The prompt with `{{PLACEHOLDERS}}`
- **Examples**: Filled-in versions
- **Placeholder Reference**: Table explaining each placeholder
- **Tips**: Best practices for using the template

### Step 3: Fill Placeholders
Replace all `{{PLACEHOLDER}}` values with your specific details.

**Example**:
```
Template:
Create {{PROJECT_TYPE}} in {{LANGUAGE}}

Filled:
Create REST API in Go
```

### Step 4: Prompt Claude
Copy your filled template and send it to Claude Code.

### Step 5: Verify Output
Always review and verify Claude's generated code.

---

## 📖 Quick Start Examples

### Example 1: Scaffolding a New Project

**Scenario**: Starting a Python FastAPI project

**Template**: [Project Structure](./scaffolding/project-structure.md)

**Filled**:
```
Create the Python FastAPI directory structure.

**Project Root: my-api/**

1. Initialize git repository

2. Create .gitignore covering:
   - Python files (*.pyc, __pycache__, .pytest_cache)
   - Virtual environment (venv/, .venv/)
   - Environment files (.env, .env.local)
   - IDE files (.vscode/, .idea/)

3. Backend structure (Python):
   - Initialize poetry with pyproject.toml
   - Create directory structure:
     - app/routers/ (API endpoints)
     - app/services/ (business logic)
     - app/models/ (Pydantic models)
     - app/database/ (database connection)
     - app/core/ (configuration, dependencies)
     - tests/ (pytest tests)

4. Documentation:
   - Create README.md with setup instructions
   - Add docs/ directory with API.md placeholder

Use TodoWrite to track each step.
```

---

### Example 2: Creating an API Endpoint

**Scenario**: Adding a user login endpoint

**Template**: [HTTP Handler](./code-generation/http-handler.md)

**Filled**:
```
Create a POST handler for /api/v1/auth/login in backend/internal/handlers/auth_handler.go.

**Requirements**:

1. Handler function:
   - Name: HandleLogin
   - Method: POST
   - Request body: LoginRequest (email, password)
   - Response: LoginResponse (access_token, refresh_token, expires_at)

2. Validation:
   - Validate email: required, valid email format
   - Validate password: required, min 8 chars
   - Return 400 on validation failure

3. Service layer:
   - Call AuthService.Authenticate(email, password)
   - Generate JWT tokens on success
   - Return 401 on invalid credentials

4. Error handling:
   - 400: Validation errors
   - 401: Invalid credentials
   - 429: Rate limit (5 attempts per 15 min)
   - 500: Internal errors

Use TodoWrite. Write unit tests with mocked AuthService.
```

---

### Example 3: Planning a Feature

**Scenario**: Adding caching to reduce API calls

**Template**: [Plan Mode Prompt](./architecture/plan-mode-prompt.md)

**Filled**:
```
I want to add caching to reduce Claude API calls for identical prompts.

Please enter Plan Mode and:

1. Explore existing codebase:
   - Current ClaudeClient implementation
   - How proposals are generated in ProposalService

2. Design approach considering:
   - Cache storage (in-memory vs Redis)
   - Cache key generation (hash of prompt + parameters)
   - TTL (time-to-live) strategy
   - Cache invalidation

3. Address these questions:
   - Should we cache per user or globally?
   - What's appropriate TTL (1 hour? 24 hours?)?
   - How do we handle cache misses?
   - Do we need cache warming?

4. In your plan, include:
   - Files to modify
   - Cache interface definition
   - Dependencies (if using Redis)
   - Testing strategy

Context:
- MVP stage, single server (no distributed system yet)
- Claude API is rate-limited and costs money
- Using Go with standard library

Constraints:
- Must be optional (degrade gracefully if cache unavailable)
- No breaking changes to existing API
```

---

## 🎓 Best Practices

### Writing Good Prompts

1. **Be Specific**
   - ❌ "Create authentication"
   - ✅ "Create JWT authentication with email/password, refresh tokens, and bcrypt hashing"

2. **Include Context**
   - Mention your tech stack
   - Explain project stage (MVP vs production)
   - Reference existing patterns

3. **List Requirements**
   - Use numbered or bulleted lists
   - Separate "must-have" from "nice-to-have"
   - Specify validation rules explicitly

4. **Request Testing**
   - "Write unit tests"
   - "Include integration tests"
   - Specify test cases to cover

5. **Ask for TodoWrite**
   - "Use TodoWrite to track progress"
   - Helps you see what's being done

6. **Demand Verification**
   - "Verify with 'go test ./...'"
   - "Check compilation with 'go build'"
   - "Run linter"

### Reviewing AI Output

After Claude generates code:

1. **Read the code** - Don't blindly accept
2. **Check for security issues** - SQL injection, XSS, etc.
3. **Verify tests pass** - Run test suite
4. **Look for best practices** - Does it follow conventions?
5. **Test manually** - Try the feature yourself

---

## 🔧 Customizing Templates

### Adapting to Your Language

Most templates are written for Go but can be adapted:

**Go → Python**:
```
Go: internal/handlers/user_handler.go
Python: app/routers/user_router.py

Go: go.mod
Python: pyproject.toml

Go: go test ./...
Python: pytest
```

**Go → TypeScript/Node**:
```
Go: internal/services/
TypeScript: src/services/

Go: go-playground/validator
TypeScript: zod, joi, or yup

Go: httptest
TypeScript: supertest
```

### Creating Your Own Templates

Found a prompt pattern you use often? Create a template!

**Template format**:
```markdown
# Template: {{TEMPLATE_NAME}}

**Category**: {{CATEGORY}}
**Use Case**: {{USE_CASE}}
**Language**: {{LANGUAGE}}

---

## Template

[Your prompt with {{PLACEHOLDERS}}]

---

## Example

[Filled example]

---

## Placeholder Reference

| Placeholder | Description | Example |
|-------------|-------------|---------|
| ... | ... | ... |
```

**Submit a PR** to add your template to the library!

---

## 📊 Template Statistics

| Category | Templates | Status |
|----------|-----------|--------|
| Scaffolding | 1 | ✅ |
| Git Workflow | 1 | ✅ |
| Code Generation | 1 | ✅ |
| Architecture | 1 | ✅ |
| Testing | 0 | 🔜 Lecture 4 |
| Deployment | 0 | 🔜 Lecture 5 |

**Total**: 4 templates available

---

## 🆘 Troubleshooting

### "Claude didn't follow the template"

**Solutions**:
- Make sure all placeholders are filled (no `{{MISSING}}` left)
- Add more context about your project
- Break complex prompts into smaller steps
- Use TodoWrite to track incremental progress

### "Output doesn't match my expectations"

**Solutions**:
- Be more specific in requirements
- Provide examples of what you want
- Reference existing code patterns to follow
- Ask Claude to explain its approach first

### "Too much boilerplate generated"

**Solutions**:
- Add constraint: "Keep it minimal"
- Specify: "Don't add features I didn't request"
- Review and delete unnecessary code

### "Not enough error handling"

**Solutions**:
- Explicitly list error scenarios
- Ask for specific error types (404, 400, 500)
- Request: "Include comprehensive error handling"

---

## 💡 Tips for Success

1. **Start with templates** - Don't write prompts from scratch
2. **Customize to fit** - Adapt templates to your project
3. **Keep templates updated** - Improve based on experience
4. **Share discoveries** - Submit PRs for new patterns
5. **Review output** - Templates guide Claude, not guarantee perfection
6. **Iterate** - Refine prompts based on results

---

## 📚 Learning Resources

- [Lecture 0: MCP Fundamentals](../lectures/LECTURE-00-MCP-FUNDAMENTALS.md)
- [Lecture 1A: Project Scaffolding](../lectures/LECTURE-01A-PROJECT-SCAFFOLDING.md)
- [Course Index](../lectures/INDEX.md)
- [Claude Code Documentation](https://code.claude.com/docs)

---

## 🤝 Contributing

Have a great prompt template? Share it!

**Steps**:
1. Create template following the format above
2. Add example(s) with filled placeholders
3. Include placeholder reference table
4. Test with Claude to verify it works
5. Submit PR to add to library

**Template locations**:
- Scaffolding: `docs/templates/scaffolding/`
- Git: `docs/templates/git/`
- Code: `docs/templates/code-generation/`
- Architecture: `docs/templates/architecture/`
- Testing: `docs/templates/testing/`
- Deployment: `docs/templates/deployment/`

---

## 📝 Template Requests

Need a template that doesn't exist? Open an issue:

**Template Request Format**:
```
**Category**: (e.g., Code Generation)
**Use Case**: (e.g., Creating a gRPC service)
**Language**: (e.g., Go)
**Description**: What the template should help with
**Example scenario**: When would someone use this?
```

---

## 🎉 Using Templates in the Course

Throughout the course, we'll:
- **Lecture 1B**: Use HTTP Handler template
- **Lecture 2**: Use Service Layer template (to be created)
- **Lecture 4**: Create Testing templates
- **Lecture 5**: Create CI/CD templates
- **Lecture 6**: Create Deployment templates

As we progress, this library will grow!

---

**Remember**: Templates are starting points, not rigid rules. Adapt them to your needs, and always review Claude's output critically.

Happy prompting! 🚀
