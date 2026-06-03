# Data Model
## Student Abroad Admission Agency Management System

This document describes the architecture-level data model. It is an entity overview, not a full database schema.

Source documents:

- [Business Domain Documentation](../business/business_domain_documentation.md)
- [Module Boundaries](module_boundaries.md)

## Data Model Principles

- Use PostgreSQL as the source of truth.
- Use Prisma for schema definition, migrations, and typed database access.
- Use UUID primary keys for main records.
- Keep monetary values as decimal types, not floating point.
- Preserve audit history for sensitive actions.
- Do not physically delete business records that affect history; use inactive/cancelled statuses where appropriate.

## Core Relationships

```text
Country
  └── University
        └── Program
              └── Package
                    └── PackageFeeLineItem

Student
  └── File
        ├── FileFee
        ├── Payment
        ├── Document
        ├── AdmissionRecord
        ├── VisaRecord
        ├── Commission
        └── FileActivityLog

User
  ├── assigned Files as Consultant
  ├── recorded Payments
  ├── confirmed Payments
  ├── uploaded/reviewed Documents
  └── performed Audit Actions
```

## Main Entities

| Entity | Purpose | Owning Module |
|---|---|---|
| User | Internal staff account with one primary role. | Auth and Users |
| Student | Student personal, guardian, academic, and passport information. | Students |
| Country | Destination country supported by the agency. | Catalog |
| University | Partner university under a country. | Catalog |
| Program | Academic program under a university. | Catalog |
| Package | Active or historical fee package for a program. | Catalog |
| PackageFeeLineItem | Stage-wise package fees grouped by File Opening, Admission, Visa. | Catalog |
| File | Central case record for a student's admission journey. | Files / Cases |
| FileFee | Snapshot fee record copied from package to file; may include Owner-approved custom changes. | File Fees |
| Payment | Student payment record, confirmation status, method, and reference. | Payments |
| Document | Uploaded admission or visa document metadata and storage path. | Documents |
| AdmissionRecord | Admission checklist, submission, offer letter, and approval state. | Admission |
| VisaRecord | Visa checklist, submission, outcome, rejection/reapplication state. | Visa |
| Commission | Owner-only university commission record linked to a file and university. | Commissions |
| Notification | In-app notification and read/unread status. | Notifications |
| FileActivityLog | Audit-oriented lifecycle and action history for a file. | Audit Log |

## Package Snapshot Model

When a formal file is created:

1. The selected program must have an active package.
2. The active package line items are copied into file fee records.
3. File fees become the pricing source for that file.
4. Future package changes do not alter existing file fees.

Custom fee changes:

- Must be Owner-approved.
- Must update the file fee records, not the package template.
- Must record reason, old amount, new amount, approver, and timestamp in the audit log.

## Status and Stage Model

The File entity owns the overall lifecycle status:

- `FILE_OPENED`
- `PENDING_PAYMENT_FILE_OPENING`
- `ADMISSION_IN_PROGRESS`
- `PENDING_PAYMENT_ADMISSION`
- `DOCUMENTS_PENDING`
- `APPLICATION_SUBMITTED`
- `OFFER_LETTER_RECEIVED`
- `ADMISSION_APPROVED`
- `VISA_IN_PROGRESS`
- `PENDING_PAYMENT_VISA`
- `VISA_APPLIED`
- `VISA_APPROVED`
- `VISA_REJECTED`
- `COMPLETED`
- `ON_HOLD`
- `CANCELLED`

Admission and Visa modules can keep their own stage records for checklists, submissions, and outcomes, but the File status remains the single source for the overall lifecycle.

## Payment and Due Model

Payments are recorded by stage:

- `FILE_OPENING`
- `ADMISSION`
- `VISA`
- `OTHER`

Due calculation:

```text
Due Amount per Stage = Sum(FileFee for Stage) - Sum(Confirmed Payment for Stage)
```

Rules:

- Unconfirmed payments do not reduce due.
- Partial payments are allowed.
- A stage is financially cleared only when due is zero.
- Phase 1 has no payment-gate override.

## Document Model

Documents belong to a file and a stage:

- `ADMISSION`
- `VISA`

Document status:

- `PENDING`
- `SUBMITTED`
- `VERIFIED`
- `REJECTED`

Document records store metadata and storage path. File binary content is stored on server disk, not inside PostgreSQL.

## Sensitive Data Boundaries

| Data | Visibility |
|---|---|
| Commission records | Owner only |
| Payment records and dues | Owner and Accounts |
| Admission documents | Owner, Admission, assigned Consultant |
| Visa documents | Owner, Visa, assigned Consultant |
| Consultant-owned file list | Owner and assigned Consultant |
| Reports | Owner, with limited financial reports for Accounts |

## Future Data Extensions

Phase 2 and Phase 3 may add:

- Student portal account
- Student communication history
- Referral/source tracking
- Document expiry alerts
- Branch entity
- Public catalog visibility flags
- Advanced analytics snapshots
