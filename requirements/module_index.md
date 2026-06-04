# Requirement Module Index
## Student Abroad Admission Agency Management System

This index maps business flows into requirement modules. Each module has an independent folder containing separate EPIC files, user story files, detailed task implementation-plan files, acceptance criteria, and progress fields.

Source documents:

- [Business Flows Index](../business/flows/00_business_flows_index.md)
- [Users and Roles](../business/users_and_roles.md)
- [Architecture Module Boundaries](../architecture/module_boundaries.md)
- [Testing Strategy](../architecture/testing_strategy.md)
- [Agent Map](agent_map.md)

## Module Map

| Module ID | Module Folder | Source Business Flow | Primary Frontend Workspace | Primary Backend Module |
|---|---|---|---|---|
| CAT | [Catalog and Packages](modules/CAT_catalog_and_packages/index.md) | Catalog and Package Setup | Catalog Management | Catalog |
| CNS | [Counselling and Program Selection](modules/CNS_counselling_and_program_selection/index.md) | Counselling and Program Selection | Consultant File Workspace | Catalog, Students, Files |
| FIL | [File Opening and Student Case](modules/FIL_file_opening_and_student_case/index.md) | File Opening | Consultant File Workspace | Students, Files / Cases, File Fees |
| PAY | [Payments and Financial Clearance](modules/PAY_payments_and_financial_clearance/index.md) | Payment and Deposit Confirmation | Accounts Payment Workspace | Payments, File Fees |
| ADM | [Admission Processing](modules/ADM_admission_processing/index.md) | Admission Processing | Admission Workspace | Admission, Documents |
| VIS | [Visa Processing](modules/VIS_visa_processing/index.md) | Visa Processing | Visa Workspace | Visa, Documents |
| COM | [University Commission Tracking](modules/COM_university_commission_tracking/index.md) | University Commission Tracking | Owner Reports and Settings | Commissions |
| REP | [Reporting and Dashboards](modules/REP_reporting_and_dashboards/index.md) | Reporting and Dashboard | Role-Based Dashboard | Reporting |
| NOT | [Notifications and Task Follow-up](modules/NOT_notifications_and_task_follow_up/index.md) | Notifications and Communication | Role-Based Dashboard | Notifications |
| ACL | [Access Control and Role Visibility](modules/ACL_access_control_and_role_visibility/index.md) | Access Control and Role Visibility | All Workspaces | Auth and Users |
| EXC | [Exception and File Closure](modules/EXC_exception_and_file_closure/index.md) | Exception and File Closure Handling | File Detail Workspaces | Files / Cases |
| USR | [User Management](modules/USR_user_management/index.md) | User Management | Owner Reports and Settings | Auth and Users |

## Folder Structure

Each module folder follows this shape:

```text
{MODULE_ID}_{module_slug}/
├── index.md
├── epics/
├── stories/
└── tasks/
```

Read [Detailed Structure Guide](detailed_structure_guide.md) for exact file responsibility and status-maintenance rules.

## Requirement ID Format

Use stable IDs in this format:

```text
{MODULE}-EP{number}-US{number}-{FE|BE|QA}{number}
```

Examples:

- `CAT-EP1-US1-FE1`: first frontend task under catalog EPIC 1 story 1.
- `PAY-EP2-US2-BE3`: third backend task under payment EPIC 2 story 2.
- `ADM-EP1-US2-QA1`: first quality or acceptance verification task under admission EPIC 1 story 2.

## Status Values

| Status | Meaning |
|---|---|
| Not Started | Work has not begun. |
| In Progress | An agent or developer is actively implementing it. |
| Blocked | Work cannot continue without a business, design, or technical decision. |
| In Review | Implementation is complete but not verified or accepted. |
| Complete | Implementation, tests, and acceptance checks are done. |

## Agent Assignment Rule

Each task should have one current owner at a time:

- Frontend task owner: frontend agent or frontend developer.
- Backend task owner: backend agent or backend developer.
- QA task owner: reviewer, test agent, or developer responsible for verification.

When work changes ownership, update the task file, story file, module folder index, and [Progress Tracker](progress_tracker.md).

## Agent Routing

Use [Agent Map](agent_map.md) before assigning implementation work. It explains how frontend agents, backend agents, QA/review agents, and progress maintainers should choose tasks, handle dependencies, update checkboxes, and maintain [Progress Tracker](progress_tracker.md).
