# ACL-EP2: Data Scope and Sensitive Field Filtering
## Detailed EPIC

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Module Context

| Field | Value |
|---|---|
| Module ID | `ACL` |
| Module | Access Control and Role Visibility |
| Frontend Workspace | All Workspaces |
| Backend Module Boundary | Auth and Users |

## EPIC Goal

Deliver this capability area as a coherent business workflow, not as isolated screens or endpoints. The EPIC is complete only when every linked user story is accepted, tested, and reflected in the progress tracker.

## Functional Scope

- Owner can access all files and reports.
- Consultant can access assigned files only.
- Accounts can access financial records and limited file identifiers.
- Admission and Visa can access only relevant stage data.
- Commission fields are removed from all non-owner responses.

## Business Rules To Preserve

- Backend authorization is mandatory.
- UI hiding is not enough.
- Sensitive fields are filtered by role.

## Dependencies

- Depends on role model from business/users_and_roles.md and applies to all modules.

## User Stories

- [ ] [ACL-EP2-US1: Apply Query-Level Data Scope](../stories/ACL-EP2-US1_apply_query_level_data_scope.md)
- [ ] [ACL-EP2-US2: Filter Sensitive Fields](../stories/ACL-EP2-US2_filter_sensitive_fields.md)

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
