# Mapping Specification

This document defines how configurator inputs (see `variables.schema.json`) map to concrete templates and conditional content blocks.

## Selection Algorithm (High-Level)

1. Determine presence of frontend/backend via `frontend.present`, `backend.present`.
2. For each present layer, select framework folder under `frontends/` or `backends/` based on `framework`.
3. Always include cross-stack agents from `shared/agents/` unless excluded by rules.
4. Resolve validation/ORM/security variants to set template variables and condition flags.
5. Render templates with conditionals; write outputs to `feature-workflow/agents/` and update the top-level `feature-workflow/README.md` using stack-specific sections.

## Template Inclusion Rules

- If `frontend.present == true`:
  - Include: `frontends/{{frontend.framework}}/web-technical-planner.md.template`
  - Include: `frontends/{{frontend.framework}}/{{frontend.framework}}-engineer.md.template`
  - Include: `frontends/{{frontend.framework}}/feature-planner.md.template`
  - For Next: also include `designer.md.template`, `design-reviewer.md.template` (optional for React/Vue if desired)

- If `backend.present == true`:
  - Include: `backends/{{backend.framework}}/api-technical-planner.md.template`
  - Include: `backends/{{backend.framework}}/{{backend.framework}}-engineer.md.template`

- Always include (unless explicitly turned off):
  - `shared/agents/technical-reviewer.md.template`
  - `shared/agents/code-documentation-specialist.md.template`
  - `shared/agents/finalization-agent.md.template`

## Conditional Content Flags (examples)

Set the following booleans for template logic:

- `isMonorepo = project.type == 'monorepo'`
- `usesNext = frontend.framework == 'next'`
- `usesReact = frontend.framework == 'react'`
- `usesVue = frontend.framework == 'vue'`
- `usesApiProxy = usesNext`  # default heuristic; override if user disables
- `usesZod = contracts.validation == 'zod'`
- `usesJoi = contracts.validation == 'joi'`
- `usesPydantic = contracts.validation == 'pydantic'`
- `usesDRFSerializers = contracts.validation == 'drf-serializers'`
- `usesGoValidator = contracts.validation == 'goplayground'`
- `usesPrisma = backend.orm == 'prisma'`
- `usesTypeORM = backend.orm == 'typeorm'`
- `usesSQLAlchemy = backend.orm == 'sqlalchemy'`
- `usesDjangoORM = backend.orm == 'django-orm'`
- `usesGORM = backend.orm == 'gorm'`

Additional convenience strings for templates:

- `sharedContractsPath = contracts.sharedLocation || (isMonorepo ? 'monorepo-root/packages/shared' : 'src/common/shared')`
- `packageManager = project.packageManager`

## Output Targets

- Agents: `feature-workflow/agents/`
- README: `feature-workflow/README.md` (assemble from stack-specific sections + philosophy)

## Example Mappings

### 1) Next + Nest + Zod + Prisma (Monorepo)

- Include next frontend templates (planner, designer, reviewer, web planner, next engineer)
- Include nest backend templates (api planner, nest engineer)
- Technical reviewer strict on Next API proxy and shared Zod schemas
- Shared contracts: Zod examples

### 2) React + Express + Joi + Prisma (Single)

- Include react web planner + react engineer
- Include express api planner + express engineer
- Reviewer adapts: no Next proxy; emphasize REST endpoints and Joi validation alignment

### 3) Vue + FastAPI + Pydantic + SQLAlchemy (Monorepo)

- Include vue web planner + vue engineer
- Include fastapi api planner + fastapi engineer
- Reviewer focuses on OpenAPI/Pydantic parity; state via vue-query/pinia

## Conflict Resolution

If incompatible choices are selected (e.g., `backend.framework = django` with `contracts.validation = zod`), the configurator should:

1) Warn and suggest compatible alternatives; 2) Offer a bridging strategy (e.g., server emits OpenAPI, frontend generates clients/types; or maintain an independent shared schema package).


