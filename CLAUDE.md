# CLAUDE.md

This file provides guidance for Claude Code when working with this repository.

## Project Overview

This is a full-stack React application built on **TanStack Start** - a modern framework for building web applications with server-side rendering, streaming, and type-safe APIs.

## Tech Stack

- **Framework**: TanStack Start + TanStack Router (file-based routing)
- **Frontend**: React 19, TanStack Query, TanStack Form, TanStack Store
- **Styling**: Tailwind CSS 4, shadcn/ui components
- **Backend**: Nitro server runtime, oRPC (type-safe RPC)
- **Database**: PostgreSQL with Drizzle ORM
- **Auth**: Better Auth (email/password, session-based)
- **Build**: Vite 7, TypeScript 5.7 (strict mode)
- **i18n**: Paraglide.js

## Common Commands

```bash
pnpm dev           # Start dev server (port 3000)
pnpm build         # Build for production
pnpm test          # Run tests (Vitest)
pnpm lint          # Run ESLint
pnpm format        # Run Prettier
pnpm check         # Format + lint + fix

# Database
pnpm db:generate   # Generate Drizzle migrations
pnpm db:migrate    # Run migrations
pnpm db:push       # Push schema to database
pnpm db:studio     # Open Drizzle Studio GUI
```

## Project Structure

```
src/
├── components/       # React components (Header, LocaleSwitcher, ui/)
├── routes/           # File-based routing (TanStack Router)
│   ├── __root.tsx    # Root layout
│   ├── index.tsx     # Homepage
│   ├── demo/         # Demo feature routes
│   └── api/          # API routes
├── db/               # Database schema and client (Drizzle)
├── orpc/             # oRPC API handlers and schemas
├── integrations/     # Third-party integrations (query, auth)
├── hooks/            # Custom React hooks
├── lib/              # Utilities and configs
└── styles.css        # Global styles
```

## Code Conventions

- **Imports**: Use path aliases `@/*` for src imports
- **Formatting**: No semicolons, single quotes, trailing commas (Prettier)
- **Components**: Use shadcn/ui components from `@/components/ui/`
- **API Routes**: Define type-safe handlers in `src/orpc/router/`
- **Validation**: Use Zod schemas for API input validation
- **State**: TanStack Query for server state, TanStack Store for client state

## Testing

- Test framework: Vitest with React Testing Library
- Run tests: `pnpm test`
- Test files: Place next to source files or in `__tests__/` directories

## Environment Variables

Required variables in `.env.local`:
- `DATABASE_URL` - PostgreSQL connection string
- `BETTER_AUTH_SECRET` - Auth secret key
- `BETTER_AUTH_URL` - Auth callback URL

## Key Files

- `vite.config.ts` - Build configuration with TanStack plugins
- `drizzle.config.ts` - Database ORM configuration
- `src/db/schema.ts` - Database table definitions
- `src/lib/auth.js` - Authentication configuration
- `src/router.tsx` - Router configuration
