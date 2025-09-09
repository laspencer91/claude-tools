# Feature Workflow Templates

An extensible library of agent templates and stack-specific building blocks used by the custom workflow configurator to scaffold an opinionated, production-friendly feature workflow across many projects.

## Goals

- Provide parameterized, high-fidelity agent definitions for popular stacks.
- Allow selective inclusion/exclusion of agents based on project shape (single workspace vs monorepo; frontend/backends present).
- Support multiple validation libraries, ORMs, and security postures with conditional content blocks.
- Keep outputs consistent with the opinionated patterns used in `feature-workflow/agents` while remaining adaptable.

## Directory Structure

```
workflow-creator/
├── README.md
├── variables.schema.json       # Formal configuration variables (JSON Schema)
├── mapping-spec.md             # Rules mapping variables → which templates/blocks to render
├── shared/
│   └── agents/                 # Cross-stack agents
│       ├── technical-reviewer.md.template
│       ├── code-documentation-specialist.md.template
│       └── finalization-agent.md.template
├── frontends/
│   ├── next/
│   │   ├── feature-planner.md.template
│   │   ├── designer.md.template
│   │   ├── design-reviewer.md.template
│   │   ├── web-technical-planner.md.template
│   │   └── next-engineer.md.template
│   ├── react/
│   │   ├── feature-planner.md.template
│   │   ├── web-technical-planner.md.template
│   │   └── react-engineer.md.template
│   └── vue/
│       ├── feature-planner.md.template
│       ├── web-technical-planner.md.template
│       └── vue-engineer.md.template
├── backends/
│   ├── nest/
│   │   ├── api-technical-planner.md.template
│   │   └── nest-engineer.md.template
│   ├── express/
│   │   ├── api-technical-planner.md.template
│   │   └── express-engineer.md.template
│   ├── fastapi/
│   │   ├── api-technical-planner.md.template
│   │   └── fastapi-engineer.md.template
│   ├── django/
│   │   ├── api-technical-planner.md.template
│   │   └── django-engineer.md.template
│   └── gin/
│       ├── api-technical-planner.md.template
│       └── gin-engineer.md.template
└── shared-contracts/
    ├── zod/
    │   ├── guidelines.md.template
    │   └── example.contract.ts.template
    └── pydantic/
        ├── guidelines.md.template
        └── example_contract.py.template
```

## Template Syntax

- Variables: `{{ variable.path }}`
- Conditionals: `{{#if condition}} ... {{/if}}`, `{{#unless condition}} ... {{/unless}}`
- Switch/when: `{{#switch variable}} {{#case 'value'}}...{{/case}} {{/switch}}`
- Loops: `{{#each arrayVar}} ... {{/each}}`

Conditions and variables come from the configuration that conforms to `variables.schema.json`.
The configurator is responsible for evaluating conditions and rendering final files.

## How Selection Works

1. Collect answers for variables defined in `variables.schema.json`.
2. Apply rules in `mapping-spec.md` to determine:
   - Which agent templates to render
   - Which conditional blocks to include
   - Which terminology to use (e.g., API proxying, auth strategy, schema lib)
3. Render templates to the target workflow folder (usually `feature-workflow/agents/`) and write a tailored `README.md`.

## Supported Choices (Initial Set)

- Frontend frameworks: Next.js, React, Vue
- Backend frameworks: Nest.js, Express (Node), FastAPI, Django (Python), Gin (Go)
- Validation libraries: Zod, Joi, Pydantic, DRF Serializers, go-playground/validator
- ORMs/DB layers: Prisma, TypeORM, Sequelize (Node); SQLAlchemy (Py), Django ORM, GORM (Go)
- Package managers: pnpm, yarn, npm
- Security posture: MVP-basic, Advanced

This library is designed to grow. Add new stacks by introducing a new folder under `frontends/` or `backends/` and extending the mapping rules.


