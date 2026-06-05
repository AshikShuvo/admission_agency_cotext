# ACL-EP1-US1-FE1: Build role-based navigation configuration for allowed workspaces.
## Detailed Frontend Task Plan

Status: `Complete`
Owner: `Gibbs`
Last updated: `2026-06-05`

## Traceability

| Level | Reference |
|---|---|
| Module | `ACL` - Access Control and Role Visibility |
| EPIC | [ACL-EP1: Role Permissions](../epics/ACL-EP1_role_permissions.md) |
| User Story | [ACL-EP1-US1: Enforce Role Permissions](../stories/ACL-EP1-US1_enforce_role_permissions.md) |
| Task Type | `FE` |

## Business Context

As the system, I want to enforce role permissions so that users cannot perform actions outside their business responsibility.

This task supports the module goal: Ensure every screen, API, query, and action respects the user's role and data scope. UI hiding is not enough; access must be enforced by backend authorization and query-level filters.

## Source Documents

- [Access Control and Role Visibility Flow](../../../../business/flows/10_access_control_and_role_visibility_flow.md)
- [Users and Roles](../../../../business/users_and_roles.md)
- [Access Control Architecture](../../../../architecture/access_control.md)

## Acceptance Criteria Impact

- [x] Each protected API checks authenticated role before executing mutations.
- [x] Non-owner users cannot manage catalog, users, or commissions.
- [x] Accounts cannot approve admission or visa stages.

## Business Rules To Preserve

- Backend authorization is mandatory.
- UI hiding is not enough.
- Sensitive fields are filtered by role.

## Dependencies To Check First

- Depends on role model from business/users_and_roles.md and applies to all modules.

## Implementation Plan

1. Locate or create the All Workspaces route or workspace section that owns this behavior.
2. Create typed UI models for the data needed by the story; keep field names aligned with the backend DTO/API contract.
3. Build the screen, panel, form, table, queue, or state component described by the task with loading, empty, success, and error states.
4. Apply role-aware behavior using authenticated user role and backend permission response; do not rely on visual hiding for security decisions.
5. Connect mutation actions to API calls only after backend contract exists; otherwise document the missing contract as a blocker.
6. Add user-visible validation for required fields, invalid transitions, duplicate warnings, and blocked workflow states mentioned by acceptance criteria.
7. Add frontend coverage for the happy path and at least one blocked/error path. Prefer Playwright for full role flows and component tests only for risky reusable pieces.
8. Test at least two roles: one allowed role and one restricted role.

## UI and Contract Expectations

- Frontend workspace: `All Workspaces`.
- Use Next.js, TypeScript, Tailwind CSS, and React Query patterns when implementation begins.
- Prefer API-driven permissions and response fields over hardcoded role assumptions.
- Required states: loading, empty, successful data, validation error, authorization-restricted, and server error.
- Design reference: `../../../../design-guide/14-notifications-access-exceptions.html`.

## Data, State, and Error Handling

- Identify all required fields from the story acceptance criteria before implementation.
- Keep IDs stable and use backend-generated identifiers for persisted records.
- Handle not found, forbidden, validation error, duplicate/conflict, and workflow-blocked responses.
- Preserve historical records when the business flow says data must not be deleted or overwritten.
- Do not expose restricted fields in UI state, API responses, logs, or test fixtures.

## Test Plan

- [x] Add or update automated tests for the normal successful path.
- [x] Add or update tests for at least one blocked or invalid path.
- [x] Add role/access tests when task touches restricted data or actions.
- [x] Confirm test data includes the minimum business objects needed for this story.
- [x] Record the test command in the agent handoff note.

## Definition of Done

- [x] Implementation matches this task plan and the linked story acceptance criteria.
- [x] Required UI/API/service behavior is implemented in the correct module boundary.
- [x] Authorization and data visibility are enforced where applicable.
- [x] Tests are added or an explicit test gap is recorded as a blocker.
- [x] This task checkbox is marked complete in the story file and source module summary.
- [x] [Progress Tracker](../../../progress_tracker.md) is updated with the completed task count.

## Handoff Note Template

```text
Module: ACL
Story: ACL-EP1-US1
Completed task: ACL-EP1-US1-FE1
Files changed:
Tests run:
Tracker updated:
Open blockers:
Next recommended task:
```
