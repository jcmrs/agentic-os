# GitHub Copilot Instructions for Agentic-OS

## Technology Stack

This project is built with:

- **Runtime**: Deno 1.40+
- **Language**: TypeScript (native, no build step required)
- **Testing**: Deno.test (built-in)
- **Dependencies**: Deno standard library only (zero npm dependencies)

## Development Commands

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

## Project Architecture

This is a **local-first TypeScript library** (NOT a REST API server):

- 100% local, serverless SDK
- Designed for direct consumption by AI assistants
- No HTTP endpoints or server components
- Provides programmatic API through TypeScript function exports

### Directory Structure

```
agentic-os/
├── .github/                 # GitHub configuration (workflows, templates, etc.)
├── README.md                # Main documentation
└── LICENSE                  # License file

# Future structure (as described in README.md):
├── mod.ts                   # Main library entry point
├── src/
│   ├── core/                # Core logic (template engine, etc.)
│   ├── types/               # TypeScript type definitions
│   └── utils/               # Utility functions (file ops, yaml)
└── tests/                   # Test suite
```

## Code Standards & Best Practices

### Testing Requirements

- **Test-Driven Development**: Aim for >80% test coverage (target from
  README.md)
- Use Deno.test for all tests
- Tests require explicit permissions: `--allow-read --allow-write`
- All tests must pass before committing changes
- Create test infrastructure as project develops

### Permissions Model

- Deno requires explicit permissions for security
- Common permissions needed:
  - `--allow-read`: For reading configuration files and profiles
  - `--allow-write`: For creating project structures and files
  - `--allow-env`: For environment variable access (optional)

### Code Style

- Use TypeScript's strict mode
- Follow Deno's standard formatting (enforced by `deno fmt`)
- No comments unless matching existing style or explaining complex logic
- Use existing libraries from Deno standard library when possible

### Dependencies

- **ZERO npm dependencies** - This is a core principle
- Only use Deno standard library
- Do not add external dependencies unless absolutely critical
- This decision eliminates npm security vulnerabilities and dependency hell

## Development Methodology

This project follows **Specification-Driven Development (SDD)**:

1. All changes should start with a specification in `specs/` (when the directory
   exists)
2. Generate implementation plan in `plan.md`
3. Create task breakdown in `tasks.md`
4. Implement following tasks sequentially
5. Maintain complete traceability

Refer to project documentation for governance principles as they are
established.

## Key Constraints

1. **No npm**: Never suggest npm packages or Node.js dependencies
2. **Deno only**: All code must run on Deno
3. **No build step**: Native TypeScript support means no build configuration
4. **Explicit permissions**: Always specify required Deno permissions
5. **Local-first**: No server-side components or HTTP endpoints
6. **Test coverage**: Maintain >80% coverage requirement

## Common Tasks

### Adding a new feature

1. Create specification in `specs/` directory (create if it doesn't exist)
2. Update `plan.md` and `tasks.md`
3. Write tests first (TDD approach)
4. Implement feature
5. Run tests: `deno test --allow-read --allow-write`
6. Check types: `deno check mod.ts` (once mod.ts exists)
7. Lint: `deno lint`
8. Format: `deno fmt`

### Fixing a bug

1. Write a failing test that reproduces the bug
2. Fix the bug
3. Verify test passes
4. Run full test suite
5. Update documentation if needed

## Important Files

- `README.md`: Main documentation describing the project vision and architecture
- `.github/`: GitHub configuration including workflows and templates

**Note**: This project is in early stages. Files referenced in README.md like
`mod.ts`, `src/`, `tests/`, and specification directories will be created as
development progresses.

## Migration Context

This project migrated from Node.js/npm to Deno on 2025-10-15 to:

- Eliminate npm security vulnerabilities
- Remove dependency management complexity
- Simplify development with built-in tools
- Provide secure-by-default permissions model

When suggesting changes, remember this is a Deno project, not Node.js.
