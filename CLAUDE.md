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
| **Styling** | Tailwind CSS, shadcn/ui (new-york, zinc) | 4.0.6 |
| **Backend** | Nitro server runtime | nightly |
| **RPC** | oRPC (type-safe RPC) | 1.13.0 |
| **Database** | PostgreSQL + Drizzle ORM + Drizzle Kit | 0.45.0, 0.31.8 |
| **Auth** | Better Auth (email/password, sessions) | 1.4.12 |
| **Validation** | Zod 4 | 4.1.11 |
| **i18n** | Paraglide.js | 2.8.0 |
| **Env** | @t3-oss/env-core (type-safe env) | 0.13.8 |
| **Build** | Vite, TypeScript (strict) | 7.1.7, 5.7.2 |
| **Testing** | Vitest, React Testing Library | 3.0.5, 16.2.0 |
| **Icons** | Lucide React | 0.561.0 |
| **Data** | Faker.js | 10.0.0 |

## Commands

```bash
# Development
npm run dev           # Start dev server (port 3000)
npm run build         # Build for production
npm run preview       # Preview production build

# Testing & Quality
npm test              # Run tests (Vitest)
npm run lint          # Run ESLint
npm run format        # Run Prettier
npm run check         # Format + lint + fix all

# Database (Drizzle)
npm run db:generate   # Generate migrations from schema changes
npm run db:migrate    # Run pending migrations
npm run db:push       # Push schema directly to database (dev)
npm run db:pull       # Pull schema from database
npm run db:studio     # Open Drizzle Studio GUI
```

## Project Structure

```
src/
├── components/           # React components
│   ├── Header.tsx        # Main navigation with demo links
│   ├── LocaleSwitcher.tsx # i18n locale picker
│   ├── demo.*.tsx        # Demo-specific components (FormComponents, chat-area, messages)
│   └── ui/               # shadcn/ui components
│       └── input.tsx     # Input component
├── routes/               # File-based routing (TanStack Router)
│   ├── __root.tsx        # Root layout with providers
│   ├── index.tsx         # Homepage
│   ├── api.$.js          # Catch-all API handler
│   ├── api.rpc.$.js      # oRPC endpoint handler
│   ├── demo.i18n.tsx     # i18n demo route
│   ├── demo/             # Demo feature routes
│   │   ├── drizzle.tsx   # Database CRUD demo
│   │   ├── better-auth.tsx # Auth demo
│   │   ├── orpc-todo.tsx # oRPC demo
│   │   ├── tanstack-query.tsx # TanStack Query demo
│   │   ├── form.*.tsx    # TanStack Form demos (simple, address)
│   │   ├── table.tsx     # TanStack Table demo
│   │   ├── store.tsx     # TanStack Store demo
│   │   ├── db-chat.tsx   # Chat with TanStack React DB
│   │   ├── db-chat-api.js # Chat API endpoint
│   │   ├── api.tq-todos.ts # Todos API for TanStack Query
│   │   ├── api.names.js  # Names API endpoint
│   │   └── start.*.tsx   # SSR/streaming demos (ssr, server-funcs, api-request)
│   └── api/
│       └── auth/$.js     # Better Auth handler
├── db/
│   ├── index.ts          # Drizzle client setup
│   └── schema.ts         # Database table definitions (todos)
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
│   │   ├── root-provider.tsx
│   │   └── devtools.tsx
│   └── better-auth/
│       └── header-user.tsx # Auth header component
├── hooks/                # Custom React hooks
│   ├── demo.form.js      # Form hook factory
│   ├── demo.form-context.js # Form context hook
│   └── demo.useChat.js   # Chat with streaming
├── lib/
│   ├── auth.js           # Better Auth server config
│   ├── auth-client.js    # Better Auth client
│   ├── demo-store.js     # TanStack Store example
│   ├── demo-store-devtools.tsx # Store devtools integration
│   └── utils.js          # cn() utility (clsx + tailwind-merge)
├── data/                 # Demo data (Faker generated)
│   ├── demo.punk-songs.js
│   └── demo-table-data.js
├── paraglide/            # Generated i18n files
├── env.js                # Type-safe environment variables (@t3-oss/env-core)
├── polyfill.js           # Browser polyfills
├── server.ts             # Server entry point
├── styles.css            # Global Tailwind styles
├── logo.svg              # App logo
└── router.tsx            # Router configuration

messages/                 # i18n message files
├── en.json               # English translations
└── de.json               # German translations

drizzle/                  # Generated migrations

Root configs:
├── vite.config.ts        # Vite + TanStack + Tailwind + Paraglide + Nitro
├── drizzle.config.ts     # Drizzle ORM config
├── tsconfig.json         # TypeScript (strict mode, ES2022)
├── eslint.config.js      # ESLint (TanStack config)
├── prettier.config.js    # Prettier (no semi, single quotes, trailing commas)
├── components.json       # shadcn/ui config (new-york style, zinc base)
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
- Use Zod 4 schemas for input validation (defined in `src/orpc/schema.js`)
- oRPC endpoints available at `/api/rpc`
- Server functions use `createServerFn` from TanStack Start

### State Management
- **Server state**: TanStack Query (use `orpc` utils for oRPC integration)
- **Client state**: TanStack Store for simple state
- **Local collections**: TanStack React DB with Zod validation

### Database
- Define tables in `src/db/schema.ts` using Drizzle's `pgTable`
- Import `db` from `@/db` for queries
- Run `npm run db:generate` after schema changes, then `npm run db:migrate`

### Environment Variables
- Use `@t3-oss/env-core` for type-safe env validation
- Define schemas in `src/env.js`
- Client variables must use `VITE_` prefix

## Environment Variables

Required in `.env.local`:

```bash
# PostgreSQL connection (required)
DATABASE_URL="postgresql://username:password@localhost:5432/mydb"

