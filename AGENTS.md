# Personal Global Rules

Before first response in every new chat and before each subagent task, load and apply skill `caveman` (default level: `full`).
Exception: do not apply caveman style when preparing input for `sequential-thinking` MCP calls; use normal precise technical language for those calls.

If user says `/caveman lite|full|ultra`, switch level.
If user says `stop caveman` or `normal mode`, disable caveman for that session.

Never run Prisma reset commands unless user explicitly asks in current chat.
- Block all reset-like commands by default: `prisma migrate reset`, `prisma db reset`, `prisma db push --force-reset`, or any command that drops/recreates database.
- If user explicitly requests reset, require clear one-line confirmation right before execution.
- Prisma migration granularity: keep one `migration.sql` focused on one logical schema change.
- Example: if creating multiple tables, create one table per migration (separate migrations).

Only invoke `sequential-thinking` MCP for genuinely complex, multi-step reasoning tasks. Do not use it for straightforward requests — it consumes significant tokens.

Use `superlocalmemory` MCP when appropriate.
- At task start, recall memory when request depends on prior decisions, user preferences, project conventions, or earlier unresolved commitments.
- When recalled memories materially influence the work, call `mcp__superlocalmemory__report_outcome` with used `memory_ids` and outcome (`success`, `partial`, or `failure`) to improve future retrieval.
- At task end, capture only durable, reusable facts (stable preferences, workflow rules, architecture decisions, environment constraints, and explicit follow-ups).
- Prefer `mcp__superlocalmemory__observe` for end-of-task capture.
- Use `mcp__superlocalmemory__remember` only when explicit deterministic storage is needed; before calling it, check `list_recent` and skip if same fact content already exists.
- Never store secrets, credentials, tokens, private keys, or one-off transient debugging details.
- If recalled memory conflicts with explicit current-chat instructions, follow current-chat instructions and update memory accordingly.
