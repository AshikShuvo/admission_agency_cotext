# NOT-EP2-US1-FE1: Build task center page with filters, unread count, and result list.
## Detailed Frontend Task Plan

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `NOT` - Notifications and Task Follow-up |
| EPIC | [NOT-EP2: Task Center and Follow-up](../epics/NOT-EP2_task_center_and_follow_up.md) |
| User Story | [NOT-EP2-US1: View My Task Center](../stories/NOT-EP2-US1_view_my_task_center.md) |
| Task Type | `FE` |

## Business Context

As a staff user, I want a task center so that I can see pending follow-up items for my role.

This task supports the module goal: Create role-aware in-app notifications and task follow-up items when important business events occur, while respecting file assignment and data visibility rules.

## Source Documents

- [Notifications and Communication Flow](../../../../business/flows/09_notifications_and_communication_flow.md)
- [Module Boundaries](../../../../architecture/module_boundaries.md)
- [Notification Task Center Design](../../../../design-guide/17-notification-task-center.html)

## Acceptance Criteria Impact

- [ ] Task center lists unread notifications and unresolved follow-up items.
- [ ] Users see only tasks they are authorized to act on.
- [ ] Tasks can be filtered by file, stage, event type, and read/resolved state.

## Business Rules To Preserve

- Notifications must respect role visibility.
- Consultants receive notifications only for assigned files.
- Commission notifications are Owner-only.

## Dependencies To Check First

- Depends on business events from FIL, PAY, ADM, VIS, and EXC.

## Implementation Plan

1. Locate or create the Role-Based Dashboard route or workspace section that owns this behavior.
2. Create typed UI models for the data needed by the story; keep field names aligned with the backend DTO/API contract.
3. Build the screen, panel, form, table, queue, or state component described by the task with loading, empty, success, and error states.
4. Apply role-aware behavior using authenticated user role and backend permission response; do not rely on visual hiding for security decisions.
5. Connect mutation actions to API calls only after backend contract exists; otherwise document the missing contract as a blocker.
6. Add user-visible validation for required fields, invalid transitions, duplicate warnings, and blocked workflow states mentioned by acceptance criteria.
7. Add frontend coverage for the happy path and at least one blocked/error path. Prefer Playwright for full role flows and component tests only for risky reusable pieces.

## UI and Contract Expectations

- Frontend workspace: `Role-Based Dashboard`.
- Use Next.js, TypeScript, Tailwind CSS, and React Query patterns when implementation begins.
- Prefer API-driven permissions and response fields over hardcoded role assumptions.
- Required states: loading, empty, successful data, validation error, authorization-restricted, and server error.
- Design reference: `../../../../design-guide/17-notification-task-center.html`.

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
Story: NOT-EP2-US1
Completed task: NOT-EP2-US1-FE1
Files changed:
Tests run:
Tracker updated:
Open blockers:
Next recommended task:
```
