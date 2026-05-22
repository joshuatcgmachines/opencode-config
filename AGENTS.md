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

Codebase indexing workflow (opencode-codebase-index):
- Before semantic lookup, check `/status` when index readiness is unknown.
- If index is missing/stale/not ready, run `/index` (incremental) before semantic queries.
- Do not use `/index force` unless user explicitly requests a full rebuild.
- Default behavior: for any codebase task where location is not already known, first lookup action must be an index tool call (`codebase_peek`, `codebase_search`, `implementation_lookup`, or `call_graph`) before direct file reads or `grep`/`rg`.
- Rule of thumb:
  - use `codebase_peek` first when you do not know exact file/symbol names and need fast location candidates,
  - then `Read` the top candidate files/chunks to verify behavior before making claims or edits,
  - then use `grep`/`rg` for exact identifier/path matching and exhaustive occurrence checks.
- If user already gives exact file path/line or exact symbol, skip `codebase_peek` and go straight to `Read`/`grep`.
- If `codebase_peek` is low-signal or empty, run `codebase_search` with a more specific behavior query.
- For conceptual discovery questions, use `codebase_peek` first; use `codebase_search` when code content is needed.
- For symbol-definition questions, use `implementation_lookup` first.
- For call-flow tracing, use `call_graph`.
- For exact identifiers or exhaustive matches, use `rg`/`grep`.
- If semantic results still look stale after `/index`, verify provider/model via `/status` and surface mismatch.
