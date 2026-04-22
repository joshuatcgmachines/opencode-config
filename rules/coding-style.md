# Coding Style Rules

## TypeScript / JavaScript

- Use `!!value` for boolean coercion, not `Boolean(value)`.
- Write plain numeric literals without underscores: `10000`, not `10_000`.
- Omit explicit return types when TypeScript can infer them; only add them when inference fails or the type would be ambiguous to a reader.
- Prefer destructuring for objects and arrays when accessing multiple properties or elements. When a destructured name would be ambiguous without its source context, rename it inline (e.g. `const { id: userId } = user` instead of a bare `id`).
- Boolean variables and props must use a semantic prefix: `is`, `are`, `has`, `should`, `can`, `did`, `will`, etc. (e.g. `isLoading`, `hasError`, `shouldRefetch`).
- Prefer `async`/`await` over `.then()`/`.catch()` chains for Promise handling.
- Prefer arrow function expressions over function declarations: `const foo = () => {}` not `function foo() {}`. Exceptions: class methods, object methods that use `this`, generator functions, and any context where hoisting is required.
- Prefer named exports over default exports. Only use `export default` when required by a framework convention (e.g. Next.js page/layout files, dynamic `import()` with named-export limitations).
