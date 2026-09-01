# Stack Standards

This document distinguishes a **direct application dependency currently installed** from a **standard technology when the concern exists**. A standard is the approved default when needed; it is not permission to install every package before a feature requires it.

## Current starter setup

| Area | Current fact |
| --- | --- |
| Package manager | Bun; `bun.lock` is committed. |
| Framework | Next.js with the App Router and React Compiler enabled. |
| UI | React, Tailwind CSS, and shadcn `base-vega` with Base UI and Tabler icons. |
| Styling | `src/app/globals.css` imports Tailwind, `tw-animate-css`, and shadcn CSS; semantic CSS variables are enabled. |
| Internationalization | `next-intl` with `en` and `es` locale-prefixed routes, configured in `src/i18n` and `src/proxy.ts`. |
| Theme and fonts | `next-themes`; Geist via the local `geist` package. |
| Quality | Biome formats and lints, with Next and React recommended domains. |
| TypeScript | Strict, no-emit TypeScript with the `@/* → src/*` alias. |

Use Bun. The only current scripts are `dev`, `build`, `start`, `lint`, and `format`; see the [README](../README.md) for their exact commands. See [`package.json`](../package.json) for installed package versions.

## Fixed standard stack

| Technology | Responsibility | Use it for | Do not use it for | Alternatives |
| --- | --- | --- | --- | --- |
| Next.js | App Router, server rendering, routes, server boundaries | Product routes, layouts, route handlers, server actions | A client-only shell by default | A product-level framework change requires an explicit decision |
| React | Component model and local UI state | Presentational and interactive UI | Global persistence or URL synchronization | Native DOM only for isolated non-React embeds |
| TypeScript | Static contracts | Public props, domain data, adapter boundaries | Runtime validation | JavaScript is not the standard |
| Tailwind CSS | Token-based styling | Layout and semantic design tokens | Domain logic or one-off raw color systems | CSS modules only when a product case clearly needs them |
| shadcn/ui | Source-owned, accessible UI primitives | Reusable controls and composed interface patterns | Feature/domain components in `components/ui` | Build a primitive only after verifying shadcn does not fit |
| Zod | Runtime schemas when installed | Forms, actions, URLs, webhooks, external data | Replacing domain behavior or client-only trust | Valibot only by explicit product decision |
| Zustand | Minimal global client state when added | Genuine cross-feature client state | React local state, server data, or nuqs URL state | React context for small, static dependency injection |
| nuqs | Typed URL state when added | Filters, sorting, pagination, shareable views | Hidden or ephemeral component state | Next search params for simple server-only reads |
| Stripe | Default payments boundary when payments are required | Product billing and payment workflows | General persistence or entitlement logic spread through UI | Another provider only by an explicit product decision |
| Resend | Default transactional email boundary when email is required | Product emails through an adapter | UI notifications or business rules | Another provider only by an explicit product decision |

Zod is **not a direct application dependency** in `package.json`; it may be present transitively for tooling. Zustand, nuqs, Stripe, and Resend are **not direct dependencies** and are absent from `bun.lock`. Add each only when the product needs it: use Zod for runtime validation once installed, React local state for component state, nuqs for URL state, Zustand for genuine global client state, Stripe for payments, and Resend for transactional email. Isolate provider SDKs behind a feature service or repository.

## Project-specific decisions

The following values must be chosen by each cloned product and recorded precisely before implementation. Replace `[DEFINE]` with the selected technology and its owner; do not silently inherit an assumption.

| Decision | Placeholder | Questions to answer |
| --- | --- | --- |
| Authentication | `[DEFINE]` | Identity provider, session model, roles, authorization boundary |
| Database and ORM | `[DEFINE]` | Data store, migration ownership, repository adapter |
| Hosting and runtime | `[DEFINE]` | Region, environment variables, observability, deployment owner |
| File storage | `[DEFINE]` | Provider, access policy, lifecycle, upload boundary |
| Payments | `[DEFINE]` | Whether payments are required; choose Stripe when they are |
| Transactional email | `[DEFINE]` | Whether email is required; choose Resend when it is |
| Analytics and error reporting | `[DEFINE]` | Events, privacy, sampling, owner, retention |
| Test tooling | `[DEFINE]` | Unit/component/integration runner and CI execution |

## UI workflow

The shadcn configuration is `components.json`: RSC enabled, `src/app/globals.css`, `@/components/ui`, Base UI, Tabler icons, and CSS variables. Check for an existing primitive, then use Bun to add only what is needed:

```bash
bunx --bun shadcn@latest add <component>
```

Use semantic tokens such as `bg-background` and `text-muted-foreground`; preserve the current Base UI configuration when adding components. For a cloned product's preset, use shadcn Create and apply the supplied code with `bunx --bun shadcn@latest apply <preset-code>`.
