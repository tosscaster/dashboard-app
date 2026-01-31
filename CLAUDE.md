# CLAUDE.md

This file provides guidance for Claude Code when working with this repository.

## Project Overview

A full-stack React application built on **TanStack Start** - a modern meta-framework for building web applications with server-side rendering, streaming, and type-safe APIs. Features comprehensive demos for TanStack ecosystem tools, oRPC integration, Better Auth, and Drizzle ORM.

## Tech Stack

| Category | Technology | Version |
|----------|------------|---------|
| **Framework** | TanStack Start + TanStack Router | 1.132.0 |
| **Frontend** | React (with React Compiler) | 19.2.0 |
| **State** | TanStack Query, TanStack Store, TanStack React DB | 5.66.5, 0.8.0, 0.1.1 |
| **Forms** | TanStack Form | 1.0.0 |
| **Tables** | TanStack Table | 8.21.2 |
| **Styling** | Tailwind CSS, shadcn/ui (new-york) | 4.0.6 |
| **Backend** | Nitro server runtime | nightly |
| **RPC** | oRPC (type-safe RPC) | 1.13.0 |
| **Database** | PostgreSQL + Drizzle ORM | 0.45.0 |
| **Auth** | Better Auth (email/password, sessions) | 1.4.12 |
| **Validation** | Zod | 4.1.11 |
| **i18n** | Paraglide.js | 2.8.0 |
| **Build** | Vite, TypeScript (strict) | 7.1.7, 5.7.2 |
| **Testing** | Vitest, React Testing Library | 3.0.5, 16.2.0 |

## Commands

```bash
# Development
pnpm dev              # Start dev server (port 3000)
pnpm build            # Build for production
pnpm preview          # Preview production build

# Testing & Quality
pnpm test             # Run tests (Vitest)
pnpm lint             # Run ESLint
pnpm format           # Run Prettier
pnpm check            # Format + lint + fix all

# Database (Drizzle)
pnpm db:generate      # Generate migrations from schema changes
pnpm db:migrate       # Run pending migrations
pnpm db:push          # Push schema directly to database (dev)
pnpm db:pull          # Pull schema from database
pnpm db:studio        # Open Drizzle Studio GUI
```

## Project Structure

```
src/
├── components/           # React components
│   ├── Header.tsx        # Main navigation with demo links
│   ├── LocaleSwitcher.tsx # i18n locale picker
│   ├── demo.*.tsx        # Demo-specific components
│   └── ui/               # shadcn/ui components
├── routes/               # File-based routing (TanStack Router)
│   ├── __root.tsx        # Root layout with providers
│   ├── index.tsx         # Homepage
│   ├── demo/             # Demo feature routes (18+ demos)
│   │   ├── drizzle.tsx   # Database CRUD demo
│   │   ├── better-auth.tsx # Auth demo
│   │   ├── orpc-todo.tsx # oRPC demo
│   │   ├── form.*.tsx    # TanStack Form demos
│   │   ├── table.tsx     # TanStack Table demo
│   │   ├── store.tsx     # TanStack Store demo
│   │   └── start.*.tsx   # SSR/streaming demos
│   └── api/
│       └── auth/$.js     # Better Auth handler
├── db/
│   ├── index.ts          # Drizzle client setup
│   └── schema.ts         # Database table definitions
├── db-collections/
│   └── index.js          # TanStack React DB collections
├── orpc/
│   ├── client.js         # oRPC client + TanStack Query utils
│   ├── schema.js         # Zod schemas for RPC
│   └── router/
│       ├── index.js      # Router export
│       └── todos.js      # Todo endpoints
├── integrations/
│   ├── tanstack-query/   # QueryClient provider + devtools
│   └── better-auth/      # Auth header component
├── hooks/                # Custom React hooks
│   ├── demo.form.js      # Form hook factory
│   └── demo.useChat.js   # Chat with streaming
├── lib/
│   ├── auth.js           # Better Auth server config
│   ├── auth-client.js    # Better Auth client
│   ├── demo-store.js     # TanStack Store example
│   └── utils.js          # cn() utility (clsx + tailwind-merge)
├── data/                 # Demo data (Faker generated)
├── paraglide/            # Generated i18n files
├── styles.css            # Global Tailwind styles
└── router.tsx            # Router configuration

Root configs:
├── vite.config.ts        # Vite + TanStack + Tailwind
├── drizzle.config.ts     # Drizzle ORM config
├── tsconfig.json         # TypeScript (strict mode)
├── eslint.config.js      # ESLint (TanStack config)
├── prettier.config.js    # Prettier rules
├── components.json       # shadcn/ui config
└── project.inlang/       # Paraglide i18n config
```

