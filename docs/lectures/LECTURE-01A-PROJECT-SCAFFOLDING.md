# Lecture 1A: Project Scaffolding & AI-Assisted Development

**Duration**: ~60 minutes
**Prerequisites**: Lecture 0 completed, Git installed, GitHub account
**Objective**: Learn effective prompting for project setup and scaffolding

---

## Table of Contents
1. [The Golden Rules of AI-Assisted Development](#the-golden-rules)
2. [Effective Prompting Strategies](#effective-prompting-strategies)
3. [Project Structure Design](#project-structure-design)
4. [Hands-On: Scaffolding the Project](#hands-on-scaffolding)
5. [Git Workflow & GitHub Setup](#git-workflow--github-setup)
6. [TodoWrite Best Practices](#todowrite-best-practices)
7. [Code Review & Verification](#code-review--verification)
8. [Key Takeaways](#key-takeaways)
9. [Self-Assessment](#self-assessment)

---

## The Golden Rules

### Rule 1: Start with Planning, Not Coding
- Use Plan Mode (`/plan` or EnterPlanMode) for non-trivial features
- Let Claude explore the codebase before making changes
- Get architectural alignment before writing code

### Rule 2: Be Specific, Not Prescriptive

**❌ Bad Prompt**:
```
Add authentication
```

**✅ Good Prompt**:
```
Implement JWT-based authentication with refresh tokens.
Users should register with email/password. Store hashed
passwords using bcrypt. Include middleware for protected routes.
```

**Why it's better**:
- Specific implementation details (JWT, bcrypt)
- Clear requirements (email/password registration)
- Mentions architecture (middleware)
- Claude knows exactly what to build

### Rule 3: Iterate in Small Chunks
- Break large features into digestible tasks
- Use TodoWrite to track progress
- Review and test each chunk before moving on

### Rule 4: Let Claude Read Before Writing
- Never assume Claude knows your codebase structure
- Always let it read existing files first
- Use the Explore agent for understanding patterns

### Rule 5: Review Everything
- After Claude writes significant code, review it
- Ask Claude to review its own code
- Use the Task tool for code review tasks

### Rule 6: Tests Are Non-Negotiable
- Request tests alongside features
- Ask for unit, integration, and e2e tests
- Use tests to validate behavior

---

## Effective Prompting Strategies

### Anatomy of a Good Scaffolding Prompt

**Example: Backend Scaffolding**

```
Create the Go backend directory structure according to the plan at
/Users/taeksookim/.claude/plans/steady-greeting-avalanche.md.

**Project Root: proposal-generator/**

1. Initialize git repository in the root

2. Create comprehensive .gitignore covering:
   - Go binaries and vendor/
   - Node.js node_modules/
   - Environment files (.env)
   - IDE files (.vscode/, .idea/)
   - OS files (.DS_Store)

3. Backend structure (Go):
   - Initialize go.mod with module "github.com/kkomaruty/proposal-generator" and Go 1.21+
   - Create directory structure:
     - backend/cmd/api/ (entry point)
     - backend/internal/handlers/ (HTTP handlers)
     - backend/internal/services/ (business logic)
     - backend/internal/models/ (data structures)
     - backend/internal/middleware/ (CORS, logging, rate limit)
     - backend/internal/config/ (configuration)
     - backend/pkg/claude/ (Claude API client)
     - backend/pkg/validator/ (input validation)
     - backend/tests/ (integration tests)

4. Frontend structure (placeholder for Next.js - we'll scaffold this next):
   - Create empty frontend/ directory with a README.md noting it will be Next.js

5. Documentation:
   - Create docs/ directory
   - Add placeholder for ARCHITECTURE.md

6. Root level:
   - Create basic README.md with project description
   - Create .github/workflows/ directory (empty for now)

Use TodoWrite to track each major step. After completion, verify the structure
with tree command or ls -R.
```

### What Makes This Prompt Effective?

| Element | Why It Works |
|---------|-------------|
| **References plan** | "according to the plan at..." gives context |
| **Numbered steps** | Easy to track, clear sequence |
| **Detailed paths** | Exact directory structure specified |
| **Explains purpose** | Comments like "(entry point)", "(business logic)" |
| **Technology versions** | "Go 1.21+", "Next.js" - specific requirements |
| **Verification request** | "verify the structure" - asks Claude to check work |
| **TodoWrite mention** | Explicitly requests progress tracking |

---

## Project Structure Design

### Standard Go Project Layout

Our project follows the **Standard Go Project Layout**:

```
backend/
├── cmd/                  # Main applications
│   └── api/             # API server entry point
│       └── main.go      # Application bootstrap
├── internal/            # Private application code
│   ├── handlers/        # HTTP request handlers
│   ├── services/        # Business logic layer
│   ├── models/          # Data structures
│   ├── middleware/      # HTTP middleware (CORS, auth, etc.)
│   └── config/          # Configuration management
├── pkg/                 # Public libraries (can be imported)
│   ├── claude/          # Claude API client package
│   └── validator/       # Input validation utilities
├── tests/               # Integration and E2E tests
├── go.mod               # Go module definition
└── go.sum               # Dependency checksums
```

### Why This Structure?

#### `cmd/` - Command Entry Points
- **Purpose**: Executable applications
- **Convention**: `cmd/api/` for API server, `cmd/worker/` for background jobs
- **Best Practice**: Keep main.go minimal, delegate to internal packages

#### `internal/` - Private Application Code
- **Purpose**: Code that cannot be imported by other projects
- **Go special**: `internal/` is enforced by the Go compiler
- **Benefit**: Prevents external dependencies on implementation details

#### `pkg/` - Public Libraries
- **Purpose**: Code that can be imported by other projects
- **Use Case**: Reusable utilities, clients, shared types
- **Best Practice**: Only put truly reusable code here

#### `tests/` - Integration Tests
- **Purpose**: Integration and E2E tests
- **Convention**: Separate from unit tests (which live next to code)
- **Best Practice**: Test full request/response cycles

---

## Hands-On: Scaffolding

### Step 1: Project Root & Git

**Commands executed:**
```bash
mkdir -p proposal-generator
cd proposal-generator
git init
git branch -m main  # Rename master → main (modern best practice)
```

**Why `main` instead of `master`?**
- Modern convention (GitHub, GitLab default)
- More inclusive terminology
- Industry standard since 2020

---

### Step 2: .gitignore

**Created**: `.gitignore` with comprehensive patterns

**Key sections:**
```gitignore
# Go
*.exe
*.dll
*.so
*.dylib
vendor/
*.test
*.out

# Node.js
node_modules/
npm-debug.log*

# Next.js
.next/
out/
build/

# Environment
.env
.env.local
*.env

# IDE
.vscode/
.idea/
.DS_Store
```

**Teaching Point**: .gitignore is **critical**
- Prevents committing binaries, dependencies, secrets
- Keeps repository size small
- Avoids merge conflicts on generated files

---

### Step 3: Backend Structure

**Command executed:**
```bash
mkdir -p backend/{cmd/api,internal/{handlers,services,models,middleware,config},pkg/{claude,validator},tests}
```

**Bash brace expansion breakdown:**
```bash
backend/{cmd/api,internal}
# Expands to:
backend/cmd/api
backend/internal

internal/{handlers,services,models}
# Expands to:
internal/handlers
internal/services
internal/models
```

**Result**: 12 directories created in one command!

---

### Step 4: Go Module Initialization

**Command executed:**
```bash
cd backend
go mod init github.com/kkomaruty/proposal-generator
```

**What this does:**
- Creates `go.mod` file
- Sets module path (import path for your code)
- Specifies Go version

**go.mod contents:**
```go
module github.com/kkomaruty/proposal-generator

go 1.22.1
```

**Why `github.com/username/project`?**
- Standard convention for Go modules
- Even for private projects
- Makes future open-sourcing easier
- go get can fetch it: `go get github.com/kkomaruty/proposal-generator`

---

### Step 5: Frontend Placeholder

**Created:**
- `frontend/` directory
- `frontend/README.md` explaining Next.js will be added later

**Why not scaffold Next.js now?**
1. **Focus**: One thing at a time (backend first)
2. **Teaching**: Learn scaffolding incrementally
3. **Practical**: Can develop backend independently

---

### Step 6: Documentation Structure

**Created:**
- `docs/` directory
- `docs/ARCHITECTURE.md` placeholder
- Root `README.md` with project overview

**Documentation is non-negotiable:**
- Future you will thank present you
- Helps teammates understand decisions
- Makes project shareable/open-sourceable

---

### Step 7: GitHub Actions Setup

**Created:**
- `.github/workflows/` directory (empty)
- Ready for CI/CD pipelines in later lectures

**Why create it now?**
- Part of modern project structure
- Signals intent (we'll add CI/CD)
- Empty directories are fine in git

---

## Git Workflow & GitHub Setup

### Making the Initial Commit

**Commands executed:**
```bash
git add .
git commit -m "Initial project structure

- Backend Go directory layout (clean architecture)
- Frontend placeholder for Next.js
- Comprehensive .gitignore
- CI/CD workflow directories
- Project documentation

🤖 Generated with Claude Code"
```

### Anatomy of a Good Commit Message

```
Short, descriptive title (50 chars max)    ← What changed
                                           ← Blank line
- Bullet point explaining detail           ← Why/what in detail
- Another detail
- More context

🤖 Generated with Claude Code              ← Attribution (optional)
```

**Why this format?**
- Title shows in `git log --oneline`
- Body explains context (why, not just what)
- Bullets make scanning easy
- Attribution credits AI assistance

---

### GitHub CLI Workflow

**Step 1: Install & Authenticate**
```bash
# macOS
brew install gh

# Authenticate
gh auth login
# Follow prompts: GitHub.com → HTTPS → Yes → Browser
```

**Step 2: Create Repository**
```bash
# Option 1: Single command (if we had it earlier)
gh repo create proposal-generator --public --source=. --remote=origin --push

# Option 2: Manual (what we did)
# Repo created via web, then:
git remote add origin https://github.com/kkomaruty/proposal-generator.git
git push -u origin main
```

**Step 3: Verify**
```bash
gh repo view kkomaruty/proposal-generator
```

### Git Remote Configuration

**Check remotes:**
```bash
git remote -v
```

**Output:**
```
origin  https://github.com/kkomaruty/proposal-generator.git (fetch)
origin  https://github.com/kkomaruty/proposal-generator.git (push)
```

**What is a remote?**
- Named reference to a repository URL
- `origin` is conventional name for main remote
- Can have multiple remotes (origin, upstream, etc.)

---

## TodoWrite Best Practices

### How We Used TodoWrite

**Initial todos:**
```json
[
  {"content": "Create proposal-generator root directory", "status": "in_progress"},
  {"content": "Initialize git repository", "status": "pending"},
  {"content": "Create comprehensive .gitignore", "status": "pending"},
  {"content": "Create backend Go directory structure", "status": "pending"},
  {"content": "Initialize go.mod with proper module path", "status": "pending"},
  {"content": "Create frontend directory placeholder", "status": "pending"},
  {"content": "Create docs directory and structure", "status": "pending"},
  {"content": "Create root README.md", "status": "pending"},
  {"content": "Create .github/workflows directory", "status": "pending"},
  {"content": "Verify complete directory structure", "status": "pending"}
]
```

### TodoWrite Pattern

**1. Break into specific tasks** (not vague)
```
❌ "Set up project"
✅ "Create backend Go directory structure"
✅ "Initialize go.mod with proper module path"
```

**2. One task in_progress at a time**
```
✅ in_progress: "Initialize git repository"
❌ in_progress: "Initialize git repository"
❌ in_progress: "Create .gitignore"  ← Multiple in_progress = bad
```

**3. Update immediately after completion**
```javascript
// Complete task → Mark completed → Move to next
"Create .gitignore" → completed → "Create backend structure" → in_progress
```

**4. Use active voice in activeForm**
```json
{
  "content": "Initialize go.mod",        // Imperative: what needs doing
  "activeForm": "Initializing go.mod",  // Present continuous: what's happening
  "status": "in_progress"
}
```

### Why TodoWrite Matters

| Benefit | Explanation |
|---------|-------------|
| **Transparency** | You see what Claude is doing in real-time |
| **Accountability** | Claude must complete tasks, not skip steps |
| **Progress tracking** | Clear visual feedback on completion |
| **Debugging** | If something goes wrong, you know which step failed |
| **Learning** | Shows you how to break down complex tasks |

---

## Code Review & Verification

### Always Verify AI Work

**After scaffolding, we verified:**

1. **Directory structure**
   ```bash
   ls -R
   find . -type d | sort
   ```

2. **Git status**
   ```bash
   git status
   git log --oneline
   ```

3. **File contents**
   ```bash
   cat backend/go.mod
   cat .gitignore
   cat README.md
   ```

4. **GitHub sync**
   ```bash
   gh repo view kkomaruty/proposal-generator
   gh api repos/kkomaruty/proposal-generator/contents
   ```

### Verification Checklist

```
✅ All directories created
✅ .gitignore includes Go, Node, env files
✅ go.mod has correct module path
✅ README.md has project description
✅ Git initialized with main branch
✅ Initial commit includes all files
✅ GitHub repo created and synced
✅ Remote configured correctly
```

### What to Look For When Reviewing

**File Structure:**
- [ ] Follows conventions (cmd/, internal/, pkg/)
- [ ] No typos in directory names
- [ ] Placeholder files have useful content

**Git:**
- [ ] .gitignore comprehensive
- [ ] Commit message descriptive
- [ ] No sensitive files committed

**Configuration:**
- [ ] go.mod has correct module path
- [ ] Go version matches your installation
- [ ] Remote URL is correct

---

## Key Takeaways

### ✅ Prompting Best Practices

1. **Be specific**: Include exact paths, versions, requirements
2. **Reference plans**: Point to architecture documents
3. **Use numbered steps**: Makes tracking easier
4. **Request TodoWrite**: Explicitly ask for progress tracking
5. **Ask for verification**: "Verify the structure with..."

### ✅ Project Structure Principles

1. **Follow conventions**: Use standard layouts (cmd/, internal/, pkg/)
2. **Separation of concerns**: Handlers → Services → Models
3. **Think ahead**: Create directories you'll need (tests/, docs/)
4. **Document structure**: README explains layout

### ✅ Git Workflow

1. **Initialize early**: `git init` before writing code
2. **Comprehensive .gitignore**: Cover all platforms, tools
3. **Modern defaults**: Use `main` branch, not `master`
4. **Descriptive commits**: Title + body with bullets
5. **Verify push**: Check GitHub UI or `gh` CLI

### ✅ AI Collaboration

1. **TodoWrite for transparency**: You see progress in real-time
2. **Verify everything**: Don't assume, check the output
3. **Iterate incrementally**: Small steps, frequent checks
4. **Review before proceeding**: Validate each phase

---

## Self-Assessment

### Question 1
**Why do we use `internal/` instead of just putting everything in `backend/`?**

<details>
<summary>Answer</summary>

Go's `internal/` directory is special - code here cannot be imported by other projects. The Go compiler enforces this. This:
- Prevents external dependencies on implementation details
- Enforces encapsulation
- Gives you freedom to refactor internal code without breaking anyone

</details>

---

### Question 2
**What's wrong with this prompt?**
```
Create the backend
```

<details>
<summary>Answer</summary>

Too vague! It should specify:
- Technology/language (Go)
- Directory structure (cmd/, internal/, pkg/)
- Module initialization (go.mod with path)
- What goes in each directory
- Conventions to follow

Better: "Create Go backend with cmd/api/, internal/{handlers,services,models}, initialize go.mod as github.com/user/repo, following Standard Go Project Layout"

</details>

---

### Question 3
**When should you mark a todo as `completed` in TodoWrite?**

<details>
<summary>Answer</summary>

**Immediately after finishing the task**, not when batching multiple tasks.

❌ Bad: Complete 3 tasks, then mark all 3 completed
✅ Good: Complete task 1 → mark completed → start task 2 → complete it → mark completed

This gives real-time feedback and prevents forgetting to mark items.

</details>

---

### Question 4
**Why did we create the `frontend/` directory but not scaffold Next.js yet?**

<details>
<summary>Answer</summary>

**Focus and incremental learning**:
1. One thing at a time (backend first)
2. Backend can be developed independently
3. Teaches scaffolding step-by-step
4. Allows backend testing before frontend integration

Practical benefit: Can deploy and test backend API separately.

</details>

---

### Question 5
**Fix this commit message:**
```
git commit -m "stuff"
```

<details>
<summary>Answer</summary>

```bash
git commit -m "Initial project structure

- Backend Go directory layout (clean architecture)
- Frontend placeholder for Next.js
- Comprehensive .gitignore
- CI/CD workflow directories
- Project documentation

🤖 Generated with Claude Code"
```

Good commit has:
- Descriptive title (what changed)
- Blank line
- Bullet points (details)
- Context (why/how)

</details>

---

### Question 6
**How do you verify that your code was successfully pushed to GitHub?**

<details>
<summary>Answer</summary>

Multiple methods:

**1. GitHub CLI:**
```bash
gh repo view username/repo
gh api repos/username/repo/contents
```

**2. Git commands:**
```bash
git remote -v  # Check remote configured
git log origin/main  # See remote commits
```

**3. Browser:**
- Visit https://github.com/username/repo
- Check files are visible
- Verify README displays

**4. Clone test:**
```bash
cd /tmp
git clone https://github.com/username/repo
ls -R repo/
```

</details>

---

## Common Mistakes & Solutions

### Mistake 1: Vague Prompts
**Problem**: "Set up the project"
**Solution**: Specify technology, structure, conventions

### Mistake 2: Not Using TodoWrite
**Problem**: Lose track of what's been done
**Solution**: Explicitly request TodoWrite in prompts

### Mistake 3: No Verification
**Problem**: Assume AI did it correctly
**Solution**: Always verify with ls, cat, git status

### Mistake 4: Committing Sensitive Files
**Problem**: .env files in git
**Solution**: Comprehensive .gitignore BEFORE first commit

### Mistake 5: Poor Commit Messages
**Problem**: "update" or "fix"
**Solution**: Descriptive title + body with bullets

---

## Practical Exercise

**Your turn!** Try scaffolding a simple project:

**Task**: Create a "todo-api" project

**Prompt to write**:
```
Create a Go REST API project called "todo-api" with:
1. Standard Go project layout (cmd/, internal/, pkg/)
2. Routes for: GET /todos, POST /todos, DELETE /todos/:id
3. In-memory storage (no database)
4. Proper .gitignore
5. README with API documentation

Use TodoWrite to track progress. Initialize git and go.mod.
```

**What to verify**:
- [ ] Directory structure matches conventions
- [ ] go.mod initialized correctly
- [ ] .gitignore comprehensive
- [ ] README explains API endpoints
- [ ] Git initialized with good commit message

---

## Project State After Lecture 1A

```
✅ Repository: https://github.com/kkomaruty/proposal-generator
✅ Commit: "Initial project structure" (224 lines)
✅ Structure: Backend scaffolded, frontend placeholder
✅ Documentation: README, ARCHITECTURE placeholder
✅ Git: Initialized with main branch, pushed to GitHub
✅ Next: Implement backend core (main.go, handlers, services)
```

---

## Next Lecture

**Lecture 1B: Backend Core Implementation**
- Writing main.go with HTTP server
- Health check endpoint
- Config management with environment variables
- HTTP router setup (chi)
- Middleware stack (CORS, logging, request ID)
- Claude API client skeleton

---

**Course**: Building Production-Grade Applications with Claude Code
**Instructor**: Claude Sonnet 4.5
**Date**: January 2026
