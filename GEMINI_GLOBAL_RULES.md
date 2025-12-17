# Universal Developer Rules & Environment

## Workflow & Stability
- **TDD (Test-Driven Development):** Always follow a test-driven workflow. Write or update tests before/alongside feature logic.
- **Build Verification:** Always run `bun run build` immediately after completing code edits.
- **Error Resolution:** If the build fails, fix all build errors immediately. Never leave the codebase in a non-buildable state.

## Runtime & Package Management
- **Primary Runtime:** Bun.
- **Commands:** Always prefer `bun` over `npm`, `yarn`, or `pnpm`.
- **CLI Tools:** Use `bunx --bun [command]` (e.g., `bunx --bun drizzle-kit push`).

## TypeScript Standards
- **Strict Mode:** Always enabled.
- **No Implicit Any:** Never use `any`. Use `unknown` if a type is truly dynamic.
- **Data Modeling:** Prefer `interface` over `type` for object definitions.

## Environment & Security
- **Required Vars:** Always verify existence of `DATABASE_URL`, `BETTER_AUTH_SECRET`, and `RESEND_API_KEY`.
- **Validation:** Use a Zod-backed `env.ts` to validate these at runtime.

## Windows / PowerShell Workflow
- **Script Execution:** If a command is blocked, use `powershell -ExecutionPolicy Bypass -File [script]`.