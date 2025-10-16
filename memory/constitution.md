# Agentic OS Constitution

## Core Principles

### I. API-First for an Open Future

Every feature must be exposed through a well-documented RESTful API. The API is the primary contract for all interactions, ensuring **Extensibility** for future features, **Integration** with other systems, and enabling robust **Automation**.

### II. Modular by Default

All components shall be designed as independent, loosely-coupled modules. This ensures the system is adaptable and can be "retooled" as requirements evolve.

### III. Configurable Behavior

System behavior (e.g., profiles, modes) must be controlled by configuration, not hardcoded. This configuration will be accessible via the API to allow for dynamic adjustments.

### IV. Quality via Automated Testing

Development will be strictly Test-Driven (TDD). All new code must be preceded by failing tests to guarantee stability and correctness. A high test coverage (>80%) is required.

### V. Scalable & Stateless Architecture

The architecture must be serverless and stateless to ensure scalability, reduce maintenance, and simplify integrations.

### VI. Predictable Evolution with Clear Versioning

The API will follow Semantic Versioning (MAJOR.MINOR.PATCH). Breaking changes are only permitted in MAJOR version updates.

### VII. Methodological Equivalence

The refactored system must maintain functional and conceptual equivalence with the core `agent-os` methodology. The new API must provide endpoints and logic that directly represent the concepts of **Profiles**, **Roles**, multi-modal **Commands**, **Standards**, and the **template expansion engine**. Furthermore, the system must uphold the **3-Layer Context model** (Tool, Project, and File context) by ensuring the API can provide agents with access to each distinct layer.

## Technology Stack Constraints

**Technology Stack**: Deno (TypeScript runtime)

**Rationale**:

- **Eliminates npm ecosystem**: No package.json, no node_modules, no npm security vulnerabilities, no dependency hell
- **Native TypeScript support**: Built-in TypeScript compilation, no tsconfig.json needed
- **Built-in development tools**: Testing (Deno.test), formatting (deno fmt), linting (deno lint)
- **Secure by default**: Explicit permissions model prevents unauthorized file/network access
- **Modern standard library**: Comprehensive std library for common tasks (YAML, testing, assertions)
- **Single executable**: One tool for all development needs
- **URL-based imports**: Direct imports from URLs or use import maps, no package manager required
- **Zero build step**: Run TypeScript directly without compilation

This decision was made on 2025-10-15 to address persistent npm security issues and dependency management complexity while maintaining type safety, development velocity, and code quality. The change follows Spec Kit's technology stack change workflow (Use Case #2), where the specification remains unchanged and only implementation artifacts are updated.

## Development Workflow

The project will strictly adhere to the 7-phase Specification-Driven Development (SDD) process as defined by the Spec Kit methodology. No implementation work shall begin before a specification (`spec.md`) and an implementation plan (`plan.md`) are completed and validated.

## Governance

This Constitution supersedes all other practices and conventions. Amendments require a formal proposal, review, and approval. All pull requests and development work must verify compliance with these principles.

**Version**: 1.1.0 | **Ratified**: 2025-10-14 | **Last Amended**: 2025-10-15 (Technology Stack: Node.js → Deno)
