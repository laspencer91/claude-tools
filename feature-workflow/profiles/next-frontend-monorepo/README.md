# Next Frontend Monorepo Profile

A customized, frontend-only workflow for a monorepo using Next.js (App Router), React Context, Tailwind CSS v4, Yarn, and a shared UI package at `packages/optiframe-ui`. API access is proxied via Next API routes to Optimizely services (GraphQL via Optimizely Graph; REST via `api/v3.0/contentmanagement`) using server-side fetch.

## Stack Summary
- Framework: Next.js (App Router)
- State: React Context
- Styling: Tailwind CSS v4; reusable components in `packages/optiframe-ui`
- Package manager: Yarn
- Build for shared packages: tsup
- Testing: Jest (to be implemented later)
- Contracts: none shared yet (UI package only)
- Security: API proxying through Next API routes for server-side token handling
- Performance: Post-MVP priority
- Accessibility: Minimal
- Documentation: Minimal
- Review rigor: Flexible recommendations

## Component Signature & Structure
Use this component signature and colocate feature code (components, hooks, tests, styles) with the feature:
```tsx
interface ComponentProps { /* ... */ }
function ComponentName({ /* ... */ }: ComponentProps) {
  // ...
}
```

## Agents in this Profile
- feature-planner
- designer
- design-reviewer
- web-technical-planner
- technical-reviewer (frontend-only)
- next-engineer
- code-documentation-specialist (minimal)
- finalization-agent

See `agents/` for each agent’s responsibilities and outputs.
