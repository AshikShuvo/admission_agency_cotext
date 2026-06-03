# API Design
## Student Abroad Admission Agency Management System

This document describes the REST API resource groups at a business level. It does not define final DTO code.

Source documents:

- [Module Boundaries](module_boundaries.md)
- [Access Control](access_control.md)
- [Business Flows Index](../business/flows/00_business_flows_index.md)

## API Principles

- Use REST APIs for Phase 1.
- Use JWT authentication for internal staff users.
- Enforce authorization in backend services and database queries.
- Do not rely on frontend route hiding for security.
- Return role-appropriate data shapes.
- Record audit logs for sensitive mutations.
- Use consistent pagination, filtering, and date-range query conventions for list/report endpoints.

## Resource Groups

| Resource Group | Purpose |
|---|---|
| `/auth` | Login, logout/session invalidation strategy, token refresh if used, current user profile. |
| `/users` | Owner-managed staff users, roles, active/inactive status. |
| `/catalog/countries` | Country CRUD and activation status. |
| `/catalog/universities` | University CRUD, country relationship, Owner-only commission defaults. |
| `/catalog/programs` | Program CRUD and consultant browsing filters. |
| `/catalog/packages` | Package CRUD, active package rules, package line items, package summary. |
| `/students` | Student profile creation and updates. |
| `/files` | File creation, assignment, status, lifecycle actions, own/all file lists based on role. |
| `/files/:id/fees` | File fee snapshot, stage totals, Owner-approved custom fee changes. |
| `/files/:id/payments` | Payment entry, confirmation, stage dues, payment history. |
| `/files/:id/documents` | Document metadata, upload registration, status changes, review notes. |
| `/admission/files` | Admission work queue, checklist, submission, offer letter, admission approval. |
| `/visa/files` | Visa work queue, checklist, submission, outcome, completion/rejection handling. |
| `/commissions` | Owner-only commission entry and commission reporting input. |
| `/notifications` | In-app notification list, read/unread state. |
| `/reports` | Dashboards and operational/financial reports. |
| `/audit-logs` | Owner-visible audit history and file activity logs. |

## Required API Behaviors

### Auth

- Login returns JWT and user role.
- Current-user endpoint returns role and allowed profile information.
- Inactive users cannot log in.
- Password handling must be backend-owned and never expose password hashes.

### Catalog

- Only Owner can mutate catalog records.
- Consultants can browse active catalog data.
- Only one package can be active per program.
- Programs without active packages cannot be used for formal file creation.

### Files

- File creation requires student, consultant, university, program, and active package.
- File number must be unique and human-readable.
- File creation must snapshot active package line items into file fees.
- Consultants can list and view only assigned files.
- Completed and cancelled files cannot be normally edited.

### File Fees

- File fees are the pricing source after file creation.
- Owner-approved custom fee changes must require reason and audit logging.
- Custom fee changes must not mutate package templates.

### Payments

- Accounts and Owner can record payments.
- Accounts and Owner can confirm deposits.
- Unconfirmed payments do not reduce due.
- Stage due is calculated from file fees and confirmed payments.
- Phase 1 does not allow payment-gate override.

### Documents

- Document APIs store metadata and link to local file storage.
- Document visibility depends on stage and role.
- Every document upload, verification, rejection, and review note must be auditable.

### Admission

- Admission work queue shows files ready for admission processing.
- Admission approval requires completed required documents and cleared admission-stage payment.
- Offer letter upload is part of admission processing.

### Visa

- Visa work queue shows files ready for visa processing.
- Visa approval/completion requires completed required documents and cleared visa-stage payment.
- Visa rejection records reason and preserves the same file history.

### Commissions

- Only Owner can access commission endpoints.
- Commission records link to file and university.
- Commission data must not appear in non-owner responses.

### Reports

- Owner can access all reports.
- Accounts can access payment, dues, and limited revenue reports.
- Consultants can access only own-file dashboard data.
- Reports must respect the same backend access rules as normal resource endpoints.

## API Response Scope By Role

| Role | API Data Scope |
|---|---|
| Owner | Full data, including commissions and reports. |
| Consultant | Assigned files, student details for assigned files, allowed document/status information, catalog browsing. |
| Accounts | Payment and due data for all files, with limited identifying file/student information. |
| Admission | Admission queue, admission documents, academic/program details, admission clearance status. |
| Visa | Visa queue, visa documents, passport/offer letter information, visa clearance status. |

## Error and Audit Expectations

APIs should return clear business errors for:

- Missing active package during file creation.
- Unauthorized role access.
- Attempted access to another consultant's file.
- Stage approval attempted with unpaid dues.
- Stage approval attempted with incomplete required documents.
- Attempted modification of completed or cancelled file.
- Attempted commission access by non-owner.

Sensitive mutations should create audit entries:

- Login failure lockout events if implemented
- File creation
- Assignment change
- Payment recording and confirmation
- Fee customization
- Document status change
- Admission approval
- Visa outcome
- File hold/cancel/complete
- Commission entry
