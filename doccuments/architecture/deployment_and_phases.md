# Deployment and Phases
## Student Abroad Admission Agency Management System

This document describes the local-first deployment approach and how architecture should evolve across phases.

Source documents:

- [Phase Goals](../business/phase_goals.md)
- [Architecture Overview](architecture_overview.md)
- [File Storage and Documents](file_storage_and_documents.md)

## Phase 1 Runtime Decision

Phase 1 starts with localhost/local deployment.

The architecture should support:

- Local development on a developer machine.
- Local demo/testing on one machine.
- Later cost-effective deployment without redesigning the app.

No production cloud provider is locked for Phase 1.

## Local Development Setup

Recommended local components:

```text
Next.js web app
NestJS API server
PostgreSQL database
Local document storage folder
```

Recommended local orchestration:

- Use Docker Compose for PostgreSQL and optional local services.
- Run Next.js and NestJS locally during development.
- Use environment variables for database URL, JWT secret, upload path, and application URLs.

## Local Deployment Setup

For a local office or local machine deployment:

```text
Browser
  -> Next.js app
  -> NestJS API
  -> PostgreSQL
  -> Local document storage
```

Required operational practices before real business use:

- Database backup process.
- Document folder backup process.
- Password and JWT secret management.
- Admin account creation process.
- Restore test.
- Basic machine security.

## Later Hosting Options

The future deployment should be selected based on cost-effectiveness and operational need.

| Option | When To Use | Notes |
|---|---|---|
| Single VPS | Low-cost first online deployment | Requires server maintenance, backups, HTTPS, firewall setup. |
| Managed database + VPS app | Better reliability with moderate cost | Keeps app hosting simple while improving database safety. |
| Cloud managed platform | When uptime, scale, and managed services justify cost | Can add object storage, managed DB, monitoring, and autoscaling. |
| Local office server | Only if internet deployment is intentionally avoided | Highest local maintenance and backup responsibility. |

AWS is not mandatory. The architecture should allow AWS, a VPS, or another cost-effective provider later.

## Phase 1 Architecture Scope

Phase 1 goal: run the complete core operation.

Architecture must include:

- Modular monolith backend.
- Monorepo with web and API apps.
- PostgreSQL database.
- Prisma data access.
- REST APIs.
- Self-managed JWT auth.
- Local document storage.
- In-app notifications.
- Role-based dashboards.
- Audit logs.
- Basic reports.

Phase 1 excludes:

- Student portal.
- SMS/email automation.
- Public program catalog.
- Mobile app.
- Multi-branch support.
- Advanced analytics.
- Microservices.

## Phase 2 Architecture Evolution

Phase 2 goal: improve efficiency and communication.

Expected additions:

- Stronger in-app notification workflow.
- Optional email/SMS integration if business confirms it.
- Document expiry alerts.
- Package PDF/quotation generation.
- Referral/source tracking if approved.
- Better dashboards for pending tasks and staff follow-up.

Architecture preparation:

- Keep Notifications module provider-agnostic.
- Keep document metadata flexible enough for expiry dates.
- Keep reporting queries separated from core write workflows.
- Keep package summary generation reusable for PDF or public catalog use.

## Phase 3 Architecture Evolution

Phase 3 goal: support scale and business growth.

Expected additions:

- Multi-country expansion.
- Multi-branch support.
- Public program catalog.
- Student portal.
- Advanced analytics.
- Possible mobile access.

Architecture preparation:

- Keep Country and Branch concepts separate when Branch is added.
- Add branch-level access rules before multi-branch rollout.
- Consider object storage migration for documents.
- Consider managed database hosting for reliability.
- Consider analytics tables or materialized reporting views.
- Reassess microservices only if independent teams, scale, or deployment needs exist.

## Deployment Readiness Checklist

Before any real production deployment:

- Confirm hosting target.
- Configure HTTPS.
- Configure database backups.
- Configure document backups.
- Configure environment secrets.
- Create initial Owner account.
- Test restore from backup.
- Test role access rules.
- Test file upload and download.
- Test payment-gate rules.
- Run backend unit and integration tests.
- Run frontend Playwright workflow tests.
- Test audit logging for sensitive actions.

## Migration Path From Local To Hosted

When moving from local to hosted:

1. Export PostgreSQL database.
2. Copy document storage folder.
3. Deploy API and web app.
4. Configure hosted environment variables.
5. Restore database.
6. Restore document files.
7. Verify document paths.
8. Verify login and role access.
9. Verify file lifecycle workflow.
10. Run backup and restore test on hosted environment.
