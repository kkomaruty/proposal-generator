# Template: Project Structure Scaffolding

**Category**: Scaffolding
**Use Case**: Creating initial project directory structure
**Language**: Any (adapt directories to your stack)

---

## Template

```
Create the {{LANGUAGE}} {{PROJECT_TYPE}} directory structure according to the plan at {{PLAN_FILE_PATH}}.

**Project Root: {{PROJECT_NAME}}/**

1. Initialize git repository in the root

2. Create comprehensive .gitignore covering:
   - {{LANGUAGE}} specific files (binaries, build artifacts)
   - {{FRAMEWORK}} specific files (node_modules, .next, vendor/, etc.)
   - Environment files (.env, .env.local)
   - IDE files (.vscode/, .idea/, *.swp)
   - OS files (.DS_Store, Thumbs.db)

3. {{COMPONENT_1}} structure:
   - Initialize package manager ({{PACKAGE_MANAGER}})
   - Create directory structure:
     - {{DIR_1}}/ ({{PURPOSE_1}})
     - {{DIR_2}}/ ({{PURPOSE_2}})
     - {{DIR_3}}/ ({{PURPOSE_3}})
   - {{ADDITIONAL_SETUP_STEPS}}

4. {{COMPONENT_2}} structure:
   - {{COMPONENT_2_DETAILS}}

5. Documentation:
   - Create docs/ directory
   - Add placeholder for ARCHITECTURE.md
   - Add API.md placeholder (if applicable)

6. Root level:
   - Create README.md with project description, tech stack, and setup instructions
   - Create .github/workflows/ directory for CI/CD
   - Add LICENSE file ({{LICENSE_TYPE}})

Use TodoWrite to track each major step. After completion, verify the structure with tree command or ls -R.
```

---

## Example: Go Backend + Next.js Frontend

**Filled template:**
```
Create the Go backend and Next.js frontend directory structure according to the plan at /Users/username/.claude/plans/my-project-plan.md.

**Project Root: my-awesome-app/**

1. Initialize git repository in the root

2. Create comprehensive .gitignore covering:
   - Go specific files (binaries, build artifacts)
   - Node.js specific files (node_modules, .next)
   - Environment files (.env, .env.local)
   - IDE files (.vscode/, .idea/, *.swp)
   - OS files (.DS_Store, Thumbs.db)

3. Backend structure (Go):
   - Initialize go.mod with module "github.com/username/my-awesome-app"
   - Create directory structure:
     - backend/cmd/api/ (application entry point)
     - backend/internal/handlers/ (HTTP request handlers)
     - backend/internal/services/ (business logic layer)
     - backend/internal/models/ (data structures)
     - backend/internal/middleware/ (HTTP middleware)
     - backend/internal/config/ (configuration management)
     - backend/pkg/client/ (reusable client packages)
     - backend/tests/ (integration tests)

4. Frontend structure:
   - Create frontend/ directory
   - Add README.md noting Next.js will be scaffolded next

5. Documentation:
   - Create docs/ directory
   - Add placeholder for ARCHITECTURE.md
   - Add API.md placeholder

6. Root level:
   - Create README.md with project description, tech stack, and setup instructions
   - Create .github/workflows/ directory for CI/CD
   - Add LICENSE file (MIT)

Use TodoWrite to track each major step. After completion, verify the structure with tree command or ls -R.
```

---

## Placeholder Reference

| Placeholder | Description | Example |
|-------------|-------------|---------|
| `{{PROJECT_NAME}}` | Name of the project | `my-awesome-app` |
| `{{LANGUAGE}}` | Primary programming language | `Go`, `Python`, `TypeScript` |
| `{{PROJECT_TYPE}}` | Type of project | `backend`, `full-stack`, `CLI tool` |
| `{{PLAN_FILE_PATH}}` | Path to architecture plan | `/Users/.../.claude/plans/plan.md` |
| `{{FRAMEWORK}}` | Framework being used | `Next.js`, `Django`, `Express` |
| `{{PACKAGE_MANAGER}}` | Package manager command | `go mod init`, `npm init`, `poetry init` |
| `{{COMPONENT_1}}` | First major component | `Backend`, `API Server`, `Worker` |
| `{{DIR_N}}` | Directory name | `cmd/api`, `internal/handlers` |
| `{{PURPOSE_N}}` | Purpose of directory | `HTTP handlers`, `business logic` |
| `{{LICENSE_TYPE}}` | License type | `MIT`, `Apache-2.0`, `GPL-3.0` |

---

## Tips

1. **Always reference a plan**: Include `{{PLAN_FILE_PATH}}` to give Claude context
2. **Be specific about structure**: List exact directory paths, not just "create backend"
3. **Explain purposes**: Add comments like "(business logic)" to help Claude understand
4. **Request TodoWrite**: Explicitly ask for progress tracking
5. **Ask for verification**: "verify the structure with tree command or ls -R"
6. **Include .gitignore**: Do this BEFORE any files to avoid committing junk

---

## Common Variations

### Python Django Project
```
{{LANGUAGE}} = Python
{{FRAMEWORK}} = Django
{{PACKAGE_MANAGER}} = poetry init
{{DIR_1}} = app/views
{{DIR_2}} = app/models
{{DIR_3}} = app/serializers
```

### Node.js Express API
```
{{LANGUAGE}} = TypeScript
{{FRAMEWORK}} = Express
{{PACKAGE_MANAGER}} = npm init -y
{{DIR_1}} = src/routes
{{DIR_2}} = src/controllers
{{DIR_3}} = src/middleware
```

### Rust CLI Tool
```
{{LANGUAGE}} = Rust
{{PROJECT_TYPE}} = CLI tool
{{PACKAGE_MANAGER}} = cargo init
{{DIR_1}} = src/commands
{{DIR_2}} = src/utils
{{DIR_3}} = tests
```

---

**Related Templates**:
- [Git Commit Message](../git/commit-message.md)
- [README Template](../scaffolding/readme-template.md)
- [Architecture Planning](../architecture/plan-mode-prompt.md)
