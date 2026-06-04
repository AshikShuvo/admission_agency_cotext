# REP-EP1: Role-Based Dashboards
## Detailed EPIC

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Module Context

| Field | Value |
|---|---|
| Module ID | `REP` |
| Module | Reporting and Dashboards |
| Frontend Workspace | Role-Based Dashboard |
| Backend Module Boundary | Reporting |

## EPIC Goal

Deliver this capability area as a coherent business workflow, not as isolated screens or endpoints. The EPIC is complete only when every linked user story is accepted, tested, and reflected in the progress tracker.

## Functional Scope

- Owner sees whole-business metrics.
- Consultant sees only assigned files and tasks.
- Accounts sees payments, dues, and pending confirmations.
- Admission and Visa see their stage queues and blockers.

## Business Rules To Preserve

- Reports must use query-layer role scopes.
- Owner sees all reports.
- Commission appears only in Owner reports.

## Dependencies

- Depends on FIL, PAY, ADM, VIS, COM, and ACL query scopes.

## User Stories

- [ ] [REP-EP1-US1: Owner Dashboard](../stories/REP-EP1-US1_owner_dashboard.md)
- [ ] [REP-EP1-US2: Staff Dashboards](../stories/REP-EP1-US2_staff_dashboards.md)

## Implementation Expectations

- Frontend and backend agents should work story by story.
- Backend contracts should be stabilized before frontend final integration.
- Access control must be implemented in backend services and query scopes, not only by hiding UI elements.
- Task completion must be reflected in task files, story files, this EPIC file, and [Progress Tracker](../../../progress_tracker.md).

## EPIC Acceptance Criteria

- [ ] All linked user stories are complete.
- [ ] All frontend and backend tasks under those stories are complete.
- [ ] Automated tests cover the highest-risk workflow rules in this EPIC.
- [ ] Role access and sensitive-data behavior are verified.
- [ ] No open blocker remains for this EPIC.
- [ ] EPIC completion is recorded in [Progress Tracker](../../../progress_tracker.md).
