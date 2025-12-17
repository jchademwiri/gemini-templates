# Project Context: Astro + Starwind UI + Hono API

## Tech Stack
- **Framework:** Astro 5 (Island Architecture)
- **API Engine:** Hono (mounted at `/api/*`)
- **Database:** Neon (Postgres) via `drizzle-orm/neon-http`
- **Auth:** Better-Auth (Drizzle Adapter)
- **Emails:** React Email + Resend
- **Styling:** Starwind UI (Tailwind CSS v4)
- **Runtime:** Bun

## Architecture & Hono API
- **API Entry:** Logic lives in `src/pages/api/[...path].ts`. Export a single Hono app instance.
- **Type Safety:** Always export `AppType` from the Hono server for frontend RPC (`hc`).
- **Better-Auth Integration:** - Mount Better-Auth inside Hono: `app.on(["POST", "GET"], "/api/auth/*", (c) => auth.handler(c.req.raw))`.
  - Use Hono middleware to set `c.var.user` for protected routes.

## Database & Auth Patterns
- **Drizzle Schema:** Follow Better-Auth's required schema (User, Session, Account, Verification).
- **Client Auth:** Use `createAuthClient` from `better-auth/client` in interactive islands.
- **Islands:** Use `client:load` for Auth forms and `client:idle` for non-critical Starwind UI components.

## Email Workflow
- Templates live in `src/emails/`. 
- Use Resend for delivery. Always wrap email sending in a Zod-validated Hono endpoint.

## Key Commands
- `bun run dev` - Start development server.
- `bun x drizzle-kit push` - Sync schema to Neon.
- `bun build` - Production build check.