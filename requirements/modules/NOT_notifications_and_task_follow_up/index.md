# Notifications and Task Follow-up
## Independent Requirement Module Folder

Module ID: `NOT`

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Module Goal

Create role-aware in-app notifications and task follow-up items when important business events occur, while respecting file assignment and data visibility rules.

## Primary Actors

- System
- Consultant
- Accounts
- Admission
- Visa
- Owner
- Student, optional future SMS/email recipient

## Source Documents

- [Notifications and Communication Flow](../../../business/flows/09_notifications_and_communication_flow.md)
- [Module Boundaries](../../../architecture/module_boundaries.md)
- [Notification Task Center Design](../../../design-guide/17-notification-task-center.html)

## Architecture Routing

| Area | Owner |
|---|---|
| Frontend workspace | Role-Based Dashboard |
| Backend module boundary | Notifications |
| Design reference | ../../../design-guide/17-notification-task-center.html |

## Business Rules

- Notifications must respect role visibility.
- Consultants receive notifications only for assigned files.
- Commission notifications are Owner-only.

## Dependencies

- Depends on business events from FIL, PAY, ADM, VIS, and EXC.

## EPIC Files

- [ ] [NOT-EP1: Business Event Notifications](epics/NOT-EP1_business_event_notifications.md)
- [ ] [NOT-EP2: Task Center and Follow-up](epics/NOT-EP2_task_center_and_follow_up.md)

## User Story Files

- [ ] [NOT-EP1-US1: Create In-App Notification from Business Event](stories/NOT-EP1-US1_create_in_app_notification_from_business_event.md)
- [ ] [NOT-EP1-US2: Notify Correct Role on Stage Events](stories/NOT-EP1-US2_notify_correct_role_on_stage_events.md)
- [ ] [NOT-EP2-US1: View My Task Center](stories/NOT-EP2-US1_view_my_task_center.md)
- [ ] [NOT-EP2-US2: Mark Notification Read or Resolved](stories/NOT-EP2-US2_mark_notification_read_or_resolved.md)

## Task Implementation Plans

- [ ] [NOT-EP1-US1-FE1](tasks/NOT-EP1-US1-FE1.md): Build notification indicator and recent notification list in the app shell.
- [ ] [NOT-EP1-US1-FE2](tasks/NOT-EP1-US1-FE2.md): Add notification item states for unread, read, linked file, and restricted file.
- [ ] [NOT-EP1-US1-FE3](tasks/NOT-EP1-US1-FE3.md): Add tests for role-specific notification rendering.
- [ ] [NOT-EP1-US1-BE1](tasks/NOT-EP1-US1-BE1.md): Create notification entity with event type, target, file link, read state, and metadata.
- [ ] [NOT-EP1-US1-BE2](tasks/NOT-EP1-US1-BE2.md): Implement notification creation service callable by business modules after important actions.
- [ ] [NOT-EP1-US1-BE3](tasks/NOT-EP1-US1-BE3.md): Add tests for event creation, target selection, and commission owner-only routing.
- [ ] [NOT-EP1-US2-FE1](tasks/NOT-EP1-US2-FE1.md): Add stage-event notification display with clear file number and next action.
- [ ] [NOT-EP1-US2-FE2](tasks/NOT-EP1-US2-FE2.md): Add links from notification to the correct workspace route.
- [ ] [NOT-EP1-US2-FE3](tasks/NOT-EP1-US2-FE3.md): Add tests for file-stage notification navigation.
- [ ] [NOT-EP1-US2-BE1](tasks/NOT-EP1-US2-BE1.md): Wire notification events from file creation, payment confirmation, admission approval, and visa outcome services.
- [ ] [NOT-EP1-US2-BE2](tasks/NOT-EP1-US2-BE2.md): Resolve target users by role, department, and assigned consultant.
- [ ] [NOT-EP1-US2-BE3](tasks/NOT-EP1-US2-BE3.md): Add integration tests for notification targets across lifecycle events.
- [ ] [NOT-EP2-US1-FE1](tasks/NOT-EP2-US1-FE1.md): Build task center page with filters, unread count, and result list.
- [ ] [NOT-EP2-US1-FE2](tasks/NOT-EP2-US1-FE2.md): Add quick navigation from a task to the related file or workspace.
- [ ] [NOT-EP2-US1-FE3](tasks/NOT-EP2-US1-FE3.md): Add tests for task filtering and role-scoped results.
- [ ] [NOT-EP2-US1-BE1](tasks/NOT-EP2-US1-BE1.md): Implement task center list API with filters and pagination.
- [ ] [NOT-EP2-US1-BE2](tasks/NOT-EP2-US1-BE2.md): Apply target-user and role-scope filters at query layer.
- [ ] [NOT-EP2-US1-BE3](tasks/NOT-EP2-US1-BE3.md): Add tests for filters, unread counts, and scoped task access.
- [ ] [NOT-EP2-US2-FE1](tasks/NOT-EP2-US2-FE1.md): Add mark-read and resolve actions to notification and task rows.
- [ ] [NOT-EP2-US2-FE2](tasks/NOT-EP2-US2-FE2.md): Update unread counts without a full page refresh.
- [ ] [NOT-EP2-US2-FE3](tasks/NOT-EP2-US2-FE3.md): Add tests for read and resolved transitions.
- [ ] [NOT-EP2-US2-BE1](tasks/NOT-EP2-US2-BE1.md): Implement read and resolve mutation APIs with actor metadata.
- [ ] [NOT-EP2-US2-BE2](tasks/NOT-EP2-US2-BE2.md): Enforce ownership and role authorization for notification mutations.
- [ ] [NOT-EP2-US2-BE3](tasks/NOT-EP2-US2-BE3.md): Add tests for unauthorized resolve attempts and timestamp persistence.

## Folder Completion Rules

- [ ] Every EPIC file is complete.
- [ ] Every story file is accepted.
- [ ] Every task implementation plan is completed or explicitly deferred with an approved blocker.
- [ ] Module row is updated in [Progress Tracker](../../progress_tracker.md).
- [ ] Completion log records meaningful milestone completion.
