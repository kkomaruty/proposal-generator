# Building Production-Grade Applications with Claude Code

**Course Duration**: 8 Lectures (~12-15 hours total)
**Level**: Intermediate to Advanced
**Prerequisites**: Basic programming knowledge, Git, command line familiarity
**Project**: AI-Powered Proposal Generator for Freelancers

---

## 📚 Course Overview

This hands-on course teaches you how to build production-ready applications using AI-assisted development with Claude Code. You'll learn not just to write code with AI, but to **collaborate effectively** with AI agents through proper prompting, code review, testing, and deployment strategies.

### What Makes This Course Different?

- ✅ **Production-quality**: Not toy examples - real deployment, CI/CD, monitoring
- ✅ **Best practices focused**: Learn the RIGHT way to work with AI agents
- ✅ **Minimal manual coding**: Let AI do heavy lifting, you focus on architecture
- ✅ **Full-stack**: Go backend + Next.js frontend + deployment
- ✅ **Free infrastructure**: Everything runs on free tiers

---

## 🎯 Learning Objectives

By the end of this course, you will:

1. **Master AI collaboration patterns**
   - Write effective prompts for complex tasks
   - Use Plan Mode for architectural decisions
   - Review and refactor AI-generated code
   - Leverage MCP servers for extended capabilities

2. **Build production-ready applications**
   - Clean architecture with separation of concerns
   - Comprehensive testing (unit, integration, E2E)
   - CI/CD pipelines with automated deployment
   - Monitoring, logging, and error handling

3. **Work with modern tech stacks**
   - Go for high-performance backends
   - Next.js 14+ for modern frontends
   - PostgreSQL for reliable data storage
   - Docker for containerization

4. **Deploy to production**
   - Free hosting (Fly.io, Vercel)
   - Custom domains (Cloudflare)
   - SSL/TLS certificates
   - Health checks and monitoring

---

## 📖 Course Structure

### **Lecture 0: Claude Code Ecosystem & MCP Setup** ⏱️ ~45 min

**Status**: ✅ Completed

**Topics Covered**:
- Understanding MCP (Model Context Protocol)
- Transport types: stdio vs http
- Installing and configuring MCP servers
- GitHub MCP setup and testing
- Configuration scopes (local, project, user)

**Key Skills**:
- Install MCP servers with proper authentication
- Understand command anatomy (`--transport`, `--env`, `--`)
- Configure project-level vs user-level MCPs
- Troubleshoot MCP connection issues

**Artifacts**:
- GitHub MCP installed and verified
- Understanding of MCP architecture

**Read**: [LECTURE-00-MCP-FUNDAMENTALS.md](./LECTURE-00-MCP-FUNDAMENTALS.md)

---

### **Lecture 1A: Project Scaffolding** ⏱️ ~60 min

**Status**: ✅ Completed

**Topics Covered**:
- The Golden Rules of AI-assisted development
- Effective prompting strategies
- Standard Go project layout
- Git workflow and commit best practices
- GitHub CLI for repository management
- TodoWrite for progress tracking

**Key Skills**:
- Write specific, actionable prompts
- Use TodoWrite effectively
- Follow Go project conventions (cmd/, internal/, pkg/)
- Create professional commit messages
- Verify AI-generated code

