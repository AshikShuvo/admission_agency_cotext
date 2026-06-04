# NOT-EP1: Business Event Notifications
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

- System creates notifications for file creation, payment confirmation, document requests, document submissions, stage changes, visa outcomes, and completion.
- Notifications are linked to file, stage, actor, and target role.
- Notifications respect access control and consultant assignment.

## Business Rules To Preserve

- Notifications must respect role visibility.
- Consultants receive notifications only for assigned files.
- Commission notifications are Owner-only.

## Dependencies

- Depends on business events from FIL, PAY, ADM, VIS, and EXC.

## User Stories

- [ ] [NOT-EP1-US1: Create In-App Notification from Business Event](../stories/NOT-EP1-US1_create_in_app_notification_from_business_event.md)
- [ ] [NOT-EP1-US2: Notify Correct Role on Stage Events](../stories/NOT-EP1-US2_notify_correct_role_on_stage_events.md)

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
