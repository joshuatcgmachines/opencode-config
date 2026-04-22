# Coding Style Rules

All rules below are defaults and can be overridden by the user on request.

## TypeScript / JavaScript

- Use `!!value` for boolean coercion, not `Boolean(value)`.
- Write plain numeric literals without underscores: `10000`, not `10_000`.
- Omit explicit return types when TypeScript can infer them; only add them when inference fails or the type would be ambiguous to a reader.
- Prefer destructuring for objects and arrays, including function parameters. When a destructured name would be ambiguous without its source context, rename it inline rather than avoiding destructuring (e.g. `({ id: itemId, name }) => ({ itemId, name })` instead of `(item) => ({ itemId: item.id, name: item.name })`).
- Boolean variables and props must use a semantic prefix: `is`, `are`, `has`, `should`, `can`, `did`, `will`, etc. (e.g. `isLoading`, `hasError`, `shouldRefetch`).
- Prefer `async`/`await` over `.then()`/`.catch()` chains for Promise handling.
- Prefer `.forEach()` and `.map()` over `for` loops where appropriate.
- Prefer arrow function expressions over function declarations: `const foo = () => {}` not `function foo() {}`. Exceptions: class methods, object methods that use `this`, generator functions, and any context where hoisting is required.
- Prefer named exports over default exports. Only use `export default` when required by a framework convention (e.g. Next.js page/layout files, dynamic `import()` with named-export limitations).
- React component props types must be named after their component with a `Props` suffix: e.g. `MyComponentProps` for `MyComponent`.
