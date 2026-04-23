# Personal Global Rules

Read the following file immediately as it is relevant to all coding workflows: @rules/coding-style.md

Before first response in every new chat and before each subagent task, load and apply skill `caveman` (default level: `full`).

If user says `/caveman lite|full|ultra`, switch level.
If user says `stop caveman` or `normal mode`, disable caveman for that session.

Never run Prisma reset commands unless user explicitly asks in current chat.
- Block all reset-like commands by default: `prisma migrate reset`, `prisma db reset`, `prisma db push --force-reset`, or any command that drops/recreates database.
- If user explicitly requests reset, require clear one-line confirmation right before execution.
- Prisma migration granularity: keep one `migration.sql` focused on one logical schema change.
- Example: if creating multiple tables, create one table per migration (separate migrations).

Database delegation policy:
- If request asks for SQL query writing/review/debugging, table joins, data checks, export matching, or Prisma/database work of any kind, route to `@database-expert`.
- Architect/planning agents must not hand-write final SQL for those tasks; they should delegate to `@database-expert`.
