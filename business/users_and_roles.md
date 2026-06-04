# Users and Roles
## Student Abroad Admission Agency Management System

This document describes the users involved in the business, their responsibilities, their access scope, and their role in the student admission workflow.

Source document: [Business Domain Documentation](business_domain_documentation.md)

## User Role Summary

| Role | Business Purpose | Main System Scope |
|---|---|---|
| Owner / Admin | Runs and oversees the agency | Full access to all data, users, catalog, reports, and commissions |
| Consultant / Counsellor | Handles student counselling and file creation | Own assigned student files and catalog browsing |
| Accounts Department User | Manages payments and deposit confirmation | Financial records, dues, payment confirmations, limited reports |
| Admission Department User | Handles university admission processing | Admission documents, application submission, admission approval |
| Visa Department User | Handles visa processing | Visa documents, visa submission, visa outcome, visa approval |
| Student | Receives counselling and submits payment/documents | External actor; not a system user in Phase 1 unless student portal is added later |
| University | Receives applications and pays commissions | External actor; not a direct system user |

## 1. Owner / Admin

### Business Role

The Owner / Admin is the highest authority in the business. This role manages the agency setup, monitors operations, controls confidential financial information, and makes final business decisions.

### Responsibilities

- Manage users and staff access.
- Configure countries, universities, programs, and program packages.
- View all student files across all consultants and departments.
- Monitor company-wide operations.
- View all financial information.
- Track revenue from student payments.
- Enter and view university commission records.
- Review reports by date, consultant, university, status, and revenue category.
- Authorize special actions such as overriding restricted edits, if the business allows it.

### Access Scope

- All student files
- All student information
- All financial records
- All payment and due records
- All admission and visa documents
- All reports
- All commission data
- User management
- Catalog and package management

### Restrictions

- No functional restriction by default.
- Any owner override should be logged for audit purposes.

## 2. Consultant / Counsellor

### Business Role

The Consultant is the main student-facing employee. This role guides students, helps them choose programs, creates student files, collects documents from students, and follows up throughout the process.

### Responsibilities

- Counsel students about available countries, universities, and programs.
- Browse the program catalog and package summaries.
- Explain stage-wise package costs to students.
- Create files for students who decide to proceed.
- Record student personal and academic information.
- Collect admission and visa documents from students.
- Upload or submit documents requested by Admission or Visa departments.
- Track the status of assigned files.
- Follow up with students when documents or payments are pending.

### Access Scope

- Own assigned student files only
- Student profile details for own files
- Program catalog browsing
- Package fee breakdown during counselling
- Admission document status for own files
- Visa document status for own files
- Notifications related to own files

### Restrictions

- Cannot view other consultants' files.
- Cannot confirm payments.
- Cannot view company-wide financial summaries.
- Cannot view university commission data.
- Cannot manage users.
- Cannot create, edit, or deactivate countries, universities, programs, or packages.

## 3. Accounts Department User

### Business Role

The Accounts user manages money-related operations. This role records payments, confirms deposits, calculates dues, and provides financial clearance for each processing stage.

### Responsibilities

- Record student payments.
- Verify deposits through cash, bank transfer, mobile banking, or other accepted methods.
- Confirm payments in the system.
- Track partial payments.
- Monitor outstanding dues by file and stage.
- Provide payment clearance before a file can move forward.
- View financial reports available to Accounts.

### Access Scope

- Payment records for all files
- Due amounts for all files
- Deposit confirmation history
- File number and student name for payment reference
- Stage-wise financial clearance status
- Limited revenue reports
- Package fee breakdown only when linked to a specific file

### Restrictions

- Cannot view document content.
- Cannot view detailed admission or visa processing information beyond financial context.
- Cannot approve admission or visa stages.
- Cannot view or enter university commission data.
- Cannot manage catalog or user records.

## 4. Admission Department User

### Business Role

The Admission user handles the university application stage after the file-opening payment has been confirmed.

### Responsibilities

- Review files that are ready for admission processing.
- Generate admission document checklists.
- Request documents from the assigned consultant.
- Verify admission documents.
- Ask for corrections or missing documents when needed.
- Submit applications to universities.
- Record university application submission date.
- Upload offer letters or acceptance letters.
- Approve the admission stage and move the file to visa processing.

### Access Scope

