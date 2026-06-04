# NOT-EP2: Task Center and Follow-up
## Detailed EPIC

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Module Context

| Field | Value |
|---|---|
| Module ID | `NOT` |
| Module | Notifications and Task Follow-up |
| Frontend Workspace | Role-Based Dashboard |
| Backend Module Boundary | Notifications |

## EPIC Goal

Deliver this capability area as a coherent business workflow, not as isolated screens or endpoints. The EPIC is complete only when every linked user story is accepted, tested, and reflected in the progress tracker.

## Functional Scope

- Users can view pending task-like notifications.
- Users can mark notifications read or resolved.
- Follow-up tasks remain linked to the file and business stage.

## Business Rules To Preserve

- Notifications must respect role visibility.
- Consultants receive notifications only for assigned files.
- Commission notifications are Owner-only.

## Dependencies

- Depends on business events from FIL, PAY, ADM, VIS, and EXC.

## User Stories

- [ ] [NOT-EP2-US1: View My Task Center](../stories/NOT-EP2-US1_view_my_task_center.md)
- [ ] [NOT-EP2-US2: Mark Notification Read or Resolved](../stories/NOT-EP2-US2_mark_notification_read_or_resolved.md)

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
