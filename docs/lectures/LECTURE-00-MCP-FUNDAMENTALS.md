# Lecture 0: Claude Code Ecosystem & MCP Setup

**Duration**: ~45 minutes
**Prerequisites**: Node.js, Go installed
**Objective**: Understand and configure MCP (Model Context Protocol) servers

---

## Table of Contents
1. [What is MCP?](#what-is-mcp)
2. [MCP Architecture](#mcp-architecture)
3. [Transport Types](#transport-types)
4. [Installation & Configuration](#installation--configuration)
5. [Command Anatomy](#command-anatomy)
6. [Practical Exercise](#practical-exercise)
7. [Key Takeaways](#key-takeaways)
8. [Self-Assessment](#self-assessment)

---

## What is MCP?

**MCP (Model Context Protocol)** is Claude Code's plugin system that extends capabilities beyond basic file operations and bash commands.

### The Problem MCP Solves

**Without MCP:**
```
You: "Check the database schema"
Claude: "Let me write a bash command to run psql..."
*Writes complex SQL query, formats output, parses results*
```

**With MCP:**
```
You: "Check the database schema"
Claude: *Uses PostgreSQL MCP server*
*Directly queries schema with structured data*
```

### How MCP Works

```
┌─────────────────┐
│   You (User)    │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Claude Code    │ ◄─── Uses tools
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  MCP Servers    │ ◄─── Extended capabilities
│  (Plugins)      │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ External System │
│ (DB, API, etc)  │
└─────────────────┘
```

**Key Concept**: MCP servers are background processes that expose tools to Claude Code. When you install an MCP server, Claude gains new capabilities.

---

## MCP Architecture

### Built-in Tools vs MCP Tools

| Built-in Tools | MCP-Added Tools |
|----------------|-----------------|
| Read, Write, Edit (files) | Direct database access |
| Bash (shell commands) | API integrations (GitHub, Slack) |
| Grep, Glob (search) | Specialized operations (Docker, K8s) |
| Task (spawn agents) | Custom business logic |

### Benefits of MCP

1. **Direct Integration**: No need to write wrapper code
2. **Structured Data**: Type-safe responses from systems
3. **Authentication**: MCP handles OAuth, tokens, etc.
4. **Reusability**: Install once, use everywhere

---

## Transport Types

MCP servers use different **transports** to communicate with Claude Code:

### 1. stdio (Standard Input/Output)

**How it works**: Claude Code launches a local process, communicates via stdin/stdout

**Process Model**:
```
┌──────────────┐    stdin/stdout    ┌─────────────────┐
│ Claude Code  │ ◄─────────────────► │ MCP Process     │
│              │                      │ (runs locally)  │
└──────────────┘                      └─────────────────┘
```

**Use case**: Local tools, npm packages, Python scripts

**Example**:
```bash
claude mcp add --transport stdio github \
  --env GITHUB_TOKEN=ghp_token \
  -- npx -y @modelcontextprotocol/server-github
```

**Pros**:
- Low latency (local execution)
- Full control over the process
- Works offline

**Cons**:
- Requires package installation
- Manual updates needed

---

### 2. http (HTTP/REST)

**How it works**: Claude Code makes HTTP requests to a remote server

**Process Model**:
```
┌──────────────┐   HTTP requests    ┌─────────────────┐
│ Claude Code  │ ─────────────────► │ Remote MCP      │
│              │ ◄───────────────── │ (cloud hosted)  │
└──────────────┘   HTTP responses   └─────────────────┘
```

**Use case**: Cloud-hosted MCP servers, managed services

**Example**:
```bash
claude mcp add --transport http notion \
  --header "Authorization: Bearer token" \
  https://mcp.notion.com/mcp
```

**Pros**:
- No local installation
- Auto-updates (server-side)
- Can use OAuth authentication

**Cons**:
- Network latency
- Requires internet connection
- May have usage costs

---

### 3. sse (Server-Sent Events)

**Status**: Deprecated - use HTTP instead

---

### Transport Comparison

| Feature | stdio | http |
|---------|-------|------|
| **Latency** | Low (local) | Higher (network) |
| **Setup** | Install package | Just add URL |
| **Security** | Tokens in local config | Can use OAuth |
| **Debugging** | Can inspect process | Easier (HTTP logs) |
| **Updates** | Manual (npx caches) | Server-side |
| **Cost** | Free (runs locally) | May require hosting |

---

## Installation & Configuration

### Management Commands

```bash
# List installed MCP servers
claude mcp list

# Get details for specific server
claude mcp get <server-name>

# Remove a server
claude mcp remove <server-name>

# Check status in Claude Code
/mcp
```

### Configuration Scopes

MCP servers can be installed at different scopes:

| Scope | Location | File | Use Case |
|-------|----------|------|----------|
| **Local** (default) | Project-specific, private | `~/.claude.json` | Personal dev servers, experiments |
| **Project** | Shared with team, in git | `.mcp.json` (project root) | Team collaboration, project tools |
| **User** | Cross-project, private | `~/.claude.json` | Utilities for all projects |

**Add to specific scope**:
```bash
# Local scope (default)
claude mcp add --transport stdio server -- command

# Project scope (shared via git)
claude mcp add --transport stdio server --scope project -- command

# User scope (all your projects)
claude mcp add --transport stdio server --scope user -- command
```

---

## Command Anatomy

Let's break down the installation command:

```bash
claude mcp add --transport stdio github \
  --env GITHUB_TOKEN=your_token_here \
  -- npx -y @modelcontextprotocol/server-github
```

### Part-by-Part Explanation

#### 1. `claude mcp add`
- **What**: Registers a new MCP server with Claude Code
- **Analogy**: Like installing a plugin in VS Code

#### 2. `--transport stdio`
- **What**: Specifies communication method
- **Options**: `stdio`, `http`, `sse` (deprecated)
- **Why**: Determines how Claude Code talks to the MCP server

#### 3. `github` (server name)
- **What**: Identifier for this MCP server
- **Usage**: Reference it with `claude mcp remove github`
- **Note**: Must be unique

#### 4. `--env GITHUB_TOKEN=your_token_here`
- **What**: Passes environment variables to the MCP process
- **Usage**: Multiple vars: `--env VAR1=val1 --env VAR2=val2`
- **Security**: Tokens stored in `~/.claude.json` - keep secure!

#### 5. `--` (double dash separator)
- **Critical**: Everything after `--` is the command to run the MCP server
- **Why needed**: Separates Claude's options from the MCP command
- **Example**:
  ```bash
  # WRONG - Claude tries to parse npx flags
  claude mcp add --transport stdio github --env TOKEN=xyz npx -y server

  # CORRECT - Claude knows where its options end
  claude mcp add --transport stdio github --env TOKEN=xyz -- npx -y server
  ```

#### 6. `npx -y @modelcontextprotocol/server-github`
- **What**: The command that starts the MCP server
- **npx**: Node.js package executor (runs npm packages)
- **-y**: Auto-confirm (don't prompt)
- **@modelcontextprotocol/server-github**: The npm package

---

## Practical Exercise

### Exercise 1: Install GitHub MCP

**Step 1**: Get GitHub Personal Access Token
1. Go to: https://github.com/settings/tokens/new
2. Name: "Claude Code MCP"
3. Scopes: `repo`, `workflow`
4. Generate and copy token (starts with `ghp_...`)

**Step 2**: Install the MCP server
```bash
claude mcp add --transport stdio github \
  --env GITHUB_TOKEN=ghp_your_actual_token \
  -- npx -y @modelcontextprotocol/server-github
```

**Step 3**: Verify installation
```bash
claude mcp list
```

Expected output:
```
github (stdio)
  Command: npx -y @modelcontextprotocol/server-github
  Status: ✓ Connected
```

**Step 4**: Check configuration file
```bash
cat ~/.claude.json
```

Should show:
```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_TOKEN": "ghp_..."
      }
    }
  }
}
```

### Exercise 2: Test the MCP

In Claude Code, try:
```
Create a GitHub repository called "mcp-test" with description "Testing MCP"
```

Claude will use the GitHub MCP to create the repo directly!

---

## Key Takeaways

### ✅ Core Concepts

1. **MCP extends Claude's capabilities** beyond file operations
2. **Transport types** determine how Claude communicates with MCP servers
3. **stdio for local**, **http for cloud** services
4. **Configuration scopes** control sharing (local vs project vs user)
5. **Double dash `--`** separates Claude options from MCP command

### ✅ Best Practices

1. **Use project scope** for team-shared MCP servers
2. **Store sensitive tokens** securely (not in git if using project scope)
3. **Verify installation** with `claude mcp list` after setup
4. **Test MCP servers** before relying on them
5. **Document which MCPs** your project needs in README

### ✅ Common Issues & Solutions

| Issue | Cause | Solution |
|-------|-------|----------|
| "No MCP servers configured" in session | Session started before install | Restart Claude Code session |
| "Command not found" | Missing `--` separator | Add `--` before MCP command |
| "Authentication failed" | Wrong token or expired | Regenerate token, reinstall |
| "MCP server timeout" | Process takes too long to start | Increase timeout with `MCP_TIMEOUT=10000` |

---

## Self-Assessment

Test your understanding:

### Question 1
**What's the difference between stdio and http transports?**

<details>
<summary>Answer</summary>

- **stdio**: Runs locally, communicates via stdin/stdout, low latency, requires installation
- **http**: Runs remotely, communicates via HTTP, higher latency, no local installation

</details>

---

### Question 2
**What does the `--` separator do?**

<details>
<summary>Answer</summary>

It separates Claude Code's options from the MCP server command. Everything after `--` is passed as the command to run the MCP server, not parsed by Claude.

</details>

---

### Question 3
**When should you use project scope vs local scope?**

<details>
<summary>Answer</summary>

- **Local scope**: Personal experiments, sensitive credentials, project-specific configs you don't want to share
- **Project scope**: Team collaboration, standard tools everyone needs, configs that should be version controlled

</details>

---

### Question 4
**Fix this command:**
```bash
claude mcp add --transport stdio db --env DB_URL=localhost npx server-postgres
```

<details>
<summary>Answer</summary>

```bash
claude mcp add --transport stdio db --env DB_URL=localhost -- npx server-postgres
```

Missing `--` before `npx`

</details>

---

### Question 5
**A teammate cloned your repo but the project MCP server isn't working. What might be wrong?**

<details>
<summary>Answer</summary>

Possible issues:
1. MCP was installed in local scope (not project scope) - not in `.mcp.json`
2. Environment variables contain secrets not in version control
3. They haven't installed dependencies (e.g., Node.js for npx-based servers)
4. They need to restart their Claude Code session

Solution: Use project scope and document required setup in README

</details>

---

## Additional Resources

- **Official MCP Registry**: https://api.anthropic.com/mcp-registry/docs
- **GitHub MCP Servers**: https://github.com/modelcontextprotocol/servers
- **Claude Code MCP Docs**: https://code.claude.com/docs/en/mcp.md

---

## Next Lecture

**Lecture 1A: Project Scaffolding**
- Effective prompting strategies
- Directory structure design
- Git initialization
- GitHub repository creation

---

**Course**: Building Production-Grade Applications with Claude Code
**Instructor**: Claude Sonnet 4.5
**Date**: January 2026
