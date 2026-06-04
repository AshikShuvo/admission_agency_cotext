# REP-EP2-US2-BE3: Add tests for financial aggregate accuracy and commission exclusion.
## Detailed Backend Task Plan

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `REP` - Reporting and Dashboards |
| EPIC | [REP-EP2: Operational Reports](../epics/REP-EP2_operational_reports.md) |
| User Story | [REP-EP2-US2: View Financial and Due Reports](../stories/REP-EP2-US2_view_financial_and_due_reports.md) |
| Task Type | `BE` |

## Business Context

As Owner or Accounts, I want financial and due reports so that payment follow-up is accurate.

This task supports the module goal: Give each role the operational and financial visibility needed for daily work while enforcing query-layer data boundaries.

## Source Documents

- [Reporting and Dashboard Flow](../../../../business/flows/08_reporting_and_dashboard_flow.md)
- [Module Boundaries](../../../../architecture/module_boundaries.md)
- [Reports and Dashboards Design](../../../../design-guide/13-reports-and-dashboards.html)

## Acceptance Criteria Impact

- [ ] Accounts can see payment totals, dues, and pending confirmations.
- [ ] Owner can see all financial reports and commission summaries.
- [ ] Commission data is excluded from Accounts reports.

## Business Rules To Preserve

- Reports must use query-layer role scopes.
- Owner sees all reports.
- Commission appears only in Owner reports.

## Dependencies To Check First

- Depends on FIL, PAY, ADM, VIS, COM, and ACL query scopes.

## Implementation Plan

1. Implement inside the NestJS Reporting ownership boundary unless an explicit dependency requires another module.
2. Define or update Prisma/NestJS entities, DTOs, enums, and validation rules needed by the task.
3. Implement service-layer business logic first; controllers should stay thin and call typed service methods.
4. Apply authorization guards and query-level scope filters before reading or mutating protected records.
5. Persist audit log or notification events when the task changes sensitive business state.
6. Return role-appropriate response shapes and exclude sensitive fields for restricted roles.
7. Add unit tests for business rules and integration tests for API behavior, persistence, and authorization.
8. Include fixtures for allowed and blocked roles, valid and invalid inputs, and important workflow states.
9. Add transaction-safe checks so the workflow cannot advance when required payment, document, or status prerequisites fail.

## Backend Contract Expectations

- Backend module ownership: `Reporting`.
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
Module: REP
Story: REP-EP2-US2
Completed task: REP-EP2-US2-BE3
Files changed:
Tests run:
Tracker updated:
Open blockers:
Next recommended task:
```
