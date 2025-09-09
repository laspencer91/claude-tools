## Overview

This repository contains agent-driven, opinionated workflows you can use to plan, review, and implement software features efficiently. It ships with ready-to-use profiles (preconfigured sets of agents) and a workflow creator for customizing to your stack.

## What's inside

- **`feature-workflow/`**: The workflows and profiles you can run as-is.
  - **`profiles/next-nest/`**: Full-stack profile (Next.js + Nest.js).
  - **`profiles/next-frontend-monorepo/`**: Frontend-only Next.js monorepo profile.
  - Top-level **`README.md`** in `feature-workflow/` explains philosophy and links to profiles.
- **`feature-workflow/workflow-creator/`**: Templates and the custom workflow creator to generate your own profile.
  - Frontend and backend agent templates (Next, React, Vue; Nest, Express, FastAPI, etc.).
  - Shared agents (technical reviewer, docs, finalization).
  - **`custom-workflow-creator.md`**: Guided prompts to produce a tailored profile.

## How to use

- **Use a ready-made profile**
  1. Open a profile at `feature-workflow/profiles/...`.
  2. Read its `README.md` for stack assumptions and agent list.
  3. Start with the `feature-planner` agent and proceed in order:
     - planner → designer/design-reviewer → web-technical-planner (and api if applicable) → technical-reviewer → engineer(s) → docs → finalization.
  4. Copy the agent files into your project or run them in-place as working guides.

- **Create a custom profile**
  1. Open `feature-workflow/workflow-creator/custom-workflow-creator.md`.
  2. Answer the prompts (monorepo vs single app, frontend/backend stacks, tooling, philosophy).
  3. The creator will scaffold a new profile under `feature-workflow/profiles/<your-profile>/` with tailored agent files and a profile `README.md`.

## Suggested starting points

- **Full-stack Next.js + Nest.js**: `feature-workflow/profiles/next-nest/`
- **Frontend-only Next.js monorepo**: `feature-workflow/profiles/next-frontend-monorepo/`

## Conventions

- **Agents** are markdown files describing responsibilities, deliverables, and checklists.
- **Profiles** bundle a curated set of agents for a specific stack and philosophy.
- **Philosophy** (in `feature-workflow/README.md`) outlines core practices (type-safety, clear architecture, alignment gates, pragmatic documentation).

## Notes

- You can mix and match agents across profiles.
- Use the creator to adapt language/framework choices, validation strategies, and review rigor to your needs.
