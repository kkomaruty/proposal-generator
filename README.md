# AI-Powered Proposal Generator

An intelligent proposal generator for Upwork/Fiverr freelancers, powered by Claude AI.

## Overview

This application helps freelancers generate winning, personalized proposals by analyzing job descriptions and creating tailored responses using AI.

## Tech Stack

### Backend
- **Language**: Go 1.21+
- **API**: RESTful with standard library + chi router
- **AI Integration**: Claude API (Anthropic)
- **Deployment**: Fly.io

### Frontend
- **Framework**: Next.js 14+ (App Router)
- **Language**: TypeScript (strict mode)
- **Styling**: Tailwind CSS + shadcn/ui
- **Deployment**: Vercel

## Project Structure

```
proposal-generator/
├── backend/                 # Go API server
│   ├── cmd/api/            # Application entry point
│   ├── internal/           # Private application code
│   │   ├── handlers/       # HTTP request handlers
│   │   ├── services/       # Business logic
│   │   ├── models/         # Data structures
│   │   ├── middleware/     # HTTP middleware
│   │   └── config/         # Configuration management
│   ├── pkg/                # Public libraries
│   │   ├── claude/         # Claude API client
│   │   └── validator/      # Input validation
│   └── tests/              # Integration tests
├── frontend/               # Next.js application
├── docs/                   # Documentation
└── .github/workflows/      # CI/CD pipelines
```

## Getting Started

### Prerequisites
- Go 1.21 or higher
- Node.js 18+ and npm
- Claude API key
- Git

### Backend Setup
```bash
cd backend
go mod download
go run cmd/api/main.go
```

### Frontend Setup
```bash
cd frontend
npm install
npm run dev
```

## Development

This project follows clean architecture principles:
- **Separation of Concerns**: Clear boundaries between layers
- **Dependency Injection**: Testable, loosely coupled code
- **API-First Design**: Well-defined contracts between services

## Environment Variables

### Backend
- `CLAUDE_API_KEY` - Your Claude API key
- `PORT` - Server port (default: 8080)
- `ALLOWED_ORIGINS` - CORS allowed origins

### Frontend
- `NEXT_PUBLIC_API_URL` - Backend API URL

## Testing

```bash
# Backend tests
cd backend && go test ./...

# Frontend tests
cd frontend && npm test
```

## Deployment

- **Backend**: Deployed to Fly.io (see `backend/fly.toml`)
- **Frontend**: Deployed to Vercel (auto-deploy on push to main)

## CI/CD

GitHub Actions workflows handle:
- Linting and code quality checks
- Running test suites
- Building Docker images
- Automated deployment

## Documentation

- [Architecture Decisions](docs/ARCHITECTURE.md)
- [API Documentation](docs/API.md) - Coming soon
- [Deployment Guide](docs/DEPLOYMENT.md) - Coming soon

## License

MIT

## Contributing

This is a learning project. Contributions welcome!

---

Built with Claude Code as part of a production-ready development course.
