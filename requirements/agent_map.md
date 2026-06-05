# Agent Map
## Requirement Routing and Progress Maintenance

This document explains how frontend agents, backend agents, review agents, and progress-maintenance agents should route through the requirement documents, choose tasks, and keep completion tracking accurate.

## Goal

Use the requirement workspace as the source of truth for implementation work:

```text
Business flow
  -> Requirement module
  -> EPIC
  -> User story
  -> Frontend task or backend task
  -> Implementation
  -> Test and review
  -> Progress tracker update
```

No agent should pick work directly from memory, conversation history, or a high-level business flow when a matching requirement task exists.

## Agent Roles

| Agent Role | Main Responsibility | Primary Documents |
|---|---|---|
| Requirement Router | Select the correct module, EPIC, story, and task before implementation starts. | [Module Index](module_index.md), module folder indexes, this agent map |
| Frontend Agent | Implement `FE` task files only: screens, routes, components, UI states, frontend validation, frontend tests. | Target task file, story file, EPIC file, module folder index, relevant design guide page |
| Backend Agent | Implement `BE` task files only: data model, DTOs, services, APIs, authorization, backend tests. | Target task file, story file, EPIC file, module folder index, architecture docs, business flow source |
| QA / Review Agent | Verify acceptance criteria, tests, role access, and task completion evidence. | Target story file, task files, [Testing Strategy](../architecture/testing_strategy.md), progress tracker |
| Progress Maintainer | Update task, story, EPIC, module folder, tracker totals, blockers, and completion log. | Target module folder, [Progress Tracker](progress_tracker.md) |

One person or AI agent can perform more than one role, but the work should still follow these role boundaries.

## Routing Order

When assigning work, route in this order:

1. Open [requirements/index.md](index.md).
2. Open [module_index.md](module_index.md).
3. Select the module folder that matches the business capability.
4. Open the selected module folder `index.md`.
5. Pick the next incomplete EPIC and open its file under `epics/`.
6. Pick the next incomplete user story and open its file under `stories/`.
7. Assign either frontend task files or backend task files under `tasks/` based on agent type.
8. Check dependencies before starting.
9. Mark the selected task as `In Progress` in the task file or module progress notes if active status tracking has been added.
10. Implement the task.
11. Run the relevant tests.
12. Update the task file, story file, EPIC file, module folder index, and [progress_tracker.md](progress_tracker.md).

## Module Routing Map

| Business Capability | Module ID | Requirement Folder | Frontend Agent Starts At | Backend Agent Starts At |
|---|---|---|---|---|
| Manage countries, universities, programs, packages | CAT | [Catalog and Packages](modules/CAT_catalog_and_packages/index.md) | Catalog management screens | Catalog entities, APIs, package activation rules |
| Search programs and counsel students | CNS | [Counselling and Program Selection](modules/CNS_counselling_and_program_selection/index.md) | Program browser and counselling input UI | Program search, counselling draft, eligibility APIs |
| Open student file and create package snapshot | FIL | [File Opening and Student Case](modules/FIL_file_opening_and_student_case/index.md) | Student/file forms and file detail | Student, file, file number, fee snapshot services |
| Record payments and enforce payment gates | PAY | [Payments and Financial Clearance](modules/PAY_payments_and_financial_clearance/index.md) | Accounts payment workbench | Payment, due calculation, clearance gate services |
| Process admission documents and offer letter | ADM | [Admission Processing](modules/ADM_admission_processing/index.md) | Admission checklist and approval UI | Admission checklist, document verification, approval APIs |
| Process visa documents and outcome | VIS | [Visa Processing](modules/VIS_visa_processing/index.md) | Visa checklist, submission, outcome UI | Visa checklist, application, outcome, completion services |
| Track confidential commission | COM | [University Commission Tracking](modules/COM_university_commission_tracking/index.md) | Owner commission screens | Owner-only commission APIs and reporting |
| View dashboards and reports | REP | [Reporting and Dashboards](modules/REP_reporting_and_dashboards/index.md) | Role dashboards and report tables | Reporting queries and aggregates |
| Notify users and manage follow-up tasks | NOT | [Notifications and Task Follow-up](modules/NOT_notifications_and_task_follow_up/index.md) | Notification list and task center | Notification entity, event routing, read/resolve APIs |
| Enforce permissions and visibility | ACL | [Access Control and Role Visibility](modules/ACL_access_control_and_role_visibility/index.md) | Protected routes and role-aware UI | Guards, policies, query scopes, response filtering |
| Hold, cancel, reject, close, and lock files | EXC | [Exception and File Closure](modules/EXC_exception_and_file_closure/index.md) | Exception action panels and locked states | File status transitions and edit restrictions |
| Bootstrap Owner login and manage staff users | USR | [User Management](modules/USR_user_management/index.md) | Login/session screens and staff user management screens | Auth/session APIs, user lifecycle APIs, suspension, audit trail |

