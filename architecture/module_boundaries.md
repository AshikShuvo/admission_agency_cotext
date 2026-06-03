# Module Boundaries
## Student Abroad Admission Agency Management System

This document maps business flows to backend modules and frontend workspaces.

Source documents:

- [Business Flows Index](../business/flows/00_business_flows_index.md)
- [Users and Roles](../business/users_and_roles.md)
- [Architecture Overview](architecture_overview.md)

## Backend Module Principles

- Name modules after business capabilities, not database tables.
- Keep workflow rules in the backend, not only in the frontend.
- Enforce role access at the service/query layer.
- Keep shared utilities small and avoid circular dependencies.
- Use audit logging for approvals, status changes, document actions, custom fee changes, and payment confirmation.

## Backend Modules

| Module | Responsibility |
|---|---|
| Auth and Users | Login, JWT issuance, password handling, user profile, active/inactive staff status, role assignment. |
| Catalog | Countries, universities, programs, packages, package line items, active package rules, package summary views. |
| Students | Student personal information, guardian details, academic background, passport metadata. |
| Files / Cases | Central student file, file number, assigned consultant, status lifecycle, stage transitions, hold/cancel/complete handling. |
| File Fees | Package snapshot, file-specific fee records, Owner-approved custom fee changes, stage totals. |
| Payments | Payment recording, deposit confirmation, partial payment tracking, due calculation, financial clearance. |
| Documents | Document metadata, upload records, document status, checklist items, review notes, local storage references. |
| Admission | Admission checklist, document review, university application submission, offer letter, admission approval. |
| Visa | Visa checklist, visa document review, visa application submission, visa outcome, rejection/reapplication history. |
| Commissions | Owner-only university commission records and commission reports. |
| Notifications | In-app notifications for file events, payment confirmation, document requests, stage movement, visa outcome. |
| Reporting | Owner, consultant, and accounts dashboards; revenue, dues, consultant performance, file status reports. |
| Audit Log | Immutable action history for sensitive operations and lifecycle events. |
| Settings / Admin | System configuration controlled by Owner, including future numbering and business settings. |

## Flow Ownership

| Business Flow | Primary Owning Module | Supporting Modules |
|---|---|---|
| Catalog and Package Setup | Catalog | Auth and Users, Audit Log |
| Counselling and Program Selection | Catalog | Students, Files / Cases |
| File Opening | Files / Cases | Students, Catalog, File Fees, Payments, Audit Log |
| Payment and Deposit Confirmation | Payments | File Fees, Files / Cases, Notifications, Audit Log |
| Admission Processing | Admission | Documents, Payments, Files / Cases, Notifications, Audit Log |
| Visa Processing | Visa | Documents, Payments, Files / Cases, Notifications, Audit Log |
| University Commission Tracking | Commissions | Files / Cases, Catalog, Reporting, Audit Log |
| Reporting and Dashboard | Reporting | Files / Cases, Payments, Commissions, Documents |
| Notifications and Communication | Notifications | Files / Cases, Payments, Admission, Visa, Documents |
| Access Control and Role Visibility | Auth and Users | All modules |
| Exception and File Closure Handling | Files / Cases | Visa, Payments, Documents, Audit Log |

## Backend Dependency Direction

Recommended dependency direction:

```text
Auth and Users
  -> all modules for current-user and role context

Catalog
  -> Files / Cases
  -> File Fees

Files / Cases
  -> Payments
  -> Admission
  -> Visa
  -> Commissions
  -> Reporting

Documents
  -> Admission
  -> Visa

Audit Log and Notifications
  <- called by business modules after important actions
```

Rules:

- Payments should not approve admission or visa directly; it should expose financial clearance used by Files, Admission, and Visa.
- Admission and Visa should not calculate dues themselves; they should consume clearance from Payments/File Fees.
- Reporting should be read-oriented and should not mutate core business records.
- Audit Log should not contain business decision logic.

## Frontend Workspaces

| Area | Primary Users | Purpose |
|---|---|---|
| Auth Screens | All internal users | Login and password/session handling. |
| Role-Based Dashboard | All internal users | Show the user's allowed summary, tasks, and notifications. |
| Catalog Management | Owner | Manage countries, universities, programs, packages, and active package rules. |
| Consultant File Workspace | Consultant, Owner | Counselling support, file opening, own file tracking, document follow-up. |
| Accounts Payment Workspace | Accounts, Owner | Payment entry, deposit confirmation, dues, financial clearance. |
| Admission Workspace | Admission, Owner | Admission checklist, document review, application submission, offer letter, approval. |
| Visa Workspace | Visa, Owner | Visa checklist, document review, application submission, outcome, completion/rejection. |
| Owner Reports and Settings | Owner | Full reports, commissions, user management, system settings. |

## Monorepo Shape

Recommended repository structure:

```text
apps/
├── web/                    # Next.js frontend
└── api/                    # NestJS backend
packages/
├── config/                 # Shared lint, TypeScript, formatting config
├── types/                  # Shared API/domain types when useful
└── ui/                     # Shared UI components if the project grows
infra/
├── docker/                 # Local Docker setup
└── deployment-notes/       # Future VPS/cloud deployment notes
```

Phase 1 can keep `packages/ui` minimal or omit it until reusable UI components justify it.