# Better Auth (required)
BETTER_AUTH_URL=http://localhost:3000
BETTER_AUTH_SECRET=  # Generate: npx @better-auth/cli secret

# Optional
SERVER_URL=           # Server URL override
VITE_APP_TITLE=       # App title (client-side)
```

## Testing

- **Framework**: Vitest with React Testing Library
- **Run**: `npm test`
- **Location**: Place tests next to source files (`*.test.ts(x)`) or in `__tests__/` directories
- **Environment**: JSDOM for DOM simulation

## Key Files

| File | Purpose |
|------|---------|
| `vite.config.ts` | Build config with TanStack, Tailwind, Paraglide, Nitro plugins |
| `drizzle.config.ts` | Database ORM configuration |
| `src/db/schema.ts` | Database table definitions |
| `src/env.js` | Type-safe environment variable validation |
| `src/lib/auth.js` | Better Auth server configuration |
| `src/lib/auth-client.js` | Better Auth client setup |
| `src/orpc/client.js` | oRPC client with TanStack Query integration |
| `src/orpc/router/index.js` | oRPC endpoint definitions |
| `src/routes/__root.tsx` | Root layout with all providers |
| `src/routes/api.rpc.$.js` | oRPC API route handler |
| `src/router.tsx` | Router configuration |
| `src/server.ts` | Server entry point |
| `src/styles.css` | Global styles with CSS variables |
| `components.json` | shadcn/ui component configuration |

## Adding New Features

### New Route
Create file in `src/routes/` - filename becomes the URL path:
- `src/routes/users.tsx` → `/users`
- `src/routes/users/$id.tsx` → `/users/:id`
- `src/routes/demo/feature.tsx` → `/demo/feature`

### New oRPC Endpoint
1. Add Zod schema in `src/orpc/schema.js`
2. Create handler in `src/orpc/router/`
3. Export from `src/orpc/router/index.js`

### New Database Table
1. Define table in `src/db/schema.ts`
2. Run `npm run db:generate`
3. Run `npm run db:migrate`

### New UI Component (shadcn)
```bash
npx shadcn@latest add <component-name>
```
Components are installed to `src/components/ui/` with new-york style and zinc base color.

### New Environment Variable
1. Add to `.env.local`
2. Define schema in `src/env.js` (server or client section)
3. Use `VITE_` prefix for client-side variables

## Troubleshooting

### Database connection errors
- Verify `DATABASE_URL` in `.env.local`
- Ensure PostgreSQL is running
- Run `npm run db:push` for quick schema sync during development

### Auth not working
- Generate secret: `npx @better-auth/cli secret`
- Set `BETTER_AUTH_URL` to your app URL
- Check `/api/auth/$` route is present

### Type errors after schema changes
- Run `npm run db:generate` to update types
- Restart TypeScript server in your editor

### Environment variable errors
- Check `src/env.js` for required variables
- Ensure client variables have `VITE_` prefix
- Restart dev server after changing `.env.local`
