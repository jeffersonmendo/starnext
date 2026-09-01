# Starnext Agent Guide

Starnext is a reusable, Bun-first Next.js starter. Read the detailed documents before changing code:

- [Architecture](docs/architecture.md)
- [Development](docs/development.md)
- [Stack](docs/stack.md)
- [Product](docs/product.md)

## Authority

Apply instructions in this exact order: **user instructions > AGENTS.md > docs/architecture.md > docs/development.md > docs/stack.md > installed skills > framework/library conventions > agent defaults**. Skills assist with a task but never override naming, architecture, feature boundaries, folders, stack decisions, helpers, or local conventions. Adapt skill examples to these rules (for example, `currentUser` becomes `current_user`).

## Operational summaries

Detailed rules live in the linked documents; these summaries are mandatory.

### Naming and modules

- Use `kebab-case` files and directories; components and types are `PascalCase`.
- Functions, handlers (`handleSubmit`), and Server Actions are `camelCase`. Do not add an `Async` suffix solely because a function returns a Promise.
- Variables, internal application object keys, and application-owned JSON use `snake_case`; condition booleans are condition-prefixed `snake_case` (`is_loading`, `has_access`). Conceptual constants use `UPPER_SNAKE_CASE`, not every `const`.
- Hooks use `useXxx` in kebab-case filenames; callback props use `onXxx`.
- Prefer named exports. Use default exports only where a framework requires them. Prefer type aliases; use interfaces only when extension semantics help.
- Preserve external API casing at the integration boundary and map it to internal conventions.

### Reuse, helpers, and state

- Search and reuse existing features, primitives, helpers, and package capabilities before creating anything. For UI, reuse existing shadcn/Base UI primitives, compose them, then add a needed primitive before custom markup.
- Keep helpers pure and feature-local by default. Promote them to `shared` or `lib` only after real cross-feature reuse; extract only when it removes repeated, stable responsibility. Never create a catch-all helpers directory.
- Use React local state for component interaction; when directly installed, use nuqs for URL state and Zustand only for genuine global client state. Do not put derived or URL state in stores.

### Stack and environment

- Follow the standard stack in [Stack](docs/stack.md): Zod runtime validation when directly installed and adopted, Stripe when payments are needed, and Resend when email is needed. Add standards only when the product requires them.
- Validate required environment values at the server boundary. Treat runtime configuration as untrusted; never commit or expose private secrets. Keep server-only values and provider SDKs on the server, expose client values intentionally, and fail clearly for missing required configuration. When a product introduces environment variables, maintain `.env.example` with variable names and safe placeholders only; do not build environment infrastructure before the product needs it.

### Pre-task checklist

1. Read the relevant architecture and development sections.
2. Check existing code for a reusable feature, primitive, helper, or pattern.
3. Preserve `src/app` as routing-only, Server Component defaults, and the smallest client boundary.
4. Use Bun and only scripts declared in `package.json`.

## Definition of Done

- Feature boundaries, naming, validation, state ownership, environment safety, accessibility, i18n, and error handling follow the detailed docs.
- Reuse was considered; no dead code, unused exports, speculative abstraction, catch-all helper, or unrelated formatting changes remain.
- Relevant tests are added or updated. Run the applicable checks; for this starter, run `bun run lint` and `bun run build` when applicable.
- Update these docs when a durable convention or stack decision changes.

## Installed skills

`.agents/skills/` is the canonical project-local skill directory. Use the matching installed skill:

| Skill | Trigger | Path |
| --- | --- | --- |
| `typescript-advanced-types` | Complex type logic, generics, type utilities | `.agents/skills/typescript-advanced-types/SKILL.md` |
| `vercel-react-best-practices` | React/Next components, fetching, performance, refactoring | `.agents/skills/vercel-react-best-practices/SKILL.md` |
| `next-best-practices` | App Router, RSC boundaries, routes, metadata, errors | `.agents/skills/next-best-practices/SKILL.md` |
| `shadcn` | shadcn components, registries, presets, styling | `.agents/skills/shadcn/SKILL.md` |

The requested [`tailwind` skill](https://www.skills.sh/heygen-com/hyperframes/tailwind) is intentionally not installed because it covers Tailwind v4 browser-runtime patterns for deterministic HyperFrames video compositions, not general Tailwind development for this Next.js starter. Tailwind remains governed by the project's Tailwind v4 tooling, documentation, and applicable installed skills.
