# Template: Architecture Planning with Plan Mode

**Category**: Architecture
**Use Case**: Planning non-trivial features or project architecture
**Tool**: EnterPlanMode (Plan Mode)

---

## When to Use Plan Mode

Use Plan Mode for:
- ✅ New feature implementation (multi-file changes)
- ✅ Architectural decisions (multiple valid approaches)
- ✅ Code modifications (affects existing behavior)
- ✅ Multi-component changes (>2-3 files)
- ✅ Unclear requirements (need exploration first)

Don't use for:
- ❌ Simple bug fixes (typos, obvious errors)
- ❌ Adding console.log or single-line changes
- ❌ Pure research tasks (use Explore agent instead)

---

## Template

```
I want to {{FEATURE_DESCRIPTION}}.

Please enter Plan Mode and:

1. Explore existing codebase:
   - {{AREA_1_TO_EXPLORE}}
   - {{AREA_2_TO_EXPLORE}}
   - Identify similar patterns we're already using

2. Design approach considering:
   - {{DESIGN_CONSIDERATION_1}}
   - {{DESIGN_CONSIDERATION_2}}
   - {{DESIGN_CONSIDERATION_3}}

3. Address these questions:
   - {{QUESTION_1}}
   - {{QUESTION_2}}
   - {{QUESTION_3}}

4. In your plan, include:
   - Files to create/modify (with specific paths)
   - Interfaces and key types to define
   - Dependencies needed (external packages)
   - Testing strategy
   - Migration path (if updating existing code)
   - Trade-offs of chosen approach

5. Present options if multiple valid approaches exist:
   - Approach A: {{APPROACH_A_SUMMARY}}
   - Approach B: {{APPROACH_B_SUMMARY}}
   - Recommend one with reasoning

Context:
- {{RELEVANT_CONTEXT_1}}
- {{RELEVANT_CONTEXT_2}}

Constraints:
- {{CONSTRAINT_1}}
- {{CONSTRAINT_2}}
```

---

## Example 1: Adding Authentication

**Filled template:**
```
I want to add JWT-based authentication to the API.

Please enter Plan Mode and:

1. Explore existing codebase:
   - Current middleware structure in backend/internal/middleware/
   - How handlers currently access request context
   - Identify similar patterns we're already using for other middleware

2. Design approach considering:
   - Session vs stateless JWT (prefer stateless for scalability)
   - Refresh token strategy
   - Token storage (where to keep refresh tokens)
   - Password hashing algorithm (bcrypt vs argon2)

3. Address these questions:
   - Should we use access + refresh tokens or just access tokens?
   - Where do we store user sessions/tokens? (Database? Redis?)
   - How do we handle token expiration and renewal?
   - Do we need role-based access control (RBAC) now or later?

4. In your plan, include:
   - Files to create/modify (with specific paths)
   - Interfaces for AuthService, TokenManager
   - Dependencies needed (jwt library, bcrypt)
   - Testing strategy (unit tests for auth logic, integration tests for endpoints)
   - Migration path (existing users need to set passwords)
   - Trade-offs of chosen approach

5. Present options if multiple valid approaches exist:
   - Approach A: Simple JWT with no refresh tokens (easier, less secure)
   - Approach B: Access + refresh tokens (more complex, more secure)
   - Recommend one with reasoning

Context:
- This is an MVP, but we plan to add OAuth (Google, GitHub) later
- Currently no authentication at all
- Using PostgreSQL database

Constraints:
- Must be stateless (for horizontal scaling)
- No third-party auth services yet (Auth0, etc.)
- Should work with CORS for frontend at different domain
```

---

## Example 2: Refactoring Service Layer

**Filled template:**
```
I want to refactor the proposal generation service to use a cleaner interface design and improve testability.

Please enter Plan Mode and:

1. Explore existing codebase:
   - Current ProposalService implementation in internal/services/
   - How handlers interact with the service
   - Existing test coverage and mocking patterns

2. Design approach considering:
   - Dependency injection vs global service instances
   - Interface-first design vs concrete types
   - Separation of Claude API client from business logic
   - Error handling patterns (wrap errors vs custom types)

3. Address these questions:
   - Should ClaudeClient be injected as dependency or service creates it?
   - Do we need a repository pattern for database access (future)?
   - How do we handle retries and timeouts for Claude API?
   - Should validation live in service or handlers?

4. In your plan, include:
   - Files to modify (ProposalService, handlers, tests)
   - New interfaces to define (ProposalService, ClaudeClient, Validator)
   - Dependencies needed (probably none, using existing)
   - Testing strategy (unit tests with mocked Claude API)
   - Migration path (update all handler call sites)
   - Trade-offs of chosen approach (more boilerplate but better testability)

5. Present options if multiple valid approaches exist:
   - Approach A: Constructor injection with interfaces (more Go-idiomatic)
   - Approach B: Builder pattern for complex dependencies
   - Recommend one with reasoning

Context:
- Current service is hard to test (no interfaces, tight coupling)
- Will add database in Lecture 2 (plan for that)
- Using go-playground/validator for input validation

Constraints:
- Don't break existing API contracts
- Keep changes minimal (this is a refactor, not rewrite)
- Must maintain backward compatibility
```

