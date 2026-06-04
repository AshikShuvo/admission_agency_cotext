# USR-EP2: Suspension and User Audit
## Detailed EPIC

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Module Context

| Field | Value |
|---|---|
| Module ID | `USR` |
| Module | User Management |
| Frontend Workspace | Owner Reports and Settings |
| Backend Module Boundary | Auth and Users |

## EPIC Goal

Deliver this capability area as a coherent business workflow, not as isolated screens or endpoints. The EPIC is complete only when every linked user story is accepted, tested, and reflected in the progress tracker.

## Functional Scope

- Owner can suspend staff access without deleting history.
- Suspended users cannot log in or access APIs.
- Active file reassignment warning appears for consultants.
- User lifecycle changes remain auditable.

## Business Rules To Preserve

- Only Owner manages staff users.
- Each user has one primary role unless explicitly approved.
- Suspension blocks access without deleting history.

## Dependencies

- Depends on ACL role model and audit logging.

## User Stories

- [ ] [USR-EP2-US1: Suspend Staff Access](../stories/USR-EP2-US1_suspend_staff_access.md)
- [ ] [USR-EP2-US2: Audit User Management Actions](../stories/USR-EP2-US2_audit_user_management_actions.md)

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
