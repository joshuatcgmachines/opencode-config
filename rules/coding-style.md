# Coding Style Rules

## TypeScript / JavaScript

- Use `!!value` for boolean coercion, not `Boolean(value)`.
- Write plain numeric literals without underscores: `10000`, not `10_000`.
- Omit explicit return types when TypeScript can infer them; only add them when inference fails or the type would be ambiguous to a reader.
- Boolean variables and props must use a semantic prefix: `is`, `are`, `has`, `should`, `can`, `did`, `will`, etc. (e.g. `isLoading`, `hasError`, `shouldRefetch`).
