---
description: Create a manual QA test plan
---

Ask @manual-test-planner to create a concise manual test plan that covers all changes in the current branch against `main` by default (unless user specifies another comparison target); include a concise summary of relevant chat-context changes, validate that summary against `git diff main...HEAD` (and `git status` only to flag separate uncommitted local changes), and return user-facing Markdown with plain numbered steps and clear expected results.
