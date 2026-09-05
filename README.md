# Starnext

> [!IMPORTANT]
> **Starting a real project from this starter?**
>
> Replace this README with documentation that describes your product.
>
> This file only explains what Starnext is and how to start using the starter. Once the repository becomes an actual product, this content should no longer describe Starnext.
>
> Do **not** remove or replace `AGENTS.md`, `/docs/standards`, or the documentation system. Those files contain the engineering instructions used by developers and AI coding agents.

A minimal, opinionated Next.js starter designed to provide a consistent foundation for building modern applications without forcing product-specific architecture.

Starnext provides the base environment, engineering standards, documentation structure, and development conventions needed to start a project without rebuilding the same foundation every time.

## Why Starnext?

Starting a new application often involves repeating the same setup:

- configuring Next.js and TypeScript
- configuring styling and UI primitives
- setting up formatting and linting
- defining project conventions
- deciding how components should be organized
- establishing server/client boundaries
- defining data-access rules
- documenting engineering decisions
- configuring AI coding agents

Starnext provides that foundation from the beginning.

The goal is not to provide a finished application architecture.

The goal is to provide a **consistent engineering starting point**.

## What's Included

Starnext includes a foundation built around:

- Next.js
- React
- TypeScript
- Tailwind CSS
- shadcn/ui
- next-intl
- Biome
- Bun

It also includes reusable engineering documentation under:

```text
docs/
├── standards/
└── product/
```

and repository-level instructions for AI coding agents in:

```text
AGENTS.md
```

## Getting Started

Create your project from Starnext and install the dependencies:

```bash
bun install
```

Start the development server:

```bash
bun dev
```

Then begin replacing the starter application with your product.

## Starting Your Product

When turning Starnext into a real application:

1. Replace this README with a README describing your product.
2. Define the product in `/docs/product`.
3. Keep `/docs/standards` as the engineering foundation.
4. Keep `AGENTS.md` as the entry point for AI coding agents.
5. Add product architecture and documentation only as real responsibilities emerge.

Do not create unnecessary documentation or architecture before the product requires it.

## Documentation

Starnext separates engineering standards from product knowledge.

### Engineering Standards

```text
/docs/standards
```

Defines:

> **How we build software.**

These standards are reusable and should remain independent from a specific product.

They cover architecture, components, modules, TypeScript, data access, state, validation, errors, testing, comments, and other engineering concerns.

Start with:

```text
/docs/standards/README.md
```

### Product Documentation

```text
/docs/product
```

Defines:

> **What this product does and how it behaves.**

This documentation evolves with the application and may include:

- product concepts
- features
- business rules
- workflows
- permissions
- limits
- billing behavior
- domain terminology
- product-specific technical decisions

Unlike the engineering standards, product documentation is not based on a mandatory file template.

Create documentation as real product responsibilities emerge.

## AI Coding Agents

`AGENTS.md` is the entry point for AI coding agents working in the repository.

Agents are instructed to:

1. understand the requested product behavior
2. read the relevant product documentation
3. read the applicable engineering standards
4. inspect the existing implementation
5. consult relevant installed skills
6. implement the simplest solution that respects those constraints

Do not replace `AGENTS.md` when creating a product from Starnext.

## Engineering Philosophy

Starnext follows one central principle:

> **Separate responsibilities, not code for the sake of separation.**

The starter does not require every application to have:

- repositories
- services
- adapters
- factories
- global stores
- complex module hierarchies

Those structures should exist only when they protect a meaningful responsibility.

Start simple.

Create boundaries where they provide real value.

Let the architecture evolve with the product.

## What Starnext Does Not Decide

Starnext intentionally does not define every technology your product must use.

Product-specific decisions may include:

- database
- ORM
- authentication
- payment provider
- storage provider
- analytics
- external APIs
- deployment architecture

Those choices belong to the product.

They should not become reusable engineering standards unless they represent a deliberate change to the general Starnext approach.

## License

Use the license defined by this repository.