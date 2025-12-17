# Project Context: Next.js + shadcn/ui + Hono API

## Tech Stack
- **Framework:** Next.js 15 (App Router)
- **API Engine:** Hono (mounted at `/api/[[...route]]/route.ts`)
- **Database:** Neon (Postgres)
- **Auth:** Better-Auth (Next.js Middleware + Hono)
- **Emails:** React Email + Resend
- **UI:** shadcn/ui + Tailwind CSS v4
- **Runtime:** Bun

## Architecture Rules
- **Server Actions:** Use for simple mutations. For complex logic or cross-framework compatibility, use **Hono API routes**.
- **Hono RPC:** Use the `hc` (Hono Client) in Client Components for type-safe fetching.
- **Better-Auth:** - Use `toNextJsHandler` for the main auth route.
  - Access sessions in Server Components via `auth.getSession(headers())`.
- **UI Components:** shadcn lives in `@/components/ui`. Use the `cn()` utility for all class merging.

## Data & Validation
- **Neon/Drizzle:** Use the serverless HTTP driver. 
- **Zod:** Mandatory for all API inputs via `@hono/zod-validator` and all Form schemas.
- **Emails:** Centralize Resend logic in `src/lib/resend.ts`.

## Code Style
- **Server-First:** Keep the client-side bundle small. Default to Server Components.
- **Absolute Imports:** Use `@/` for all project paths.

## Key Commands
- `bun dev` - Dev mode.
- `bun x drizzle-kit studio` - View database.
- `bunx --bun shadcn@latest add [component]` - Add UI primitives.