## Code Conventions

### Imports
- Use path alias `@/*` for all src imports: `import { Button } from '@/components/ui/button'`

### Formatting (Prettier)
- No semicolons
- Single quotes
- Trailing commas everywhere

### Components
- Use shadcn/ui components from `@/components/ui/`
- Style with Tailwind utility classes
- Use `cn()` from `@/lib/utils` for conditional classes
- Icons from `lucide-react`

### API Development
- Define oRPC handlers in `src/orpc/router/`
- Use Zod schemas for input validation (defined in `src/orpc/schema.js`)
- oRPC endpoints available at `/api/rpc`
- Server functions use `createServerFn` from TanStack Start

### State Management
- **Server state**: TanStack Query (use `orpc` utils for oRPC integration)
- **Client state**: TanStack Store for simple state
- **Local collections**: TanStack React DB with Zod validation

### Database
- Define tables in `src/db/schema.ts` using Drizzle's `pgTable`
- Import `db` from `@/db` for queries
- Run `pnpm db:generate` after schema changes, then `pnpm db:migrate`

## Environment Variables

Required in `.env.local`:

```bash
# PostgreSQL connection (required)
DATABASE_URL="postgresql://username:password@localhost:5432/mydb"

# Better Auth (required)
BETTER_AUTH_URL=http://localhost:3000
BETTER_AUTH_SECRET=  # Generate: npx @better-auth/cli secret
```

## Testing

- **Framework**: Vitest with React Testing Library
- **Run**: `pnpm test`
- **Location**: Place tests next to source files (`*.test.ts(x)`) or in `__tests__/` directories
- **Environment**: JSDOM for DOM simulation

## Key Files

| File | Purpose |
|------|---------|
| `vite.config.ts` | Build config with TanStack, Tailwind, Paraglide plugins |
| `drizzle.config.ts` | Database ORM configuration |
| `src/db/schema.ts` | Database table definitions |
| `src/lib/auth.js` | Better Auth server configuration |
| `src/lib/auth-client.js` | Better Auth client setup |
| `src/orpc/client.js` | oRPC client with TanStack Query integration |
| `src/orpc/router/index.js` | oRPC endpoint definitions |
| `src/routes/__root.tsx` | Root layout with all providers |
| `src/router.tsx` | Router configuration |
| `src/styles.css` | Global styles with CSS variables |
| `components.json` | shadcn/ui component configuration |

## Adding New Features

### New Route
Create file in `src/routes/` - filename becomes the URL path:
- `src/routes/users.tsx` → `/users`
- `src/routes/users/$id.tsx` → `/users/:id`

### New oRPC Endpoint
1. Add Zod schema in `src/orpc/schema.js`
2. Create handler in `src/orpc/router/`
3. Export from `src/orpc/router/index.js`

### New Database Table
1. Define table in `src/db/schema.ts`
2. Run `pnpm db:generate`
3. Run `pnpm db:migrate`

### New UI Component (shadcn)
```bash
npx shadcn@latest add <component-name>
```

## Troubleshooting

### Database connection errors
- Verify `DATABASE_URL` in `.env.local`
- Ensure PostgreSQL is running
- Run `pnpm db:push` for quick schema sync during development

### Auth not working
- Generate secret: `npx @better-auth/cli secret`
- Set `BETTER_AUTH_URL` to your app URL
- Check `/api/auth/$` route is present

### Type errors after schema changes
- Run `pnpm db:generate` to update types
- Restart TypeScript server in your editor