**Artifacts**:
- Project structure scaffolded
- Git repository initialized
- GitHub repository created: [kkomaruty/proposal-generator](https://github.com/kkomaruty/proposal-generator)
- Initial commit with 224 lines

**Read**: [LECTURE-01A-PROJECT-SCAFFOLDING.md](./LECTURE-01A-PROJECT-SCAFFOLDING.md)

---

### **Lecture 1B: Backend Core Implementation** ⏱️ ~90 min

**Status**: 🔜 Next

**Topics to Cover**:
- Writing main.go with HTTP server
- Health check endpoint
- Environment-based configuration
- HTTP router setup (chi)
- Middleware stack:
  - CORS
  - Request logging
  - Request ID generation
  - Error recovery
- Project structure organization

**Key Skills**:
- Prompt for Go code with interfaces
- Request error handling patterns
- Set up structured logging
- Test HTTP endpoints manually

**Artifacts**:
- Working HTTP server with /health endpoint
- Configuration management
- Middleware stack
- Basic integration tests

---

### **Lecture 2: AI Integration & Service Layer** ⏱️ ~120 min

**Status**: 🔜 Upcoming

**Topics to Cover**:
- Claude API client implementation
- Service layer architecture
- Request/response models
- Input validation
- Rate limiting (in-memory)
- Error handling and retries
- Testing with mocked API calls

**Key Skills**:
- Design clean service interfaces
- Handle external API errors gracefully
- Write testable service code
- Mock dependencies for testing

**Artifacts**:
- Claude API client (pkg/claude/)
- Proposal generation service
- Handler with full request cycle
- Unit and integration tests

---

### **Lecture 3: Frontend Development** ⏱️ ~120 min

**Status**: 🔜 Upcoming

**Topics to Cover**:
- Next.js 14+ scaffolding (App Router)
- TypeScript configuration (strict mode)
- Tailwind CSS setup
- shadcn/ui component installation
- Component architecture:
  - ProposalForm
  - ProposalOutput
  - LoadingSpinner
  - ErrorAlert
- API client implementation
- State management with React hooks

**Key Skills**:
- Prompt for React components with TypeScript
- Request professional UI/UX
- Integrate frontend with backend API
- Handle loading and error states

**Artifacts**:
- Next.js application with TypeScript
- Professional UI with shadcn/ui
- Working proposal generation flow
- End-to-end functionality

---

### **Lecture 4: Testing Strategy** ⏱️ ~90 min

**Status**: 🔜 Upcoming

**Topics to Cover**:
- Backend testing:
  - Unit tests for services
  - Integration tests for handlers
  - Table-driven tests in Go
- Frontend testing:
  - Component tests (React Testing Library)
  - Integration tests
  - Mock API responses
- Test coverage reporting
- CI integration

**Key Skills**:
- Request AI to generate comprehensive tests
- Review and improve AI-generated tests
- Achieve meaningful test coverage
- Set up test automation

**Artifacts**:
- Backend test suite with >80% coverage
- Frontend test suite
- Test documentation
- Coverage reports

---

### **Lecture 5: CI/CD Pipeline** ⏱️ ~90 min

**Status**: 🔜 Upcoming

**Topics to Cover**:
- GitHub Actions workflows:
  - Backend CI (lint, test, build)
  - Frontend CI (lint, test, build)
  - Deploy workflow
- Docker containerization:
  - Multi-stage builds
  - Optimization for size
- Security scanning (gosec, npm audit)
- Automated deployment

**Key Skills**:
- Design CI/CD workflows
- Write Dockerfiles for Go and Node
- Set up automated deployments
- Handle secrets in CI

**Artifacts**:
- Complete CI/CD pipeline
- Docker images for backend
- Automated deployment on merge to main
- Security checks integrated

---

### **Lecture 6: Production Deployment** ⏱️ ~120 min

**Status**: 🔜 Upcoming

**Topics to Cover**:
- Backend deployment to Fly.io:
  - fly.toml configuration
  - Environment variables
  - Health checks
  - Scaling configuration
- Frontend deployment to Vercel:
  - Auto-deployment setup
  - Environment variables
  - Edge network configuration
- Database setup (PostgreSQL):
  - Supabase free tier
  - Connection pooling
  - Migrations
- Custom domain setup:
  - Cloudflare DNS
  - SSL/TLS certificates
  - CNAME configuration

**Key Skills**:
- Deploy to production platforms
- Configure custom domains
- Set up SSL/TLS
- Manage production environment variables

**Artifacts**:
- Backend live on Fly.io
- Frontend live on Vercel
- Custom domain configured
- Production database

---

### **Lecture 7: Reliability & Observability** ⏱️ ~90 min

**Status**: 🔜 Upcoming

**Topics to Cover**:
- Production logging:
  - Structured logging
  - Log aggregation
  - Log levels and filtering
- Error monitoring:
  - Sentry integration
  - Error tracking and alerts
- Performance monitoring:
  - Response time tracking
  - API metrics
- Health checks and uptime monitoring:
  - Custom health endpoints
  - External monitoring (UptimeRobot)
- Circuit breakers and retries
- Graceful shutdown

**Key Skills**:
- Implement production-grade logging
- Set up error monitoring
- Configure health checks
- Handle failures gracefully

**Artifacts**:
- Comprehensive logging
- Error monitoring dashboard
- Uptime monitoring
- Alerting configured

---

### **Lecture 8: Code Review & Refactoring** ⏱️ ~90 min

**Status**: 🔜 Upcoming

**Topics to Cover**:
- AI-assisted code review:
  - Request Claude to review own code
  - Identify code smells
  - Suggest improvements
- Refactoring patterns:
  - Extract interfaces
  - Reduce duplication
  - Improve naming
- Performance optimization:
  - Identify bottlenecks
  - Optimize database queries
  - Cache frequently accessed data
- Security best practices:
  - Input sanitization
  - Rate limiting
  - Authentication hardening

**Key Skills**:
- Use AI for code review effectively
- Request and apply refactoring
- Identify security vulnerabilities
- Optimize performance systematically

**Artifacts**:
- Refactored codebase
- Performance improvements documented
- Security audit completed
- Best practices document

---

## 🛠️ Tech Stack

### Backend
- **Language**: Go 1.21+
- **Router**: chi
- **Validation**: go-playground/validator
- **Testing**: standard testing package + testify
- **Logging**: slog (Go standard library)

### Frontend
- **Framework**: Next.js 14+ (App Router)
- **Language**: TypeScript 5+ (strict mode)
- **Styling**: Tailwind CSS 3.4+
- **Components**: shadcn/ui
- **Testing**: Jest + React Testing Library
- **State**: React hooks (no Redux for MVP)

### Infrastructure
- **Backend Hosting**: Fly.io (free tier)
- **Frontend Hosting**: Vercel (free tier)
- **Database**: PostgreSQL on Supabase (free tier)
- **Domain**: Cloudflare (free)
- **CI/CD**: GitHub Actions (free for public repos)
- **Monitoring**: Sentry (free tier)

### AI
- **API**: Claude API (Anthropic)
- **Model**: claude-3-5-sonnet-20241022
- **Integration**: Native HTTP client

---

## 📊 Project Milestones

### Phase 1: Foundation (Lectures 0-1)
- [x] MCP setup and understanding
- [x] Project structure scaffolded
- [x] GitHub repository created
- [ ] Backend HTTP server running
- [ ] Basic health check endpoint

### Phase 2: Core Functionality (Lectures 2-3)
- [ ] Claude API integration
- [ ] Proposal generation working
- [ ] Frontend UI complete
- [ ] End-to-end flow functional

### Phase 3: Quality & Testing (Lecture 4)
- [ ] Backend tests (>80% coverage)
- [ ] Frontend tests
- [ ] Integration tests
- [ ] Test automation in CI

### Phase 4: Production (Lectures 5-6)
- [ ] CI/CD pipeline complete
- [ ] Backend deployed to Fly.io
- [ ] Frontend deployed to Vercel
- [ ] Custom domain configured
- [ ] Database in production

### Phase 5: Reliability (Lecture 7)
- [ ] Logging and monitoring
- [ ] Error tracking
- [ ] Health checks
- [ ] Alerting configured

### Phase 6: Optimization (Lecture 8)
- [ ] Code reviewed and refactored
- [ ] Performance optimized
- [ ] Security hardened
- [ ] Documentation complete

---

## 🎓 Best Practices Summary

### Prompting
- ✅ Be specific with requirements
- ✅ Reference architecture documents
- ✅ Use numbered steps
- ✅ Request TodoWrite tracking
- ✅ Ask for verification

### Code Quality
- ✅ Follow language conventions
- ✅ Separation of concerns
- ✅ Interface-driven design
- ✅ Comprehensive error handling
- ✅ Structured logging

### Testing
- ✅ Unit tests for business logic
- ✅ Integration tests for APIs
- ✅ E2E tests for critical flows
- ✅ >80% coverage target
- ✅ Test automation in CI

### Git Workflow
- ✅ Descriptive commit messages
- ✅ Small, focused commits
- ✅ Feature branches for new work
- ✅ Pull requests with descriptions
- ✅ Code review before merge

### Deployment
- ✅ Environment-based configuration
- ✅ Secrets management
- ✅ Health checks
- ✅ Graceful shutdown
- ✅ Monitoring and alerting

---

## 📈 Progress Tracking

### Completed Lectures
- [x] Lecture 0: MCP Fundamentals
- [x] Lecture 1A: Project Scaffolding
- [ ] Lecture 1B: Backend Core
- [ ] Lecture 2: AI Integration
- [ ] Lecture 3: Frontend Development
- [ ] Lecture 4: Testing Strategy
- [ ] Lecture 5: CI/CD Pipeline
- [ ] Lecture 6: Production Deployment
- [ ] Lecture 7: Reliability & Observability
- [ ] Lecture 8: Code Review & Refactoring

### Current Status
**🎯 Ready for Lecture 1B: Backend Core Implementation**

Project state:
- Repository: https://github.com/kkomaruty/proposal-generator
- Structure: Backend scaffolded, frontend placeholder
- Documentation: README, lecture notes
- Next: Implement main.go and HTTP server

---

## 🔗 Quick Links

- [Lecture 0: MCP Fundamentals](./LECTURE-00-MCP-FUNDAMENTALS.md)
- [Lecture 1A: Project Scaffolding](./LECTURE-01A-PROJECT-SCAFFOLDING.md)
- [Architecture Plan](../../.claude/plans/steady-greeting-avalanche.md)
- [Project README](../../README.md)
- [GitHub Repository](https://github.com/kkomaruty/proposal-generator)

---

## 💡 Tips for Success

1. **Complete lectures in order** - Each builds on previous knowledge
2. **Practice prompting** - Don't just copy prompts, understand why they work
3. **Review AI code** - Never accept code without verification
4. **Ask questions** - Stop and clarify when something is unclear
5. **Experiment** - Try variations of prompts and approaches
6. **Document learnings** - Keep notes on what works and what doesn't
7. **Test thoroughly** - Verify functionality after each lecture
8. **Commit frequently** - Small commits make debugging easier

---

## 🆘 Getting Help

If you get stuck:

1. **Review lecture notes** - Solutions to common issues included
2. **Check self-assessment questions** - Test your understanding
3. **Verify prerequisites** - Ensure tools are installed correctly
4. **Read error messages carefully** - They usually point to the issue
5. **Use `/plan` mode** - Let Claude explore and explain
6. **Ask Claude to explain** - "Explain why this command failed"

---

## 🎉 Course Completion

Upon completing all lectures, you will have:

- ✅ A production-ready web application
- ✅ Live deployment accessible via custom domain
- ✅ Comprehensive test suite
- ✅ Full CI/CD pipeline
- ✅ Monitoring and alerting
- ✅ Professional-quality codebase
- ✅ Mastery of AI-assisted development

**Final Project**: AI-Powered Proposal Generator
- **Backend**: Go API with Claude integration
- **Frontend**: Next.js with professional UI
- **Deployed**: Live on free infrastructure
- **Tested**: >80% code coverage
- **Monitored**: Health checks, error tracking
- **Documented**: Comprehensive README and docs

---

**Course**: Building Production-Grade Applications with Claude Code
**Instructor**: Claude Sonnet 4.5
**Student**: Software Engineer learning AI-assisted development
**Date**: January 2026

---

*Happy learning! 🚀*
