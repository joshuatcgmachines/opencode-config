# Personal Global Rules

Read the following file immediately as it is relevant to all coding workflows: @rules/coding-style.md

Before first response in every new chat and before each subagent task, load and apply skill `caveman` (default level: `full`).

If user says `/caveman lite|full|ultra`, switch level.
If user says `stop caveman` or `normal mode`, disable caveman for that session.

Build artifact cleanup:
- After running build/typecheck commands, remove `tsconfig.tsbuildinfo` if generated.
- Do not leave `tsconfig.tsbuildinfo` as an uncommitted workspace change unless user explicitly asks to keep it.

Never run Prisma reset commands unless user explicitly asks in current chat.
- Block all reset-like commands by default: `prisma migrate reset`, `prisma db reset`, `prisma db push --force-reset`, or any command that drops/recreates database.
- If user explicitly requests reset, require clear one-line confirmation right before execution.
- Prisma migration granularity: keep one `migration.sql` focused on one logical schema change.
- Example: if creating multiple tables, create one table per migration (separate migrations).

Data structure preference:
- Prefer arrays and array methods (`find`, `some`, `filter`, `map`) over `Map` and `Set` by default.
- Use `Map` only when strictly necessary: non-string keys, identity-based key semantics, or a measured performance hotspot.
- Use `Set` only when strictly necessary: enforcing value uniqueness or identity-based membership checks.

Testing policy:
- Never write tests. Do not create test files, add test cases, or suggest testing as part of any implementation plan or task.

Version control policy:
- Never commit any changes.

Database delegation policy:
- If request asks for SQL query writing/review/debugging, table joins, data checks, export matching, or Prisma/database work of any kind, route to `@database-expert`.
- Architect/planning agents must not hand-write final SQL for those tasks; they should delegate to `@database-expert`.