---

## Example 3: Adding New Feature

**Filled template:**
```
I want to add a feature that saves proposal history to the database for logged-in users.

Please enter Plan Mode and:

1. Explore existing codebase:
   - Current ProposalService structure
   - Database schema (if any) in migrations/
   - How we handle user context in handlers

2. Design approach considering:
   - Database schema for proposals (what fields to store)
   - Relationship between users and proposals (one-to-many)
   - Should we store full Claude API response or just the proposal text?
   - Pagination strategy for listing user's proposals

3. Address these questions:
   - Do we add database now or wait for full auth system?
   - What's the migration path (creating tables, indexes)?
   - Should this be optional (degrade gracefully if DB unavailable)?
   - How do we handle database errors without breaking existing flow?

4. In your plan, include:
   - New files to create (models/proposal.go, repository/proposal_repo.go)
   - Files to modify (ProposalService, database/migrations/)
   - Database schema with SQL migration
   - New endpoints (GET /proposals for user's history)
   - Testing strategy (integration tests with test database)
   - Trade-offs of chosen approach

5. Present options if multiple valid approaches exist:
   - Approach A: Add database now, make it required (breaks existing deployments)
   - Approach B: Add database, make it optional (more code but safer)
   - Recommend one with reasoning

Context:
- We're using PostgreSQL (will add in this feature)
- Authentication system doesn't exist yet (use user_id placeholder for now)
- MVP should still work without database (optional feature)

Constraints:
- Use PostgreSQL with pgx driver
- Must not break existing proposal generation for non-authenticated users
- Database calls should timeout after 5 seconds
```

---

## Placeholder Reference

| Placeholder | Description | Example |
|-------------|-------------|---------|
| `{{FEATURE_DESCRIPTION}}` | High-level feature goal | `add JWT-based authentication` |
| `{{AREA_N_TO_EXPLORE}}` | Codebase area to investigate | `middleware structure`, `handler patterns` |
| `{{DESIGN_CONSIDERATION_N}}` | Design decision to think about | `Session vs stateless`, `Performance` |
| `{{QUESTION_N}}` | Specific question to address | `Where do we store tokens?` |
| `{{APPROACH_X_SUMMARY}}` | Summary of an approach | `Simple JWT, no refresh tokens` |
| `{{RELEVANT_CONTEXT_N}}` | Background information | `Using PostgreSQL`, `MVP stage` |
| `{{CONSTRAINT_N}}` | Limitation or requirement | `Must be stateless`, `No breaking changes` |

---

## What Makes a Good Plan Mode Prompt?

### ✅ Do
- State the goal clearly upfront
- Ask Claude to explore existing code first
- List specific design considerations
- Include concrete questions to address
- Provide relevant context (tech stack, stage)
- Mention constraints
- Ask for multiple approaches if applicable

### ❌ Don't
- Be vague ("make it better")
- Start implementing without exploration
- Skip context (Claude needs background)
- Ignore constraints
- Demand a specific solution (let Claude explore options)

---

## After Plan Mode

Once Claude presents the plan:

1. **Review the plan carefully**
   - Does it address all requirements?
   - Are trade-offs clearly explained?
   - Does it fit project architecture?

2. **Ask clarifying questions**
   ```
   - Why did you choose Approach A over B?
   - How does this handle {{EDGE_CASE}}?
   - What about {{CONSIDERATION_I_MISSED}}?
   ```

3. **Approve or request changes**
   ```
   ✅ "Looks good, let's implement Approach B"
   🔄 "Can you modify the plan to use {{ALTERNATIVE}}?"
   ❌ "Let's reconsider the {{ASPECT}} part"
   ```

4. **Implementation begins**
   - Claude exits Plan Mode
   - Uses TodoWrite to track implementation
   - Follows the approved plan

---

## Tips for Effective Planning

1. **Don't skip Plan Mode for non-trivial features**
   - You'll save time by planning upfront
   - Reduces rework and wasted effort

2. **Use AskUserQuestion in plans**
   - Claude can ask you questions during planning
   - Helps clarify ambiguous requirements

3. **Reference existing plans**
   - Link to architecture documents
   - "According to the plan at {{PLAN_FILE_PATH}}"

4. **Be open to Claude's recommendations**
   - AI might suggest better approaches
   - Ask "why" if you disagree

5. **Iterate on the plan**
   - It's okay to refine the plan
   - Better to catch issues early

---

## Plan Mode Commands

```bash
# View current plan (if in Plan Mode session)
/plan

# View and edit plan in Vim
/plan open
```

---

**Related Templates**:
- [Project Structure Scaffolding](../scaffolding/project-structure.md)
- [Feature Implementation Request](../code-generation/feature-request.md)
- [Code Review Request](../code-generation/code-review.md)
