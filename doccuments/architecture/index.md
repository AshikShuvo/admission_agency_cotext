# Architecture Documentation Index
## Student Abroad Admission Agency Management System

Use this page as the navigator for all architecture documentation.

## Architecture Documents

| Document | Description |
|---|---|
| [Architecture Overview](architecture_overview.md) | High-level architecture decision, system boundaries, stack, and major tradeoffs. |
| [Module Boundaries](module_boundaries.md) | Backend and frontend module breakdown mapped to business flows. |
| [Data Model](data_model.md) | Entity relationship overview based on business entities. |
| [API Design](api_design.md) | REST API resource groups and request/response expectations at a business level. |
| [Access Control](access_control.md) | Role-based access model, query-level restrictions, and sensitive-data rules. |
| [File Storage and Documents](file_storage_and_documents.md) | Local document storage, upload rules, backups, and document lifecycle. |
| [Deployment and Phases](deployment_and_phases.md) | Local-first deployment plan, later hosting options, and Phase 1/2/3 architecture roadmap. |
| [Testing Strategy](testing_strategy.md) | Frontend Playwright, backend unit/integration testing, test data, and acceptance criteria. |

## Source Business Documents

| Document | Purpose |
|---|---|
| [Business Documentation Index](../business/index.md) | Navigator for all business documentation. |
| [Business Domain Documentation](../business/business_domain_documentation.md) | Full business-domain reference. |
| [Users and Roles](../business/users_and_roles.md) | Role responsibilities, restrictions, and permission matrix. |
| [Phase Goals](../business/phase_goals.md) | Business goals for Phase 1, Phase 2, and Phase 3. |
| [Business Flows Index](../business/flows/00_business_flows_index.md) | Workflow-level view of the business process. |

## Recommended Reading Path

1. Start with [Business Documentation Index](../business/index.md) to understand the business context.
2. Read [Architecture Overview](architecture_overview.md) for the core architecture decision.
3. Read [Module Boundaries](module_boundaries.md) to understand ownership of each business flow.
4. Read [Data Model](data_model.md), [API Design](api_design.md), and [Access Control](access_control.md) before implementation.
5. Read [File Storage and Documents](file_storage_and_documents.md) before building uploads or document review.
6. Read [Testing Strategy](testing_strategy.md) before implementing Phase 1 workflows.
7. Read [Deployment and Phases](deployment_and_phases.md) before setting up local deployment or planning future hosting.

## Locked Architecture Decisions

- Phase 1 uses a modular monolith, not microservices.
- The stack is Next.js, NestJS, TypeScript, Prisma, and PostgreSQL.
- APIs are REST APIs.
- The codebase should be organized as a monorepo.
- Authentication uses self-managed JWT in Phase 1.
- Phase 1 starts on localhost/local deployment.
- Uploaded documents are stored on server disk with backup rules in Phase 1.
- Phase 1 uses in-app notifications only.
- Student portal, SMS/email automation, public catalog, mobile app, and multi-branch support are out of Phase 1.
