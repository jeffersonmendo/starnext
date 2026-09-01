# Architecture

Use a feature-based architecture. Routes compose features; features own product behavior; shared code is genuinely cross-feature. Create directories only when code requires them.

## Target structure

```txt
src/
  app/             # App Router routes, layouts, route-level loading/errors
  features/        # Product capabilities, grouped by feature
  components/ui/   # Generic shadcn/Base UI primitives only
  shared/          # Cross-feature components, types, and utilities
  lib/             # Framework/infrastructure adapters and small utilities
  config/          # Application configuration
```

This is a target, not a request to create empty folders. The current starter has `app`, `components/ui`, `i18n`, `lib`, and `proxy.ts`; introduce `features`, `shared`, or `config` only with their first owner.

## Feature boundary

A feature may contain only the layers it needs:

```txt
src/features/<feature>/
  components/      # Feature UI and presentational components
  actions/         # Server actions or client action orchestration
  services/        # Use cases and application rules
  repositories/    # Data-source contracts/adapters
  schemas/         # Zod input and boundary schemas
  types/           # Feature-owned domain/view types
  mocks/           # Deterministic feature fixtures/fakes
  hooks/            # Feature hooks
```

Do not add every layer by template. A simple display feature can have only a component and types; add a service or repository when rules or a data source justify the separation.

## Feature public APIs

Cross-feature consumers normally import directly from a focused feature module via the `@/` alias. A feature entry `index.ts` is optional and may be created only as an intentional, documented public API when it prevents deep imports without circular dependencies.

## Component boundaries

- `src/components/ui` contains generic, domain-free primitives. It must not import features or product terminology.
- Feature components live with the feature. Promote a component to `shared` only after real reuse by multiple features.
- Prefer presentational components with explicit props and callbacks. Keep data access, effects, state orchestration, and side effects in a route, container, hook, action, or service.
- Design presentational components so fixtures and mock callbacks can render them without a server, store, or external service.
- Reuse an existing primitive or component before creating new markup. Compose shadcn/Base UI primitives and use semantic Tailwind tokens.

## Directional dependencies and data flow

Dependencies point inward: `app → features → shared/lib/config → external systems`. A generic primitive never imports a feature, and one feature does not reach into another feature's internals; extract shared code only when ownership is truly shared.

Data flows down through typed props. Events and actions flow up through callbacks or explicit action boundaries. Server components fetch/compose and pass the minimum serializable view data to client components. Keep browser-only behavior behind the smallest possible `"use client"` boundary.

## External boundaries

Repositories isolate database or remote persistence details. Services coordinate business rules. Actions and route handlers validate input, authenticate and authorize where applicable, call a service, and return a deliberate result. Provider SDKs (payments, email, storage, analytics) stay behind adapters in `lib` or a feature repository/service; do not spread SDK calls through components.

Schemas validate all untrusted boundaries: form input, URL data, server actions, route handlers, webhooks, and external responses. Infer application types from schemas where that removes duplication; do not trust client validation alone.

## App Router and i18n

`src/app` owns route composition and Next special files, not feature implementation. The current routes are locale-prefixed under `src/app/[locale]`; `src/i18n` owns routing, request configuration, and localized navigation, while `src/proxy.ts` applies `next-intl` middleware. Preserve this split when adding routes.

App Router components are server components by default. Use a client component only for state, event handlers, effects, or browser APIs. Route-level failures use the appropriate `error.tsx`, `not-found.tsx`, and loading boundaries when the route needs them.
