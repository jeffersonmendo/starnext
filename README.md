# Starnext

A Bun-first Next.js starter for cloned products. It keeps theme, UI primitives, local fonts, and internationalization ready without prescribing product features.

## Quick start

```bash
bun install
bun run dev
```

Open `http://localhost:3000`.

| Command | Purpose |
| --- | --- |
| `bun run dev` | Start the development server. |
| `bun run build` | Create a production build. |
| `bun run start` | Start the production server. |
| `bun run lint` | Run Biome checks. |
| `bun run format` | Format with Biome. |

## Start a product from this repository

```bash
git clone <your-starnext-repo-url> my-new-app
cd my-new-app
rm -rf .git
git init
bun install
```

Then:

- Rename `package.json` and this README.
- Update `messages/en.json` and `messages/es.json` metadata.
- Confirm locales and the default locale in `src/i18n/routing.ts`.
- Replace the starter home with the product entry point.
- Run `bun run lint` and `bun run build`.

The current locale-prefixed routes are `/en` and `/es`. i18n configuration is in `src/i18n/`; `src/proxy.ts` applies locale routing.

## UI and theme

The project uses Tailwind CSS v4 and shadcn/Base UI. Reuse primitives from `src/components/ui`, use semantic tokens such as `bg-background`, and add a component only when the product needs it:

```bash
bunx --bun shadcn@latest add <component>
```

Use shadcn Create to select a preset, then apply it to the clone. To change only a theme or font, use `--only theme` or `--only font` rather than reinstalling components.

```bash
bunx --bun shadcn@latest apply <preset-code>
```

Geist comes from the local `geist` package and is wired through `src/app/[locale]/layout.tsx` and `src/app/globals.css`; do not replace it with `next/font/google` without a product decision.

## Engineering foundation

- [Product intent](docs/product.md)
- [Architecture](docs/architecture.md)
- [Development conventions](docs/development.md)
- [Stack standards](docs/stack.md)
- [Agent operating guide](AGENTS.md)

Use this navigation when starting a cloned product: define the product, choose its `[DEFINE]` decisions, then implement against the architecture and development conventions. The canonical local agent skills are in `.agents/skills/`:

- `next-best-practices`
- `vercel-react-best-practices`
- `typescript-advanced-types`
- `shadcn`

Auth, a database, and an ORM are intentionally absent. Choose them for the cloned product rather than adding them to this base.
