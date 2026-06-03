# Architecture Overview
## Student Abroad Admission Agency Management System

This document describes the high-level architecture for the admission agency software.

Source documents:

- [Business Domain Documentation](../business/business_domain_documentation.md)
- [Phase Goals](../business/phase_goals.md)
- [Users and Roles](../business/users_and_roles.md)
- [Business Flows Index](../business/flows/00_business_flows_index.md)

## Architecture Decision

Phase 1 should be built as a **modular monolith**.

This business has multiple departments and strict workflow rules, but all modules operate around the same central student file lifecycle. Splitting this into microservices at the beginning would add deployment, data consistency, and coordination cost without solving a real Phase 1 business problem.

The monolith must still be modular. Each business capability should have clear boundaries so future extraction is possible if the agency grows into multiple branches, countries, or independent teams.

## Primary Stack

| Layer | Decision |
|---|---|
| Frontend | Next.js + TypeScript |
| Backend | NestJS + TypeScript |
| API Style | REST |
| Database | PostgreSQL |
| ORM | Prisma |
| Authentication | Self-managed JWT |
| File Storage | Server disk with backup rules |
| Notifications | In-app only in Phase 1 |
| Repository | Monorepo |
| Initial Runtime | Localhost/local deployment |

## System Boundary

The system is an internal staff application for Phase 1.

Internal users:

- Owner / Admin
- Consultant / Counsellor
- Accounts Department User
- Admission Department User
- Visa Department User

External actors:

- Student
- University
- Embassy or immigration authority

Students and universities do not log into the system in Phase 1. Staff record student, university, payment, document, and status information internally.

## High-Level Component View

```text
┌─────────────────────────────────────────────────────────────┐
│                        Next.js Web App                       │
│                                                             │
│  Role Dashboards | File Workspace | Payments | Documents    │
│  Catalog Admin   | Reports        | Notifications           │
└──────────────────────────────┬──────────────────────────────┘
                               │ REST + JWT
┌──────────────────────────────▼──────────────────────────────┐
│                       NestJS API Server                      │
│                                                             │
│ Auth | Users | Catalog | Files | Fees | Payments | Docs     │
│ Admission | Visa | Commissions | Reports | Audit | Admin    │
└───────────────┬──────────────────────────────┬──────────────┘
                │                              │
┌───────────────▼──────────────┐   ┌──────────▼───────────────┐
│         PostgreSQL            │   │   Local Document Storage  │
│ Business records, statuses,   │   │ Uploaded admission/visa   │
│ payments, audit, reports      │   │ files stored on disk      │
└───────────────────────────────┘   └──────────────────────────┘
```

## Phase 1 Scope

Phase 1 must support the complete internal student file lifecycle:

1. Catalog and package setup
2. Counselling and program selection
3. File opening
4. Payment and deposit confirmation
5. Admission processing
6. Visa processing
7. University commission tracking
8. Basic dashboards and reports
9. Access control
10. Exception and file closure handling

Phase 1 does not include:

- Student portal
- SMS/email automation
- Public program catalog
- Mobile app
- Multi-branch operation
- Advanced analytics

## Key Business Rules Reflected In Architecture

- A formal file requires a selected program with an active package.
- Package fees are snapshot-copied onto a file at file creation.
- Custom fee changes are Owner-approved only and must be audited.
- Phase 1 has no payment-gate override.
- Consultants can only access assigned files.
- Accounts can access payment and due information but not document content.
- Admission and Visa users only access their stage-relevant operational data.
- Commission data is Owner-only.
- Completed and cancelled files are immutable unless Owner-authorized.
- Visa rejection stays on the same file and preserves previous history.

## Major Tradeoffs

| Decision | Benefit | Tradeoff |
|---|---|---|
| Modular monolith | Fastest reliable path for Phase 1 | Requires discipline to maintain module boundaries |
| Local-first deployment | Lowest early infrastructure cost | Backups, disk storage, and security must be handled explicitly |
| Self-managed JWT | Simple for internal staff auth | More responsibility for password, token, and session security |
| Server disk document storage | Simple and cost-effective early | Later migration may be needed for cloud/object storage |
| In-app notifications only | Avoids provider cost and setup | Students do not receive automated external updates in Phase 1 |

## Future Architecture Direction

The system should be designed so Phase 2 and Phase 3 can add:

- Email/SMS notifications
- Student portal
- Public program catalog
- Cloud or VPS deployment
- Object storage for documents
- Multi-country and multi-branch support
- Advanced analytics

These should be extensions of the modular monolith first. Microservices should only be reconsidered if the agency has clear independent scaling, separate engineering teams, or separate deployment needs.
