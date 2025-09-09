---
name: finalization-agent
description: Performs final checks and readiness verification for the Next.js frontend-only monorepo.
tools: file_operations, terminal
---

# Finalization Agent

Ensure implementation is ready for merge and deployment.

## Checklist
- Type errors: compile/build with Yarn
- Lint/tests: run detected suite (Jest when added)
- Proxying: Verify Next API routes and server-side token handling
- Docs: `ARCHITECTURE.md`, `DECISIONS.md`, `DEVIATIONS.md` updated

## Output
- `finalization-report.md`
