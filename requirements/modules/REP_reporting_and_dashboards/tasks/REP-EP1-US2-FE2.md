# REP-EP1-US2-FE2: Add role-aware empty states and quick links to relevant workspaces.
## Detailed Frontend Task Plan

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `REP` - Reporting and Dashboards |
| EPIC | [REP-EP1: Role-Based Dashboards](../epics/REP-EP1_role_based_dashboards.md) |
| User Story | [REP-EP1-US2: Staff Dashboards](../stories/REP-EP1-US2_staff_dashboards.md) |
| Task Type | `FE` |

## Business Context

As a staff user, I want a dashboard focused on my role so that I can quickly find my pending work.

This task supports the module goal: Give each role the operational and financial visibility needed for daily work while enforcing query-layer data boundaries.

## Source Documents

- [Reporting and Dashboard Flow](../../../../business/flows/08_reporting_and_dashboard_flow.md)
- [Module Boundaries](../../../../architecture/module_boundaries.md)
- [Reports and Dashboards Design](../../../../design-guide/13-reports-and-dashboards.html)

## Acceptance Criteria Impact

- [ ] Consultant dashboard shows assigned files, pending documents, and upcoming tasks.
- [ ] Accounts dashboard shows pending confirmations, dues, and payments by period.
- [ ] Admission and Visa dashboards show stage queues, blockers, and submitted applications.

## Business Rules To Preserve

- Reports must use query-layer role scopes.
- Owner sees all reports.
- Commission appears only in Owner reports.

## Dependencies To Check First

- Depends on FIL, PAY, ADM, VIS, COM, and ACL query scopes.

## Implementation Plan

1. Locate or create the Role-Based Dashboard route or workspace section that owns this behavior.
2. Create typed UI models for the data needed by the story; keep field names aligned with the backend DTO/API contract.
3. Build the screen, panel, form, table, queue, or state component described by the task with loading, empty, success, and error states.
4. Apply role-aware behavior using authenticated user role and backend permission response; do not rely on visual hiding for security decisions.
5. Connect mutation actions to API calls only after backend contract exists; otherwise document the missing contract as a blocker.
6. Add user-visible validation for required fields, invalid transitions, duplicate warnings, and blocked workflow states mentioned by acceptance criteria.
7. Add frontend coverage for the happy path and at least one blocked/error path. Prefer Playwright for full role flows and component tests only for risky reusable pieces.
8. Test at least two roles: one allowed role and one restricted role.

## UI and Contract Expectations

- Frontend workspace: `Role-Based Dashboard`.
- Use Next.js, TypeScript, Tailwind CSS, and React Query patterns when implementation begins.
- Prefer API-driven permissions and response fields over hardcoded role assumptions.
- Required states: loading, empty, successful data, validation error, authorization-restricted, and server error.
- Design reference: `../../../../design-guide/13-reports-and-dashboards.html`.

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
Module: REP
Story: REP-EP1-US2
Completed task: REP-EP1-US2-FE2
Files changed:
Tests run:
Tracker updated:
Open blockers:
Next recommended task:
```
