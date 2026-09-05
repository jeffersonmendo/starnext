# Starnext — Agent Guide

When working on this project, read the relevant documentation and skills **before writing code**.

Do not invent conventions that are already defined in the repository.

## How to Work

1. Understand the requested change.
2. Read the relevant engineering standard(s).
3. Read the relevant product documentation.
4. Load any applicable skill(s).
5. Inspect the existing implementation.
6. Implement the simplest solution that respects those constraints.
7. Run the relevant checks.

Multiple standards, product documents, and skills may apply simultaneously.

## Engineering Standards

`docs/standards/` defines:

> **How we build software.**

| Standard             | When to read                                                                                             | Path                                                                           |
| -------------------- | -------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| Architecture         | When changing responsibilities, boundaries, dependency direction, or overall structure.                  | [`docs/standards/architecture.md`](./docs/standards/architecture.md)           |
| Project Structure    | When deciding where files, features, hooks, components, or shared code belong.                           | [`docs/standards/project-structure.md`](./docs/standards/project-structure.md) |
| Naming               | When creating or renaming files, variables, functions, components, types, hooks, or callbacks.           | [`docs/standards/naming.md`](./docs/standards/naming.md)                       |
| Components           | When creating or modifying React components or component APIs.                                           | [`docs/standards/components.md`](./docs/standards/components.md)               |
| Server / Client      | When working with Server Components, Client Components, mutations, secrets, or server/client boundaries. | [`docs/standards/server-client.md`](./docs/standards/server-client.md)         |
| Modules              | When creating or changing features, module APIs, ownership, or cross-feature dependencies.               | [`docs/standards/modules.md`](./docs/standards/modules.md)                     |
| Functions            | When designing application operations, helpers, parameters, side effects, or control flow.               | [`docs/standards/functions.md`](./docs/standards/functions.md)                 |
| TypeScript           | When designing types, contracts, generics, assertions, or external/internal representations.             | [`docs/standards/typescript.md`](./docs/standards/typescript.md)               |
| Data Access          | When accessing databases, external services, repositories, or infrastructure.                            | [`docs/standards/data-access.md`](./docs/standards/data-access.md)             |
| State Management     | When introducing local, shared, URL, server, or global client state.                                     | [`docs/standards/state-management.md`](./docs/standards/state-management.md)   |
| Validation           | When handling forms, external input, schemas, environment values, APIs, webhooks, or trust boundaries.   | [`docs/standards/validation.md`](./docs/standards/validation.md)               |
| Errors               | When designing error codes, responses, provider errors, validation errors, or failure behavior.          | [`docs/standards/errors.md`](./docs/standards/errors.md)                       |
| Internationalization | When adding user-facing copy, locale behavior, translations, formatting, or localized errors.            | [`docs/standards/i18n.md`](./docs/standards/i18n.md)                           |
| Imports              | When changing dependencies, aliases, module imports, barrels, or server-only imports.                    | [`docs/standards/imports.md`](./docs/standards/imports.md)                     |
| Testing              | When adding tests, fixing meaningful bugs, or protecting important behavior.                             | [`docs/standards/testing.md`](./docs/standards/testing.md)                     |
| Comments             | When adding comments, TSDoc, TODOs, invariants, warnings, or workarounds.                                | [`docs/standards/comments.md`](./docs/standards/comments.md)                   |
| Code Quality         | When evaluating maintainability, abstractions, duplication, refactoring, or unnecessary complexity.      | [`docs/standards/code-quality.md`](./docs/standards/code-quality.md)           |

Full standards index:

[`docs/standards/README.md`](./docs/standards/README.md)

`AGENTS.md` and `docs/standards/**` are protected engineering instructions.

**Do not modify them unless the developer explicitly requests a change to the engineering system itself.**

## Product Documentation

`docs/product/` defines:

> **What this product does and how it behaves.**

Start with:

[`docs/product/README.md`](./docs/product/README.md)

Read the product documents relevant to the feature being changed.

Product documentation may contain:

- business rules
- features
- permissions
- limits
- workflows
- domain concepts
- billing behavior
- product-specific architecture
- technical decisions

`docs/product/**` belongs to the product and may evolve freely as the application changes.

Do not modify engineering standards to solve a product-specific requirement.

## Skills

`.agents/skills/` contains task- or technology-specific instructions.

When a skill matches the current task, read its `SKILL.md` before implementing.

| Skill        | When to use                                                                                             | Path                                                                         |
| ------------ | ------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| Next.js      | When working with Next.js routing, rendering, data fetching, server/client behavior, or framework APIs. | [`.agents/skills/nextjs/SKILL.md`](./.agents/skills/nextjs/SKILL.md)         |
| React        | When working with React components, hooks, composition, state, or rendering behavior.                   | [`.agents/skills/react/SKILL.md`](./.agents/skills/react/SKILL.md)           |
| TypeScript   | When working with advanced typing, generics, contracts, narrowing, or type-level design.                | [`.agents/skills/typescript/SKILL.md`](./.agents/skills/typescript/SKILL.md) |
| shadcn/ui    | When creating or modifying UI using shadcn/ui components and patterns.                                  | [`.agents/skills/shadcn/SKILL.md`](./.agents/skills/shadcn/SKILL.md)         |
| Tailwind CSS | When working with Tailwind utilities, layout, responsive behavior, or styling conventions.              | [`.agents/skills/tailwind/SKILL.md`](./.agents/skills/tailwind/SKILL.md)     |

Additional skills may be added as the project evolves.

Skills explain **how to perform specific technical work**.

Standards define **how this repository should be engineered**.

Product documentation defines **how this specific application should behave**.

## Source Priority

When instructions conflict, use this order:

1. Explicit developer instruction for the current task
2. Product documentation
3. Engineering standards
4. Existing correct project patterns
5. Relevant skills and framework/library guidance

Do not invent business rules.

Do not introduce a new architectural pattern before checking the existing documentation and implementation.

## Core Principle

> **Separate responsibilities, not code for the sake of separation.**

Prefer clear ownership, explicit boundaries, and the simplest correct implementation.