## Task Selection Rules

Use this priority when choosing the next task:

1. Backend foundation before frontend dependency: entities, APIs, authorization, and service contracts should exist before final frontend integration.
2. Frontend shell can start early when the design guide and API contract are clear.
3. Implement stories in EPIC order unless a later story is explicitly unblocked and independent.
4. Prefer completing one full user story before starting many partial stories.
5. Do not skip access-control tasks when the story touches restricted data.
6. Do not mark a story complete until frontend tasks, backend tasks, acceptance criteria, and tests are complete.

## Dependency Guide

| If Working On | Check These First |
|---|---|
| CNS | CAT active catalog and active package lookup |
| FIL | CAT active package, CNS selected program context |
| PAY | FIL file fee snapshot |
| ADM | FIL file status, PAY file-opening and admission clearance |
| VIS | ADM approval and offer letter, PAY visa clearance |
| COM | VIS completion or enrollment state, ACL owner-only access |
| REP | FIL, PAY, ADM, VIS, COM, ACL query scopes |
| NOT | Business events from FIL, PAY, ADM, VIS, EXC |
| ACL | User roles, all module data visibility rules |
| EXC | FIL status model, VIS rejection, COM completion eligibility |
| USR | ACL role model, audit logging, and bootstrap Owner login before staff creation |

## Frontend Agent Workflow

1. Open the target module folder index.
2. Open the selected EPIC file.
3. Open the selected user story file and acceptance criteria.
4. Open only the assigned `FE` task file.
5. Open the linked design-guide page if one exists.
6. Check backend contract availability:
   - If API exists, integrate with it.
   - If API does not exist, build only the UI shell with typed placeholder contract and mark backend dependency as blocked.
7. Implement the route, component, state handling, validation, and frontend test requested by the task.
8. Update the task file, story file, EPIC file, and module folder index for completed `FE` tasks.
9. Update [progress_tracker.md](progress_tracker.md) frontend task counts.

Frontend completion evidence should include:

- Completed task IDs.
- Changed route/component files.
- Test command or reason tests were not run.
- Any backend dependency still blocking full story completion.

## Backend Agent Workflow

1. Open the target module folder index.
2. Open the selected EPIC file.
3. Open the selected user story file and acceptance criteria.
4. Open only the assigned `BE` task file.
5. Open the relevant architecture docs:
   - [Module Boundaries](../architecture/module_boundaries.md)
   - [Data Model](../architecture/data_model.md)
   - [API Design](../architecture/api_design.md)
   - [Access Control](../architecture/access_control.md)
6. Implement entities, DTOs, service logic, API routes, authorization, audit events, and backend tests requested by the task.
7. Update the task file, story file, EPIC file, and module folder index for completed `BE` tasks.
8. Update [progress_tracker.md](progress_tracker.md) backend task counts.

Backend completion evidence should include:

- Completed task IDs.
- Changed entity/module/service/controller/test files.
- API endpoints or service functions added.
- Test command or reason tests were not run.
- Any frontend dependency still waiting for integration.

## QA / Review Workflow

QA should verify the story, not only the task.

1. Open the target module folder index, EPIC file, story file, and linked task files.
2. Confirm all frontend and backend task checkboxes for the story are complete.
3. Confirm every acceptance criterion is satisfied.
4. Run or inspect relevant frontend and backend tests.
5. Verify access-control and sensitive-data behavior when the story touches role visibility.
6. Move the story to complete only when implementation and tests are done.
7. Add unresolved issues to the blocker table in [progress_tracker.md](progress_tracker.md).

