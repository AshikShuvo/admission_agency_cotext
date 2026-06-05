# Implementation Flow
## Student Abroad Admission Agency Management System

This file defines the recommended order for implementing the requirement modules. Use it before assigning work to frontend, backend, QA, or progress-maintenance agents.

## Core Rule

Implement foundations first, then follow the real business lifecycle:

```text
Access and users
  -> Catalog setup
  -> Counselling
  -> File opening
  -> Payments and gates
  -> Admission
  -> Visa
  -> Exceptions and closure
  -> Commissions
  -> Notifications
  -> Reports
```

Do not start a downstream module until its required upstream data and workflow gates exist, unless the work is only a UI shell or documentation task.

## Recommended Module Order

| Order | Module | Folder | Why This Comes Here | Can Start When |
|---:|---|---|---|---|
| 1 | Access Control and Role Visibility | [ACL](modules/ACL_access_control_and_role_visibility/index.md) | Every module needs authenticated user context, role checks, protected routes, query scopes, and sensitive-field filtering. | Start immediately. |
| 2 | User Management | [USR](modules/USR_user_management/index.md) | Owner must log in, then create staff users and assign roles before real role-based workflows can be tested. | Minimal ACL role model exists and Owner bootstrap login is available. |
| 3 | Catalog and Packages | [CAT](modules/CAT_catalog_and_packages/index.md) | Counselling and file opening require active countries, universities, programs, and packages. | Owner role and catalog mutation permission exist. |
| 4 | Counselling and Program Selection | [CNS](modules/CNS_counselling_and_program_selection/index.md) | Consultants need searchable catalog and selected program context before opening files. | CAT active catalog and active package lookup exist. |
| 5 | File Opening and Student Case | [FIL](modules/FIL_file_opening_and_student_case/index.md) | The student file is the central workflow record for payments, admission, visa, documents, reports, and commissions. | CAT active package exists; CNS selected program context exists or is mocked. |
| 6 | Payments and Financial Clearance | [PAY](modules/PAY_payments_and_financial_clearance/index.md) | Admission and visa stages depend on payment recording, due calculation, and financial clearance gates. | FIL file fee snapshot exists. |
| 7 | Admission Processing | [ADM](modules/ADM_admission_processing/index.md) | Admission depends on file status, documents, and admission-stage payment clearance. | FIL and PAY core gates exist. |
| 8 | Visa Processing | [VIS](modules/VIS_visa_processing/index.md) | Visa depends on admission approval, offer letter, documents, and visa-stage payment clearance. | ADM approval and PAY visa clearance exist. |
| 9 | Exception and File Closure | [EXC](modules/EXC_exception_and_file_closure/index.md) | Hold, cancellation, rejection, reapplication, completion, and file locking need the file lifecycle to exist first. | FIL status model exists; VIS rejection/completion paths are available or defined. |
| 10 | University Commission Tracking | [COM](modules/COM_university_commission_tracking/index.md) | Commission records are Owner-only and depend on completed or enrolled files. | VIS completion or EXC final closure exists; ACL Owner-only access is enforced. |
| 11 | Notifications and Task Follow-up | [NOT](modules/NOT_notifications_and_task_follow_up/index.md) | Notifications are useful after real business events exist: file created, payment confirmed, admission approved, visa outcome, closure. | Core lifecycle events exist in FIL, PAY, ADM, VIS, and EXC. |
| 12 | Reporting and Dashboards | [REP](modules/REP_reporting_and_dashboards/index.md) | Reports should be last because they aggregate files, payments, admission, visa, commissions, notifications, and access scopes. | Core modules have persisted data and stable query scopes. |

## Phase 1 Build Path

### Phase 1A: Security and Staff Foundation

Goal: let real internal users log in and operate only inside their role boundary.

Implementation order:

1. [ACL role permissions and direct access](modules/ACL_access_control_and_role_visibility/index.md)
2. [Owner bootstrap login](modules/USR_user_management/stories/USR-EP1-US0_bootstrap_owner_login.md)
3. [Staff user creation](modules/USR_user_management/stories/USR-EP1-US1_create_staff_user.md)
4. [Staff update, suspension, and audit](modules/USR_user_management/index.md)

Minimum usable outcome:

- Owner can log in.
- Staff users can be created, assigned roles, and suspended.
- Backend rejects unauthorized API actions.
- Frontend protects routes by role.
- Consultant, Accounts, Admission, Visa, and Owner role scopes are testable.

Browser-usable user management depends on real Owner login. Staff creation must not start as a browser workflow until the system can seed an Owner, authenticate that Owner, load `/auth/me` from a real token, and protect authenticated routes.

### Phase 1B: Pre-File Setup

