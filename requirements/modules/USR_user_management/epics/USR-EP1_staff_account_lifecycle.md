# USR-EP1: Staff Account Lifecycle
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

- Owner can create staff users with exactly one primary role.
- Owner can update staff details, department, role, and active status.
- Role scope preview is shown before changes are confirmed.
- User management actions are audited.

## Business Rules To Preserve

- Only Owner manages staff users.
- Each user has one primary role unless explicitly approved.
- Suspension blocks access without deleting history.

## Dependencies

- Depends on ACL role model and audit logging.

## User Stories

- [ ] [USR-EP1-US1: Create Staff User](../stories/USR-EP1-US1_create_staff_user.md)
- [ ] [USR-EP1-US2: Update Staff Details and Role](../stories/USR-EP1-US2_update_staff_details_and_role.md)

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
