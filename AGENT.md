# AGENT.md

Instructions for AI agents working with this codebase.

## Quick Reference

```bash
# Essential commands
npm run dev           # Start development server
npm run build         # Build for production
npm test              # Run tests
npm run check         # Format + lint + fix all

# Database
npm run db:generate   # Generate migrations
npm run db:migrate    # Run migrations
npm run db:push       # Push schema (dev)
```

## Before Making Changes

1. **Read relevant files first** - Understand existing code before modifying
2. **Check imports** - Use `@/*` path alias for all src imports
3. **Follow formatting** - No semicolons, single quotes, trailing commas

## Code Patterns

### Creating Components
```tsx
import { cn } from '@/lib/utils'

export function MyComponent({ className }: { className?: string }) {
  return <div className={cn('base-styles', className)}>...</div>
}
```

### Adding API Endpoints (oRPC)
1. Define Zod schema in `src/orpc/schema.js`
2. Create handler in `src/orpc/router/`
3. Export from `src/orpc/router/index.js`

### Database Operations
```ts
import { db } from '@/db'
import { todos } from '@/db/schema'

// Query
const items = await db.select().from(todos)

// Insert
await db.insert(todos).values({ title: 'New item' })
```

### Server Functions
```ts
import { createServerFn } from '@tanstack/react-start'

const myServerFn = createServerFn({ method: 'GET' })
  .handler(async () => {
    return { data: 'from server' }
  })
```

## File Naming Conventions

| Type | Pattern | Example |
|------|---------|---------|
| Route | `src/routes/[name].tsx` | `src/routes/users.tsx` |
| API Route | `src/routes/api.[name].js` | `src/routes/api.users.js` |
| Component | `src/components/[Name].tsx` | `src/components/Header.tsx` |
| Demo component | `src/components/demo.[name].tsx` | `src/components/demo.chat-area.tsx` |
| Hook | `src/hooks/[name].js` | `src/hooks/demo.useChat.js` |
| UI (shadcn) | `src/components/ui/[name].tsx` | `src/components/ui/button.tsx` |

## Common Tasks

### Add a new page
Create `src/routes/[page-name].tsx`:
```tsx
import { createFileRoute } from '@tanstack/react-router'

export const Route = createFileRoute('/page-name')({
  component: PageComponent,
})

function PageComponent() {
  return <div>Page content</div>
}
```

### Add a shadcn component
```bash
npx shadcn@latest add button
```

### Add a database table
1. Edit `src/db/schema.ts`
2. Run `npm run db:generate`
3. Run `npm run db:migrate`

### Add an environment variable
1. Add to `.env.local`
2. Define schema in `src/env.js`
3. Use `VITE_` prefix for client-side

## Do Not

- Skip reading files before editing
- Use relative imports instead of `@/*` alias
- Add semicolons (Prettier removes them)
- Use double quotes for strings (use single quotes)
- Commit without running `npm run check`
- Push directly to main branch

## Testing

- Place tests next to source files: `Component.test.tsx`
- Or use `__tests__/` directories
- Run with `npm test`

## Environment

Required variables in `.env.local`:
- `DATABASE_URL` - PostgreSQL connection string
- `BETTER_AUTH_URL` - App URL for auth
- `BETTER_AUTH_SECRET` - Auth secret key

## Related Documentation

- [CLAUDE.md](./CLAUDE.md) - Detailed project documentation
- [README.md](./README.md) - Getting started guide
