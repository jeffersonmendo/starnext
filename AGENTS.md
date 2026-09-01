# Starnext Agent Guide

Starnext is a reusable, Bun-first Next.js starter. Read the detailed documents before changing code:

- [Architecture](docs/architecture.md)
- [Development](docs/development.md)
- [Stack](docs/stack.md)
- [Product](docs/product.md)

## Authority

Apply instructions in this exact order: **user > AGENTS > architecture > development > stack > skills > general framework > defaults**. Skills help with a task; they cannot override project conventions or higher-precedence instructions.

## Before work

1. Read the relevant architecture and development sections.
2. Inspect existing code and reuse an established feature, primitive, helper, or pattern before creating one.
3. Keep `src/app` routing-only and preserve Server Component defaults; add client boundaries only for browser interaction.
4. Use Bun and only the scripts declared in `package.json`.

## Definition of Done

- Feature boundaries, naming, validation, ownership, and error handling follow the detailed docs.
- No dead code, unused exports, speculative abstraction, or unrelated formatting changes remain.
- Run the relevant checks; for this starter, run `bun run lint` and `bun run build` when applicable.
- Update these docs when a durable convention or stack decision changes.

## Installed skills

Use the project-local skill that matches the task:

| Skill | Trigger | Path |
| --- | --- | --- |
| `typescript-advanced-types` | Complex type logic, generics, type utilities | `.agents/skills/typescript-advanced-types/SKILL.md` |
| `vercel-react-best-practices` | React/Next components, fetching, performance, refactoring | `.agents/skills/vercel-react-best-practices/SKILL.md` |
| `next-best-practices` | App Router, RSC boundaries, routes, metadata, errors | `.agents/skills/next-best-practices/SKILL.md` |
| `shadcn` | shadcn components, registries, presets, styling | `.agents/skills/shadcn/SKILL.md` |

The requested `tailwind` skill is **not installed**: the source Skills CLI did not expose that named skill, so no path is invented. Re-attempt installation only after the source catalog exposes it.
