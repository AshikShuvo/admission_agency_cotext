# NOT-EP1-US1-BE3: Add tests for event creation, target selection, and commission owner-only routing.
## Detailed Backend Task Plan

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `NOT` - Notifications and Task Follow-up |
| EPIC | [NOT-EP1: Business Event Notifications](../epics/NOT-EP1_business_event_notifications.md) |
| User Story | [NOT-EP1-US1: Create In-App Notification from Business Event](../stories/NOT-EP1-US1_create_in_app_notification_from_business_event.md) |
| Task Type | `BE` |

## Business Context

As the system, I want to create notifications from important business events so that the responsible role knows what happened.

This task supports the module goal: Create role-aware in-app notifications and task follow-up items when important business events occur, while respecting file assignment and data visibility rules.

## Source Documents

- [Notifications and Communication Flow](../../../../business/flows/09_notifications_and_communication_flow.md)
- [Module Boundaries](../../../../architecture/module_boundaries.md)
- [Notification Task Center Design](../../../../design-guide/17-notification-task-center.html)

## Acceptance Criteria Impact

- [ ] Notification records include event type, target user or role, file link, message, read state, and timestamp.
- [ ] Consultant notifications are limited to assigned files.
- [ ] Commission-related notifications are Owner-only.

## Business Rules To Preserve

- Notifications must respect role visibility.
- Consultants receive notifications only for assigned files.
- Commission notifications are Owner-only.

## Dependencies To Check First

- Depends on business events from FIL, PAY, ADM, VIS, and EXC.

## Implementation Plan

1. Implement inside the NestJS Notifications ownership boundary unless an explicit dependency requires another module.
2. Define or update Prisma/NestJS entities, DTOs, enums, and validation rules needed by the task.
3. Implement service-layer business logic first; controllers should stay thin and call typed service methods.
4. Apply authorization guards and query-level scope filters before reading or mutating protected records.
5. Persist audit log or notification events when the task changes sensitive business state.
6. Return role-appropriate response shapes and exclude sensitive fields for restricted roles.
7. Add unit tests for business rules and integration tests for API behavior, persistence, and authorization.
8. Include fixtures for allowed and blocked roles, valid and invalid inputs, and important workflow states.

## Backend Contract Expectations

- Backend module ownership: `Notifications`.
- Use NestJS services/controllers, TypeScript DTOs, Prisma/PostgreSQL persistence, and JWT role context when implementation begins.
- Required enforcement: authentication, role permission, query-level data scope, input validation, and business-rule validation.
- REST/API reference: `../../../../architecture/api_design.md` from repository root.
- Access-control reference: `../../../../architecture/access_control.md` from repository root.

## Data, State, and Error Handling

- Identify all required fields from the story acceptance criteria before implementation.
- Keep IDs stable and use backend-generated identifiers for persisted records.
- Handle not found, forbidden, validation error, duplicate/conflict, and workflow-blocked responses.
- Preserve historical records when the business flow says data must not be deleted or overwritten.
- Do not expose restricted fields in UI state, API responses, logs, or test fixtures.

## Test Plan

- [ ] Add or update automated tests for the normal successful path.
- [ ] Add or update tests for at least one blocked or invalid path.
- [ ] Add role/access tests when task touches restricted data or actions.
- [ ] Confirm test data includes the minimum business objects needed for this story.
- [ ] Record the test command in the agent handoff note.

## Definition of Done

- [ ] Implementation matches this task plan and the linked story acceptance criteria.
- [ ] Required UI/API/service behavior is implemented in the correct module boundary.
- [ ] Authorization and data visibility are enforced where applicable.
- [ ] Tests are added or an explicit test gap is recorded as a blocker.
- [ ] This task checkbox is marked complete in the story file and source module summary.
- [ ] [Progress Tracker](../../../progress_tracker.md) is updated with the completed task count.

## Handoff Note Template

```text
Module: NOT
Story: NOT-EP1-US1
Completed task: NOT-EP1-US1-BE3
Files changed:
Tests run:
Tracker updated:
Open blockers:
Next recommended task:
```
