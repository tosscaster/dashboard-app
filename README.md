# Dashboard App

A full-stack React application built on **TanStack Start** with server-side rendering, streaming, and type-safe APIs.

## Tech Stack

- **Framework**: TanStack Start + TanStack Router
- **Frontend**: React 19 (with React Compiler)
- **Styling**: Tailwind CSS + shadcn/ui
- **Database**: PostgreSQL + Drizzle ORM
- **Auth**: Better Auth
- **RPC**: oRPC (type-safe)
- **i18n**: Paraglide.js

## Getting Started

### Prerequisites

- Node.js 18+
- PostgreSQL database

### Installation

```bash
npm install
```

### Environment Setup

Create `.env.local`:

```bash
DATABASE_URL="postgresql://username:password@localhost:5432/mydb"
BETTER_AUTH_URL=http://localhost:3000
BETTER_AUTH_SECRET=  # Generate: npx @better-auth/cli secret
```

### Database Setup

```bash
npm run db:push    # Push schema to database
```

### Development

```bash
npm run dev        # Start dev server (port 3000)
```

## Commands

```bash
# Development
npm run dev           # Start dev server
npm run build         # Build for production
npm run preview       # Preview production build

# Testing & Quality
npm test              # Run tests (Vitest)
npm run lint          # Run ESLint
npm run format        # Run Prettier
npm run check         # Format + lint + fix all

# Database
npm run db:generate   # Generate migrations
npm run db:migrate    # Run migrations
npm run db:push       # Push schema (dev)
npm run db:studio     # Open Drizzle Studio
```

## Project Structure

```
src/
├── components/       # React components
│   └── ui/           # shadcn/ui components
├── routes/           # File-based routing
├── db/               # Database schema & client
├── orpc/             # oRPC endpoints
├── lib/              # Utilities
└── hooks/            # Custom hooks
```

## Adding Routes

Create a file in `src/routes/`:

```tsx
import { createFileRoute } from '@tanstack/react-router'

export const Route = createFileRoute('/my-page')({
  component: MyPage,
})

function MyPage() {
  return <div>My Page</div>
}
```

## Adding Components

```bash
npx shadcn@latest add button
```

## Demo Files

Files prefixed with `demo` are examples and can be safely deleted.

## Documentation

- [CLAUDE.md](./CLAUDE.md) - Detailed project documentation
- [AGENT.md](./AGENT.md) - AI agent instructions

## Learn More

- [TanStack Start](https://tanstack.com/start)
- [TanStack Router](https://tanstack.com/router)
- [Drizzle ORM](https://orm.drizzle.team)
- [Better Auth](https://better-auth.com)
- [shadcn/ui](https://ui.shadcn.com)
