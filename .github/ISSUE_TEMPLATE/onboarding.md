---
name: Onboarding Guide
about: Instructions for new contributors and Copilot agents
title: 'Onboarding: Welcome to Agentic-OS'
labels: [documentation, onboarding]
assignees: ''

---

Welcome to the Agentic-OS project! This guide provides onboarding instructions for new contributors and Copilot agents to ensure a smooth setup and compliance with project standards.

## Repository Standards and Best Practices

- Review the `.github/copilot-agent.yml` file for agent instructions and repository rules.
- Review the `.github/copilot-instructions.md` file for detailed development guidelines.
- This project uses [Specification-Driven Development (SDD)] as outlined in the README. Start all changes with a specification in the `specs/` directory.
- Maintain >80% test coverage using `deno test`.

## Development Environment Setup

### Prerequisites

**Runtime:** Deno 1.40+  
**Language:** TypeScript (native)  
**Testing:** Deno.test (built-in)  
**Dependencies:** Deno standard library only (no npm)

### Install Deno

```bash
# macOS/Linux
curl -fsSL https://deno.land/x/install/install.sh | sh

# Windows (PowerShell)
irm https://deno.land/install.ps1 | iex
```

Verify installation:
```bash
deno --version
```

## Common Commands

```bash
# Run all tests
deno test --allow-read --allow-write

# Run specific test file
deno test tests/core/template_expander.test.ts --allow-read --allow-write

# Type checking
deno check mod.ts
deno check src/**/*.ts

# Linting
deno lint

# Formatting
deno fmt

# Check formatting without modifying
deno fmt --check
```

## Permissions Model

Deno requires explicit permissions for security:
- `--allow-read`: For reading configuration files and profiles
- `--allow-write`: For creating project structures and files
- `--allow-env`: For environment variable access (optional)

Example:
```bash
deno run --allow-read --allow-write your_script.ts
```

## Development Workflow

### Adding a New Feature

1. Create specification in `specs/` directory (create if it doesn't exist)
2. Update `plan.md` and `tasks.md`
3. Write tests first (TDD approach)
4. Implement feature
5. Run tests: `deno test --allow-read --allow-write`
6. Check types: `deno check mod.ts`
7. Lint: `deno lint`
8. Format: `deno fmt`

### Before Submitting a PR

Run all checks locally:
```bash
# Format code
deno fmt

# Lint code
deno lint

# Type check (once mod.ts exists)
deno check mod.ts

# Run tests
deno test --allow-read --allow-write
```

## Automated Checks

Repository standards are enforced through:
- Custom instructions in `.github/copilot-agent.yml` and `.github/copilot-instructions.md`
- GitHub Actions workflows run on each pull request:
  - Code formatting check (`deno fmt --check`)
  - Linting (`deno lint`)
  - Type checking (`deno check`)
  - Test suite (`deno test`)

All checks must pass before PRs can be merged.

## Key Constraints

1. **No npm**: Never use npm packages or Node.js dependencies
2. **Deno only**: All code must run on Deno
3. **No build step**: Native TypeScript support means no build configuration
4. **Explicit permissions**: Always specify required Deno permissions
5. **Local-first**: No server-side components or HTTP endpoints
6. **Test coverage**: Maintain >80% coverage requirement

## Architecture

This is a **local-first TypeScript library** (NOT a REST API server):
- 100% local, serverless SDK
- Designed for direct consumption by AI assistants
- No HTTP endpoints or server components
- Provides programmatic API through TypeScript function exports

## Getting Help

- Refer to the [README](../README.md) for architecture and governance details
- Review [copilot-instructions.md](.github/copilot-instructions.md) for development guidelines
- Review [copilot-agent.yml](../copilot-agent.yml) for agent rules
- For questions, comment on this issue or open a new discussion

## Migration Context

This project migrated from Node.js/npm to Deno on 2025-10-15 to:
- Eliminate npm security vulnerabilities
- Remove dependency management complexity
- Simplify development with built-in tools
- Provide secure-by-default permissions model

Thank you for joining Agentic-OS! Following these steps will help ensure your contributions meet project guidelines and pass automated checks.
