# File Storage and Documents
## Student Abroad Admission Agency Management System

This document describes Phase 1 document upload, local storage, backup expectations, and document lifecycle.

Source documents:

- [Business Domain Documentation](../business/business_domain_documentation.md)
- [Admission Processing Flow](../business/flows/05_admission_processing_flow.md)
- [Visa Processing Flow](../business/flows/06_visa_processing_flow.md)
- [Access Control](access_control.md)

## Storage Decision

Phase 1 stores uploaded documents on the server disk with explicit backup rules.

PostgreSQL stores document metadata only:

- File reference
- Stage
- Document type
- Upload user
- Upload timestamp
- Storage path
- Status
- Review notes

Binary files should not be stored in PostgreSQL in Phase 1.

## Local Storage Layout

Recommended storage layout:

```text
storage/
└── documents/
    └── files/
        └── <file-number-or-file-id>/
            ├── admission/
            │   └── <document-id>.<extension>
            └── visa/
                └── <document-id>.<extension>
```

Use document IDs in stored filenames to avoid collisions and avoid exposing original filenames as the storage identity.

## Upload Rules

- Only authenticated internal users can upload documents.
- Upload permission depends on file assignment and department role.
- Consultant can upload documents for assigned files.
- Admission can upload/review admission-stage documents.
- Visa can upload/review visa-stage documents.
- Owner can upload/review all documents.
- Accounts cannot upload or view document content unless a future business rule explicitly adds this.

## Document Lifecycle

Document status values:

- `PENDING`
- `SUBMITTED`
- `VERIFIED`
- `REJECTED`

Typical lifecycle:

```text
Document Requested
  -> Submitted
  -> Verified
  -> Used for Application/Approval
```

Correction lifecycle:

```text
Document Requested
  -> Submitted
  -> Rejected with Reason
  -> Resubmitted
  -> Verified
```

## Admission Documents

Admission documents may include:

- Academic certificates
- Transcripts
- English language score
- NID or birth certificate
- Photographs
- Passport if available or required
- Offer letter after university acceptance

Admission document content is visible to:

- Owner
- Admission Department
- Assigned Consultant

## Visa Documents

Visa documents may include:

- Passport
- University acceptance letter
- Financial statements
- Medical certificate
- Police clearance
- Photographs
- Visa application form

Visa document content is visible to:

- Owner
- Visa Department
- Assigned Consultant

## Backup Expectations

Because Phase 1 uses local disk storage, backups are mandatory.

Minimum backup expectations:

- Back up PostgreSQL database and document storage together.
- Keep backup timing aligned so database records and files match.
- Store at least one backup outside the application server.
- Document restore steps before production use.
- Periodically test restoring a backup.

Recommended local-first backup plan:

```text
Daily:
  - PostgreSQL dump
  - documents folder archive or sync

Weekly:
  - full backup copied to external drive or low-cost cloud storage

Monthly:
  - restore test on separate machine or folder
```

## Security Expectations

- Do not serve files from a public static folder.
- File downloads must go through authenticated backend endpoints.
- Backend must verify role and file access before returning a file.
- Store only safe normalized paths in the database.
- Validate allowed file types and size limits during upload.
- Keep original filename as metadata only if useful for staff display.

## Future Migration Path

When the agency deploys beyond local hosting, documents can move from server disk to object storage.

The architecture should keep document storage behind a service abstraction so future migration can change the storage implementation without changing Admission, Visa, or File modules.

Future options:

- VPS disk with automated offsite backup
- S3-compatible object storage
- AWS S3
- Cloudflare R2
- Backblaze B2

The lowest-cost reliable option should be selected during deployment planning.
