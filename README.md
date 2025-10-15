# Agentic-OS Local Library (Deno SDK)

A modern, secure, local-first TypeScript library for orchestrating agentic development workflows. Built with Deno to eliminate npm complexity and security vulnerabilities.

## Architecture

This library is a 100% local, serverless TypeScript SDK designed to be used directly by AI assistants or other developer tools. It contains all the logic for managing profiles, compiling agent prompts, and executing the Specification-Driven Development methodology.

**Key Features:**

- 🔒 **Zero npm dependencies** - No security vulnerabilities, no dependency hell
- ⚡ **Native TypeScript** - Built-in TypeScript support, no build step
- 🧪 **Built-in testing** - Deno.test included
- 🛡️ **Secure by default** - Explicit permissions model
- 📦 **Single executable** - One tool for development, testing, and linting

## Technology Stack

**Runtime:** Deno 1.40+
**Language:** TypeScript
**Testing:** Deno.test (built-in)
**Dependencies:** Deno standard library only

**Migration Note:** This project migrated from Node.js/npm to Deno on 2025-10-15 to eliminate npm security issues and dependency management complexity.

## Installation

### Prerequisites

Install Deno: https://deno.land/

```bash
# macOS/Linux
curl -fsSL https://deno.land/x/install/install.sh | sh

# Windows (PowerShell)
irm https://deno.land/install.ps1 | iex
```

### Using the Library

```typescript
// Import from URL (when published)
import * as AgenticOS from "https://deno.land/x/agentic_os/mod.ts";

// Or import from local path during development
import * as AgenticOS from "./mod.ts";
```

## Core Concepts

- **Profiles**: Self-contained sets of commands, standards, and workflows
- **Commands**: Structured prompts that guide an AI through a task
- **Standards**: Best practice documents injected into prompts
- **Template Expansion**: Recursive compilation of commands, workflows, and standards into final prompts for AI consumption

## Public API

> **Status:** Under active development following Spec Kit methodology

### Initialization

```typescript
import { initializeProject } from "./mod.ts";

// Initialize a new project
await initializeProject({
  projectPath: "./my-new-project",
  profile: "default",
});
```

### Content Management

```typescript
import { getCommand, getProfile, listCommands, listProfiles } from "./mod.ts";

// List available profiles
const profiles = await listProfiles("./my-project");

// Get specific profile
const profile = await getProfile("default", "./my-project");

// List commands in a profile
const commands = await listCommands("default");

// Get specific command
const command = await getCommand("create-spec", "single-agent", "default");
```

### Compilation

```typescript
import { compileCommand } from "./mod.ts";

// Compile a command with template expansion
const prompt = await compileCommand(
  "./.agent-os/profiles/default/commands/create-spec/single-agent/1-create-spec.md",
);
```

## Development

### Running Tests

```bash
# Run all tests
deno test

# Run specific test file
deno test tests/core/template_expander.test.ts

# Run tests with permissions
deno test --allow-read --allow-write
```

### Type Checking

```bash
# Check types for main entry point
deno check mod.ts

# Check all TypeScript files
deno check src/**/*.ts
```

### Linting

```bash
# Lint all files
deno lint

# Lint specific directory
deno lint src/
```

### Formatting

```bash
# Format all files
deno fmt

# Check formatting without modifying
deno fmt --check
```

## Project Structure

```
agentic-os/
├── mod.ts                   # Main library entry point
├── src/
│   ├── core/                # Core logic (template engine, etc.)
│   │   └── template_expander.ts
│   ├── types/               # TypeScript type definitions
│   │   └── index.ts
│   └── utils/               # Utility functions (file ops, yaml)
│       ├── file_ops.ts
│       └── yaml_parser.ts
├── tests/                   # Test suite
│   ├── core/
│   ├── utils/
│   └── *.test.ts
├── deno.json                # Deno configuration
└── README.md                # This file
```

## Permissions

Deno requires explicit permissions for security. This library needs:

- `--allow-read`: To read configuration files and profiles
- `--allow-write`: To create project structures and write files
- `--allow-env` (optional): For environment variable access

Example usage:

```bash
deno run --allow-read --allow-write your_script.ts
```

## Usage by AI Assistants

This library is designed for direct consumption by AI assistants:

```typescript
// AI assistant imports and uses the library
import { compileCommand, initializeProject } from "./mod.ts";

// Initialize project
await initializeProject({ projectPath: "./project", profile: "default" });

// Compile command for execution
const prompt = await compileCommand("./path/to/command.md");

// AI executes the compiled prompt
```

## Development Status

**Current Phase:** Phase 6 (Polish & Finalization)
**Methodology:** Specification-Driven Development (Spec Kit)

**Completed Phases:**

- ✅ Phase 1: Project Setup (Deno)
- ✅ Phase 2: Foundational Modules
- ✅ Phase 3: User Story 1 - Project Initialization
- ✅ Phase 4: User Story 3 - Agent Prompt Compilation
- ✅ Phase 5: User Story 2 - Content Management
- 🔄 Phase 6: Polish & Finalization (In Progress)

**Test Coverage:** 30 unit tests, all passing

- 13 tests for TemplateExpander (core engine)
- 17 tests for Content Management (CRUD operations)

See `specs/001-feature-refactor-agent/tasks.md` for detailed implementation tasks.

## Architecture Decisions

**Why Deno?**

- Eliminates npm security vulnerabilities (a persistent, critical issue)
- Removes dependency management complexity
- Native TypeScript support (no build configuration)
- Built-in development tools (testing, linting, formatting)
- Secure by default with explicit permissions
- Single executable for all operations

**Why Not Node.js/npm?**

- npm security vulnerabilities are constant and unavoidable
- node_modules bloat and dependency hell
- Complex build tooling (TypeScript, Jest, ESLint, Prettier)
- Fragile dependency trees
- Package manager overhead

This decision follows Spec Kit Use Case #2 (Technology Stack Change) where specifications remain unchanged while implementation details are updated.

## Contributing

This project follows strict Specification-Driven Development (SDD). All changes must:

1. Start with a specification in `specs/`
2. Generate implementation plan in `plan.md`
3. Create task breakdown in `tasks.md`
4. Implement following tasks sequentially
5. Maintain complete traceability

See `memory/constitution.md` for project governance (7 core principles including Test-Driven Development >80% coverage requirement).

## License

[To be determined]

## References

- **Original System:** [agent-os](https://github.com/buildermethods/agent-os)
- **Methodology:** [Spec Kit](https://github.com/github/spec-kit)
- **Documentation:** `CLAUDE.md` and `HANDOVER.md`
- **Specification:** `specs/001-feature-refactor-agent/spec.md`

---

**Note:** This is a local library, NOT an HTTP REST API server. It provides a programmatic API through TypeScript function exports, consumed directly by AI assistants via imports.
