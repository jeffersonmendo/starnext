# Development Conventions

Follow these conventions for every product cloned from Starnext. Prefer the simplest implementation that satisfies the current requirement.

## Naming and files

| Item | Convention |
| --- | --- |
| Files and directories | `kebab-case` (`invoice-list.tsx`) |
| React components and types | `PascalCase` (`InvoiceList`, `Invoice`) |
| Functions, internal handlers, and Server Actions | `camelCase` (`createInvoice`, `handleSubmit`) |
| Variables and internal object keys | `snake_case` (`invoice_total`) |
| Application-owned JSON keys | `snake_case` |
| Condition booleans | Condition-prefixed `snake_case` (`is_loading`, `has_access`) |
| Conceptual constants | `UPPER_SNAKE_CASE` (`MAX_UPLOAD_SIZE`) |
| Hooks | Standard React `use...` names in kebab-case files (`use-invoice-filter.ts`) |
| Callback props | `onXxx` (`onSubmit`, `onSelect`) |

Use framework-required filenames exactly as required (`page.tsx`, `layout.tsx`, `error.tsx`, and so on). Do not rename external API payload fields merely to satisfy local style; map them at the boundary.

Existing starter code may predate these naming conventions. New and touched application-owned code follows `snake_case` for variables and internal object keys; a naming-only migration is not required unless the task calls for it.

Name internal event handlers for the work they handle (`handleSubmit`) and callback props for the event they expose (`onSubmit`). Prefer type aliases; use interfaces only when declaration merging or extension semantics materially help. Prefer named exports; use default exports only where a framework requires them. Do not add an `Async` suffix solely because a function returns a Promise.

## Imports, modules, and dependencies

- Use the `@/` alias for `src` imports. Order and remove imports with Biome.
- Prefer direct module imports. Do not create barrel files by default: they hide ownership and can widen client bundles. A local, intentional barrel is allowed only when it improves a stable public feature API without creating cycles.
- Cross-feature consumers normally import directly from a focused feature module via the `@/` alias. Create a feature entry `index.ts` only as an intentional, documented public API when it prevents deep imports without circular dependencies; no feature public surface is mandatory. Keep dependency direction from `app` to features to shared infrastructure.
- Reuse before creating: inspect existing primitives, features, helpers, and package capabilities first.
- Add a dependency only when the platform or existing stack cannot solve the requirement clearly. Record a durable stack choice in `stack.md`.

## Components and state

Use server components by default. Add `"use client"` at the smallest interactive boundary and pass only serializable, necessary data across it. Keep components presentational and mockable through explicit props and callbacks.

State ownership is deliberate:

| State | Owner |
| --- | --- |
| Ephemeral component interaction | React local state (`useState`, reducer when justified) |
| Shareable, navigable filters or view state | `nuqs` URL state |
| Cross-feature client state with a real global owner | Zustand |

Do not promote local state to Zustand, or URL state to a global store, for convenience. Derive values during render instead of storing duplicate state.

## Data, validation, and errors

- Put UI orchestration in components/hooks, business rules in services, persistence in repositories, and mutation entry points in actions.
- When Zod is directly installed and adopted, validate untrusted boundaries with its schemas: form input, URLs, server actions, route handlers, webhooks, and external responses. Parse before a service performs work; server actions must authenticate and authorize themselves when the feature has access control.
- Return or render user-safe, actionable errors. Preserve technical causes for observability without leaking secrets or implementation details.
- Use Next route error boundaries for unexpected rendering failures and predictable validation states for expected user mistakes. Handle loading, empty, error, and success states intentionally.

## Comments, mocks, and maintenance

- Write comments only for non-obvious intent, constraints, or tradeoffs. Do not narrate self-evident code.
- Remove dead code, obsolete comments, unused exports, and abandoned TODOs in the same change. Do not keep commented-out code.
- Keep mocks deterministic, feature-owned, and clearly separate from production adapters. Mocks must model useful scenarios rather than silently becoming a second data source.
- Refactor when it makes a current change simpler, safer, or clearer. Do not perform unrelated rewrites or introduce abstractions for hypothetical reuse.

## Environment and secrets

- Validate required environment values where server configuration enters the application; treat runtime configuration as untrusted input and fail clearly when required configuration is missing.
- Never commit private secrets or expose them to the client. Keep server-only values and provider SDKs on the server; client-visible values require intentional exposure.
- When a product introduces environment variables, maintain `.env.example` with variable names and safe placeholders only. Reuse Zod for configuration validation when it is directly installed and adopted; do not build environment infrastructure before the product needs it.

## Testing and Definition of Done

Testing follows TDD where practical: write a focused failing test for a rule or regression, implement the smallest change, then refactor with checks green. Every bug fix adds a regression test when a testable boundary exists. Prefer fast unit tests for rules and schemas, component tests for behavior, and integration or end-to-end tests for critical user paths; do not test implementation details.

Before completion:

- [ ] Scope is minimal; existing code and primitives were reused where appropriate.
- [ ] Naming, boundaries, validation, state ownership, accessibility, i18n, and error states are correct.
- [ ] Relevant tests were added or updated; a regression is covered where feasible.
- [ ] `bun run lint` passes, and `bun run build` passes for integration-level changes.
- [ ] No dead code, unrelated changes, or unverified assumptions remain.
