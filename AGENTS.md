# Personal Global Rules

Before first response in every new chat and before each subagent task, load and apply skill `caveman` (default level: `full`).
Exception: do not apply caveman style when preparing input for `sequential-thinking` MCP calls; use normal precise technical language for those calls.

If user says `/caveman lite|full|ultra`, switch level.
If user says `stop caveman` or `normal mode`, disable caveman for that session.

Never run Prisma reset commands unless user explicitly asks in current chat.
- Block all reset-like commands by default: `prisma migrate reset`, `prisma db reset`, `prisma db push --force-reset`, or any command that drops/recreates database.
- If user explicitly requests reset, require clear one-line confirmation right before execution.