QA completion evidence should include:

- Story ID reviewed.
- Acceptance criteria passed.
- Tests checked.
- Remaining risks or blockers.

## Progress Tracking Rules

Update progress in two places:

1. The detailed folder file where the work item lives.
2. [progress_tracker.md](progress_tracker.md), which summarizes all modules.

### Detailed Folder Updates

For each completed task, change the checkbox from:

```text
- [ ] `CAT-EP1-US1-FE1` Build country and university list/detail screens...
```

to:

```text
- [x] `CAT-EP1-US1-FE1` Build country and university list/detail screens...
```

When all frontend and backend tasks under a story are complete, mark that story's acceptance criteria as complete if verified. Then update the EPIC file and module folder index.

### Progress Tracker Updates

In [progress_tracker.md](progress_tracker.md):

- Increase the module's frontend task count when an `FE` task is completed.
- Increase the module's backend task count when a `BE` task is completed.
- Increase story count only when the whole story is accepted.
- Increase EPIC count only when all stories in the EPIC are accepted.
- Increase module count only when all EPICs in the module are accepted.
- Update `Status` to `In Progress`, `Blocked`, `In Review`, or `Complete`.
- Add blocker rows when work cannot continue.
- Add completion log rows for meaningful completions.

### Completion Math

Use these formulas:

```text
Module frontend completion = completed frontend tasks / planned frontend tasks
Module backend completion = completed backend tasks / planned backend tasks
Story complete = all FE tasks + all BE tasks + acceptance criteria + required tests
EPIC complete = all stories complete
Module complete = all EPICs complete and no open blockers
Overall completion = complete items / planned items
```

## Blocker Handling

Use `Blocked` when an agent cannot continue because of a missing decision, missing dependency, failing prerequisite, or unclear rule.

Add a row to `Current Blockers` in [progress_tracker.md](progress_tracker.md):

| Field | Meaning |
|---|---|
| ID | Stable blocker ID such as `BLK-CAT-001`. |
| Module | Module ID or name. |
| Blocker | What is preventing work. |
| Decision Needed | Exact decision or dependency needed. |
| Owner | Person or role responsible for resolving it. |
| Status | Open, In Review, or Closed. |

Do not mark unrelated tasks blocked if they can continue independently.

## Handoff Format

When an agent finishes or pauses work, leave a handoff note using this format:

```text
Module:
Story:
Completed tasks:
Files changed:
Tests run:
Tracker updated:
Open blockers:
Next recommended task:
```

The next agent should start from the handoff note, then verify the module folder index and progress tracker before continuing.

## Assignment Examples

### Example Frontend Assignment

```text
Agent: Frontend
Module: PAY
Story: PAY-EP1-US1 Record Student Payment
Tasks:
- PAY-EP1-US1-FE1
- PAY-EP1-US1-FE2
- PAY-EP1-US1-FE3
Do not implement:
- Payment entity
- Payment confirmation API
- Due calculation service
Progress update:
- Check completed FE tasks in modules/PAY_payments_and_financial_clearance/tasks and story files
- Update PAY frontend task count in progress_tracker.md
```

### Example Backend Assignment

```text
Agent: Backend
Module: FIL
Story: FIL-EP2-US1 Snapshot Package Fees
Tasks:
- FIL-EP2-US1-BE1
- FIL-EP2-US1-BE2
- FIL-EP2-US1-BE3
Do not implement:
- File detail UI
- Package preview UI
Progress update:
- Check completed BE tasks in modules/FIL_file_opening_and_student_case/tasks and story files
- Update FIL backend task count in progress_tracker.md
```

## Stop Conditions

An agent should stop and create a blocker when:

- The task depends on a business rule not yet decided.
- The task requires an API contract that conflicts with an existing module.
- The task would expose restricted data to the wrong role.
- The task would change another module's ownership boundary without approval.
- The implementation cannot be tested or verified with available project setup.

Stop only the blocked task. Continue with independent tasks when possible.