Goal: prepare the data needed before a student file can be opened.

Implementation order:

1. [CAT](modules/CAT_catalog_and_packages/index.md)
2. [CNS](modules/CNS_counselling_and_program_selection/index.md)

Minimum usable outcome:

- Owner can create country, university, program, and active package.
- Only one package can be active per program.
- Consultant can browse active catalog data.
- Consultant can select a program with an active package.

### Phase 1C: File and Money Core

Goal: create the central file and enforce payment control.

Implementation order:

1. [FIL](modules/FIL_file_opening_and_student_case/index.md)
2. [PAY](modules/PAY_payments_and_financial_clearance/index.md)

Minimum usable outcome:

- Consultant can create a student file.
- System creates a unique file number.
- Active package fees are snapshot-copied onto the file.
- Accounts can record and confirm payments.
- Due calculation uses only confirmed payments.
- Admission cannot start until file-opening payment is cleared.

### Phase 1D: Processing Lifecycle

Goal: move a real student file through admission and visa.

Implementation order:

1. [ADM](modules/ADM_admission_processing/index.md)
2. [VIS](modules/VIS_visa_processing/index.md)

Minimum usable outcome:

- Admission can request and verify documents.
- Admission can submit university application.
- Admission can upload offer letter.
- Admission approval requires required documents and payment clearance.
- Visa can request and verify documents.
- Visa can submit application, record outcome, and complete or reject the file.

### Phase 1E: Closure, Owner Revenue, and Visibility

Goal: finish business lifecycle and give management visibility.

Implementation order:

1. [EXC](modules/EXC_exception_and_file_closure/index.md)
2. [COM](modules/COM_university_commission_tracking/index.md)
3. [NOT](modules/NOT_notifications_and_task_follow_up/index.md)
4. [REP](modules/REP_reporting_and_dashboards/index.md)

Minimum usable outcome:

- Files can be put on hold, cancelled, rejected, completed, and locked.
- Owner can record commission for completed/enrolled files.
- Users receive task follow-up for important lifecycle events.
- Owner, Accounts, Consultant, Admission, and Visa dashboards show role-appropriate data.

## What To Start Next

With `ACL-EP1` accepted, start here:

1. [USR-EP1: Staff Account Lifecycle](modules/USR_user_management/epics/USR-EP1_staff_account_lifecycle.md)
2. [USR-EP1-US0: Bootstrap Owner Login](modules/USR_user_management/stories/USR-EP1-US0_bootstrap_owner_login.md)
3. Backend first:
   - [USR-EP1-US0-BE1](modules/USR_user_management/tasks/USR-EP1-US0-BE1.md)
   - [USR-EP1-US0-BE2](modules/USR_user_management/tasks/USR-EP1-US0-BE2.md)
   - [USR-EP1-US0-BE3](modules/USR_user_management/tasks/USR-EP1-US0-BE3.md)
4. Then frontend:
   - [USR-EP1-US0-FE1](modules/USR_user_management/tasks/USR-EP1-US0-FE1.md)
   - [USR-EP1-US0-FE2](modules/USR_user_management/tasks/USR-EP1-US0-FE2.md)
   - [USR-EP1-US0-FE3](modules/USR_user_management/tasks/USR-EP1-US0-FE3.md)

Reason: staff creation cannot be used or verified through the browser until a real Owner account can authenticate and carry a protected session.

## Parallel Work Rules

Some frontend and backend work can happen in parallel, but only with clear contracts.

Safe parallel work:

- Frontend can build UI shell from design guide while backend builds API contract.
- Backend can build entities and service tests before frontend integration.
- QA can prepare test scenarios while implementation is in progress.

Avoid parallel work when:

- API contract is not agreed.
- Access-control behavior is unclear.
- A downstream module depends on data that does not exist yet.
- Two agents need to change the same task/story/progress files at the same time.

## Module Completion Rule

A module is complete only when:

- All EPIC files are complete.
- All story files are accepted.
- All frontend task plans are complete.
- All backend task plans are complete.
- Required tests are added or explicitly documented as a blocker.
- [Progress Tracker](progress_tracker.md) module row is updated.
- No open blocker remains for that module.

## How To Use This File Before Assigning Work

1. Identify the current highest completed module in [Progress Tracker](progress_tracker.md).
2. Pick the next module from the recommended order above.
3. Open that module folder `index.md`.
4. Choose the first incomplete EPIC.
5. Choose the first incomplete user story.
6. Assign backend tasks first when frontend depends on API/data/permissions.
7. Assign frontend tasks after backend contract exists or mark the dependency clearly.
8. Update task, story, EPIC, module folder, and tracker files after work completes.
