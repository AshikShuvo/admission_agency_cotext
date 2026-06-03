# Access Control
## Student Abroad Admission Agency Management System

This document describes role-based access control and sensitive-data visibility.

Source documents:

- [Users and Roles](../business/users_and_roles.md)
- [Business Domain Documentation](../business/business_domain_documentation.md)
- [API Design](api_design.md)

## Access Control Decision

Phase 1 uses role-based access control with one primary role per internal user.

Roles:

- `OWNER`
- `CONSULTANT`
- `ACCOUNTS`
- `ADMISSION`
- `VISA`

Students and universities are external actors in Phase 1 and do not have system login accounts.

## Enforcement Principle

Access rules must be enforced at the backend service/query layer.

Frontend route hiding is useful for user experience, but it is not a security boundary. Every list, detail, report, mutation, and file/document endpoint must apply backend authorization.

## Role Scope

| Role | Scope |
|---|---|
| Owner | Full unrestricted business access, including commissions, reports, users, catalog, documents, payments, and overrides authorized by business rules. |
| Consultant | Assigned files only, catalog browsing, own file status, own file documents where allowed. |
| Accounts | Payment, due, and confirmation data for all files, with limited file/student identifiers. |
| Admission | Admission-stage operational data, admission documents, academic/program details, and admission approvals. |
| Visa | Visa-stage operational data, visa documents, passport/offer letter information, and visa outcomes. |

## Sensitive Data Rules

| Data | Allowed Roles | Rule |
|---|---|---|
| Commission amount and records | Owner | Never return in non-owner responses. |
| Full payment history | Owner, Accounts | Consultants, Admission, and Visa only receive clearance status where needed. |
| Consultant file list | Owner, assigned Consultant | Consultant query filters must include consultant assignment. |
| Admission documents | Owner, Admission, assigned Consultant | Accounts and Visa cannot view admission document content. |
| Visa documents | Owner, Visa, assigned Consultant | Accounts and Admission cannot view visa document content. |
| Catalog management | Owner | Consultants can browse active catalog only. |
| User management | Owner | Other roles cannot create or deactivate staff users. |
| Reports | Owner, limited Accounts, own Consultant dashboard | Report queries must apply role filters. |

## Consultant Isolation

Consultant isolation is a core rule:

- Consultants cannot see other consultants' files.
- Consultant file lists must filter by `consultant_id = current_user.id`.
- Consultant detail endpoints must reject files not assigned to the current consultant.
- Consultant reports must use only assigned files.

## Department Access

Accounts:

- Can access payment records, dues, confirmations, and limited identifiers.
- Cannot access document content.
- Cannot access commission data.
- Cannot approve admission or visa stages.

Admission:

- Can access admission work queue and admission-stage documents.
- Can see program and student academic details needed for university application.
- Can see admission payment clearance status.
- Cannot confirm payments.
- Cannot access commission data.
- Cannot access visa-only documents.

Visa:

- Can access visa work queue and visa-stage documents.
- Can see passport information and offer letter information needed for visa processing.
- Can see visa payment clearance status.
- Cannot confirm payments.
- Cannot access commission data.
- Cannot approve admission.

## Owner Access

Owner can access all business data.

Owner-only actions include:

- Manage users.
- Manage catalog.
- View and enter commissions.
- View full reports.
- Approve custom fee changes.
- Authorize changes to completed or cancelled files if the business allows it.

All owner-sensitive actions must be audit logged.

## Authentication

Phase 1 uses self-managed JWT authentication:

- Login returns an access token.
- Token contains user identity and role claims.
- Backend loads current user and validates active status before processing protected requests.
- Password hashes must be stored securely.
- Tokens must not contain sensitive business data.

## Audit Logging

Audit logs should record:

- Actor
- Action
- Target record
- Timestamp
- Previous value and new value where relevant
- Reason when required

Required audit events:

- Payment confirmation
- Custom fee change
- Document upload/review/rejection
- Stage approval
- File status change
- Consultant assignment change
- Commission entry
- Owner-authorized edit to completed/cancelled file

## Access Testing Expectations

Access tests should verify:

- Consultant cannot list or open another consultant's file.
- Accounts cannot fetch document content.
- Admission cannot view commission data.
- Visa cannot view admission-only document content.
- Non-owner cannot manage catalog records.
- Non-owner cannot access commission endpoints.
- Reports return role-scoped data only.
