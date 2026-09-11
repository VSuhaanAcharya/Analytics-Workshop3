---
description: 'Commenting and documentation standards for the Tailspin Toys codebase'
applyTo: '**/*.{ts,astro,css}'
---

# Commenting and Documentation Instructions

## Comment Philosophy

- Explain **why** code exists, including intent, constraints, trade-offs, and non-obvious decisions.
- Do not restate what the code already says. If a comment only paraphrases a statement or repeats a variable name, remove it.
- Keep comments concise and close to the decision or behavior they explain.
- Treat stale comments as bugs: update or delete a comment in the same change that modifies the related code.
- Prefer clear names and straightforward code over comments that explain avoidable complexity.

## TypeScript Documentation

- Every exported function in `db/` and `src/lib/` must have a TSDoc/JSDoc comment.
- Document the function's purpose, every parameter with `@param`, and its return value with `@returns`. Document important thrown errors when they are part of the function's contract.
- For data-access helpers, document the injectable `db` parameter and explain that callers can provide an in-memory database in tests.
- Keep type annotations explicit for exported functions and data-layer callbacks; use the repository's existing two-space indentation and formatting.

```ts
/**
 * Returns games in stable title order for deterministic static builds.
 *
 * @param db Injectable database client used for production or tests.
 * @returns Games mapped to the app-facing shape.
 */
export async function getAllGames(db: Database): Promise<Game[]> {
  // ...
}
```

## Astro Component Contracts

- Every reusable `.astro` component must define a `Props` interface in its frontmatter.
- Add a short TSDoc comment above `Props` describing the component contract, especially required values and meaningful defaults.
- Keep the interface aligned with the component's actual props; update it whenever the component API changes.

