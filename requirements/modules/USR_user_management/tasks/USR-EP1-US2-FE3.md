# USR-EP1-US2-FE3: Add tests for role change reason and preserved user identity display.
## Detailed Frontend Task Plan

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `USR` - User Management |
| EPIC | [USR-EP1: Staff Account Lifecycle](../epics/USR-EP1_staff_account_lifecycle.md) |
| User Story | [USR-EP1-US2: Update Staff Details and Role](../stories/USR-EP1-US2_update_staff_details_and_role.md) |
| Task Type | `FE` |

## Business Context

As an Owner, I want to update staff details or role so that access stays aligned with current business responsibility.

This task supports the module goal: Allow Owner to create, update, suspend, and audit internal staff accounts so every user has the correct role before accessing files, payments, documents, reports, catalog records, or commissions.

## Source Documents

- [User Management Flow](../../../../business/flows/12_user_management_flow.md)
- [Users and Roles](../../../../business/users_and_roles.md)
- [User Management Design](../../../../design-guide/16-staff-user-management.html)

## Acceptance Criteria Impact

- [ ] Owner can update contact details, department, role, and account status.
- [ ] Role changes require a business reason.
- [ ] Past activity remains linked to the same user and is not rewritten.

## Business Rules To Preserve

- Only Owner manages staff users.
- Each user has one primary role unless explicitly approved.
- Suspension blocks access without deleting history.

## Dependencies To Check First

- Depends on ACL role model and audit logging.

## Implementation Plan

1. Locate or create the Owner Reports and Settings route or workspace section that owns this behavior.
2. Create typed UI models for the data needed by the story; keep field names aligned with the backend DTO/API contract.
3. Build the screen, panel, form, table, queue, or state component described by the task with loading, empty, success, and error states.
4. Apply role-aware behavior using authenticated user role and backend permission response; do not rely on visual hiding for security decisions.
5. Connect mutation actions to API calls only after backend contract exists; otherwise document the missing contract as a blocker.
6. Add user-visible validation for required fields, invalid transitions, duplicate warnings, and blocked workflow states mentioned by acceptance criteria.
7. Add frontend coverage for the happy path and at least one blocked/error path. Prefer Playwright for full role flows and component tests only for risky reusable pieces.
8. Write tests that assert the visible business outcome, not only that components render.
9. Test at least two roles: one allowed role and one restricted role.

## UI and Contract Expectations

- Frontend workspace: `Owner Reports and Settings`.
- Use Next.js, TypeScript, Tailwind CSS, and React Query patterns when implementation begins.
- Prefer API-driven permissions and response fields over hardcoded role assumptions.
- Required states: loading, empty, successful data, validation error, authorization-restricted, and server error.
- Design reference: `../../../../design-guide/16-staff-user-management.html`.

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
Module: USR
Story: USR-EP1-US2
Completed task: USR-EP1-US2-FE3
Files changed:
Tests run:
Tracker updated:
Open blockers:
Next recommended task:
```