- Admission-stage files
- Admission document checklist
- Admission documents
- Student academic information
- Selected university and program details
- Admission payment clearance status
- Offer letter upload and status

### Restrictions

- Cannot view commission data.
- Cannot confirm payments.
- Cannot view full financial records.
- Cannot view visa-specific documents unless needed as part of admission handoff.
- Cannot manage users or catalog records.

## 5. Visa Department User

### Business Role

The Visa user handles the visa processing stage after admission is approved and the student receives an offer letter.

### Responsibilities

- Review files that have moved to visa processing.
- Generate visa document checklists.
- Request visa documents from the consultant or student.
- Verify visa documents.
- Track visa-stage payment clearance.
- Submit visa applications to embassy or immigration authority.
- Record visa submission details.
- Record visa outcome.
- Mark visa approved, rejected, or completed.
- Support file completion after student departure.

### Access Scope

- Visa-stage files
- Visa document checklist
- Visa documents
- Passport and offer letter information
- Visa payment clearance status
- Visa application submission details
- Visa outcome details

### Restrictions

- Cannot view university commission data.
- Cannot confirm payments.
- Cannot view full financial records.
- Cannot approve admission stage.
- Cannot manage users or catalog records.

## 6. Student

### Business Role

The Student is the customer of the agency. The student receives counselling, selects a program, pays fees, submits documents, and eventually travels for study if the process succeeds.

### Responsibilities

- Provide accurate personal and academic information.
- Choose a target program and university.
- Pay required fees at each stage.
- Submit required admission and visa documents.
- Respond to document correction requests.
- Attend visa or embassy-related steps when required.

### Access Scope

In Phase 1, the student is treated as an external actor and does not need direct system access.

Future enhancement may include a read-only student portal where students can view:

- File status
- Payment receipts
- Pending document requests
- Offer letter and visa outcome notifications

## 7. University

### Business Role

The University is an external partner institution. It receives applications, issues admission decisions, and pays commission to the agency after successful enrollment.

### Responsibilities

- Provide program and admission information.
- Receive student applications.
- Review applications.
- Issue offer letters or acceptance letters.
- Confirm student enrollment.
- Pay commission to the agency, where applicable.

### Access Scope

The university is not a direct system user in the current scope. University information is managed internally by the Owner through the catalog.

## Permission Matrix

| Feature / Data | Owner | Consultant | Accounts | Admission | Visa |
|---|:---:|:---:|:---:|:---:|:---:|
| View all files | Yes | No | No | No | No |
| View own files | Yes | Yes | No | No | No |
| Create file | Yes | Yes | No | No | No |
| View financial data | Yes | No | Yes | No | No |
| Confirm deposit | Yes | No | Yes | No | No |
| View admission documents | Yes | Own files | No | Yes | No |
| Approve admission step | Yes | No | No | Yes | No |
| View visa documents | Yes | Own files | No | No | Yes |
| Approve visa step | Yes | No | No | No | Yes |
| View commissions | Yes | No | No | No | No |
| Input commission | Yes | No | No | No | No |
| View revenue reports | Yes | No | Limited | No | No |
| Manage users | Yes | No | No | No | No |
| Manage catalog | Yes | No | No | No | No |
| Browse program catalog | Yes | Yes | No | No | No |

## Core Access Rules

- Each internal user must have exactly one primary role unless the Owner explicitly configures otherwise.
- Consultants can only access files assigned to them.
- Accounts can access financial information for all files, but only enough student/file information to identify payments correctly.
- Admission can access admission-stage operational data.
- Visa can access visa-stage operational data.
- Commission information is confidential and Owner-only.
- Access restrictions must be enforced at the data/query layer, not only by hiding UI elements.
- Every approval, payment confirmation, document action, and status change should be recorded in the activity log.

## Related Business Flows

- [Counselling and Program Selection](flows/02_counselling_and_program_selection_flow.md)
- [File Opening](flows/03_file_opening_flow.md)
- [Payment and Deposit Confirmation](flows/04_payment_and_deposit_confirmation_flow.md)
- [Admission Processing](flows/05_admission_processing_flow.md)
- [Visa Processing](flows/06_visa_processing_flow.md)
- [University Commission Tracking](flows/07_university_commission_tracking_flow.md)
- [Access Control and Role Visibility](flows/10_access_control_and_role_visibility_flow.md)
- [User Management](flows/12_user_management_flow.md)
