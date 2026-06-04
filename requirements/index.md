# Business Requirements Index
## Student Abroad Admission Agency Management System

This folder translates the business domain into delivery-ready requirements. It is designed for future frontend and backend agents to implement module by module, story by story, and task by task.

## Purpose

- Keep business knowledge organized by module.
- Break each module into EPICs.
- Break each EPIC into user stories.
- Break each user story into frontend and backend implementation tasks.
- Track completion across module, EPIC, story, frontend task, and backend task levels.

## Requirement Documents

| Document | Purpose |
|---|---|
| [Module Index](module_index.md) | Navigator for every requirement module. |
| [Implementation Flow](implementation_flow.md) | Recommended module completion order and phase-by-phase implementation path. |
| [Agent Map](agent_map.md) | Routing guide for assigning frontend, backend, QA, and progress-maintenance agents to requirement tasks. |
| [Progress Tracker](progress_tracker.md) | Central completion tracker for module, EPIC, story, frontend, and backend progress. |
| [Detailed Structure Guide](detailed_structure_guide.md) | Defines the module folder, EPIC file, story file, and task implementation-plan structure. |
| [Module Folder Template](templates/module_folder_index_template.md) | Reusable module folder index structure for adding future modules. |
| [EPIC Template](templates/epic_template.md) | Reusable structure for one detailed EPIC file. |
| [Story Template](templates/story_template.md) | Reusable structure for one detailed user story file. |
| [Task Plan Template](templates/task_implementation_plan_template.md) | Reusable structure for one detailed frontend or backend task implementation plan. |

## Independent Module Folders

| # | Module | Requirement Folder |
|---|---|---|
| 1 | Catalog and Packages | [CAT_catalog_and_packages](modules/CAT_catalog_and_packages/index.md) |
| 2 | Counselling and Program Selection | [CNS_counselling_and_program_selection](modules/CNS_counselling_and_program_selection/index.md) |
| 3 | File Opening and Student Case | [FIL_file_opening_and_student_case](modules/FIL_file_opening_and_student_case/index.md) |
| 4 | Payments and Financial Clearance | [PAY_payments_and_financial_clearance](modules/PAY_payments_and_financial_clearance/index.md) |
| 5 | Admission Processing | [ADM_admission_processing](modules/ADM_admission_processing/index.md) |
| 6 | Visa Processing | [VIS_visa_processing](modules/VIS_visa_processing/index.md) |
| 7 | University Commission Tracking | [COM_university_commission_tracking](modules/COM_university_commission_tracking/index.md) |
| 8 | Reporting and Dashboards | [REP_reporting_and_dashboards](modules/REP_reporting_and_dashboards/index.md) |
| 9 | Notifications and Task Follow-up | [NOT_notifications_and_task_follow_up](modules/NOT_notifications_and_task_follow_up/index.md) |
| 10 | Access Control and Role Visibility | [ACL_access_control_and_role_visibility](modules/ACL_access_control_and_role_visibility/index.md) |
| 11 | Exception and File Closure | [EXC_exception_and_file_closure](modules/EXC_exception_and_file_closure/index.md) |
| 12 | User Management | [USR_user_management](modules/USR_user_management/index.md) |

## Suggested Reading Path

1. Read [Business Documentation Index](../business/index.md) for domain context.
2. Read [Architecture Module Boundaries](../architecture/module_boundaries.md) for technical module ownership.
3. Read [Implementation Flow](implementation_flow.md) to know which module should be implemented next.
4. Read [Module Index](module_index.md) to open the target module folder.
5. Read [Agent Map](agent_map.md) before assigning frontend, backend, QA, or progress-maintenance work.
6. Open the selected independent module folder.
7. Read the target EPIC file, then the target user story file, then the target task implementation-plan file.
8. Use [Progress Tracker](progress_tracker.md) before assigning or marking work complete.

## Implementation Discipline

- Frontend agents should complete only tasks listed under `Frontend Tasks`.
- Backend agents should complete only tasks listed under `Backend Tasks`.
- Agents must update the task file, story file, module folder index, and central [Progress Tracker](progress_tracker.md) after completing a task.
- No story is complete until its frontend tasks, backend tasks, acceptance criteria, and tests are complete.
