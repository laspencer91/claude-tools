# Philosophy of Agent Workflow

This workflow emphasizes a **streamlined, opinionated, and highly collaborative development approach**, heavily influenced by a modern TypeScript-centric stack.

**Key tenets include:**

*   **Schema-First Development with Zod**: Strict validation and type inference are paramount, with Zod schemas serving as the single source of truth for data contracts between frontend and backend, residing in a shared monorepo package.
*   **Layered Architecture with Clear Responsibilities**: A clear separation exists between frontend (Next.js with App Router, React Server/Client Components, React Query, React Context, Tailwind/Shadcn UI) and backend (Nest.js, Prisma). The workflow ensures strict alignment of API contracts and data flow.
*   **Security as an MVP Priority**: Basic yet robust security practices are integrated from the outset, focusing on JWT authentication, server-side token handling via Next.js API proxies for client-side calls, and conditional role-based access control. Advanced security is deferred to later stages.
*   **Pragmatism over Dogma**: While advocating for clear standards (e.g., component function signatures, direct option passing), the workflow encourages adapting to existing codebase patterns. Performance and accessibility are considered with a "simplicity and clarity" mindset, with optimizations and extensive accessibility deferred beyond the MVP.
*   **Iterative Planning and Strict Alignment**: Design is non-technical and UX-focused, followed by detailed technical planning for both frontend and backend. A dedicated technical reviewer ensures rigorous API and type system alignment, presenting clear resolution strategies with an "Implementation Confidence" metric.
*   **Focused Documentation**: Documentation is medium-level, concentrating on project goals, audience, overall technical structure, important folder patterns, and highlighting any "varying from the norm" aspects, rather than deep implementation specifics.
*   **Efficiency and Maintainability**: The emphasis is on building maintainable, scalable solutions by leveraging established frameworks, clear patterns, and robust type safety, aiming for high implementation confidence and efficient problem resolution.

## How to Use This Workflow

The agent-driven workflow typically initiates with the **`feature-planner`** agent. This agent acts as the orchestrator, guiding the development of new features or modifications through a structured, iterative process.

Here's a general overview of the workflow stages:

1.  **Feature Planning (via `feature-planner`)**:
    *   Initiate a new feature request or change with the `feature-planner` agent.
    *   This agent will clarify requirements, define user stories, and outline the high-level scope, incorporating initial security considerations.

2.  **Design Phase (via `designer` and `design-reviewer`)**:
    *   The `designer` agent generates UX/UI wireframes and user flows based on the planned feature, focusing purely on user experience.
    *   The `design-reviewer` agent evaluates these designs against business impact, consistency, and technical feasibility, providing feedback without getting into implementation details.

3.  **Technical Planning (via `web-technical-planner` and `api-technical-planner`)**:
    *   The `web-technical-planner` agent creates a detailed frontend implementation plan for Next.js, including component architecture, data flow (with API proxying), and styling.
    *   The `api-technical-planner` agent develops a comprehensive backend implementation plan for Nest.js, focusing on data models, API endpoints, and business logic, with Zod for validation.

4.  **Technical Review (via `technical-reviewer`)**:
    *   The `technical-reviewer` agent rigorously validates the alignment between the frontend and backend technical plans. It ensures strict API contract matching, consistent Zod schema usage (from `packages/shared`), and secure data flow via the Next.js API proxy.
    *   It identifies blocking issues, integration risks, and optimization opportunities, proposing clear resolution strategies and an "Implementation Confidence" metric.

5.  **Code Implementation (via `nest-engineer` and `next-engineer`)**:
    *   Once technical plans are aligned, the `nest-engineer` and `next-engineer` agents proceed with implementing the backend and frontend features, respectively, following their specific guidelines, codebase standards, and the approved technical plans.

6.  **Documentation & Finalization (via `code-documentation-specialist` and `finalization-agent`)**:
    *   The `code-documentation-specialist` ensures that project context and architectural decisions are well-documented at a medium level of detail.
    *   The `finalization-agent` handles final integration, health checks, type consistency, and pre-deployment validation, ensuring a smooth transition to production.
