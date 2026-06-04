# NOT-EP1-US1: Create In-App Notification from Business Event
## Detailed User Story

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `NOT` - Notifications and Task Follow-up |
| EPIC | [NOT-EP1: Business Event Notifications](../epics/NOT-EP1_business_event_notifications.md) |

## Story Statement

As the system, I want to create notifications from important business events so that the responsible role knows what happened.

## Business Expectation

This story must convert the business expectation into a working system behavior that staff can use without relying on manual spreadsheets, side notes, or hidden process knowledge. The implementation must preserve the role boundaries, lifecycle rules, and data ownership described in the source business flow.

## Primary Actors

- System
- Consultant
- Accounts
- Admission
- Visa
- Owner
- Student, optional future SMS/email recipient

## Source Documents

- [Notifications and Communication Flow](../../../../business/flows/09_notifications_and_communication_flow.md)
- [Module Boundaries](../../../../architecture/module_boundaries.md)
- [Notification Task Center Design](../../../../design-guide/17-notification-task-center.html)

## Acceptance Criteria

- [ ] Notification records include event type, target user or role, file link, message, read state, and timestamp.
- [ ] Consultant notifications are limited to assigned files.
- [ ] Commission-related notifications are Owner-only.

## Business Rules

- Notifications must respect role visibility.
- Consultants receive notifications only for assigned files.
- Commission notifications are Owner-only.

## Dependencies and Preconditions

- Depends on business events from FIL, PAY, ADM, VIS, and EXC.

## Frontend Tasks

- [ ] [NOT-EP1-US1-FE1](../tasks/NOT-EP1-US1-FE1.md): Build notification indicator and recent notification list in the app shell.
- [ ] [NOT-EP1-US1-FE2](../tasks/NOT-EP1-US1-FE2.md): Add notification item states for unread, read, linked file, and restricted file.
- [ ] [NOT-EP1-US1-FE3](../tasks/NOT-EP1-US1-FE3.md): Add tests for role-specific notification rendering.

## Backend Tasks

- [ ] [NOT-EP1-US1-BE1](../tasks/NOT-EP1-US1-BE1.md): Create notification entity with event type, target, file link, read state, and metadata.
- [ ] [NOT-EP1-US1-BE2](../tasks/NOT-EP1-US1-BE2.md): Implement notification creation service callable by business modules after important actions.
- [ ] [NOT-EP1-US1-BE3](../tasks/NOT-EP1-US1-BE3.md): Add tests for event creation, target selection, and commission owner-only routing.

## Cross-Agent Contract

- Backend owns persistence, authorization, workflow gates, audit events, and role-scoped API responses.
- Frontend owns the staff-facing workflow, visible states, validation feedback, and clear blocked-state messaging.
- QA/review owns acceptance verification across frontend, backend, and access-control behavior.
- If the frontend and backend agents disagree on API shape, pause the story and add a blocker to [Progress Tracker](../../../progress_tracker.md).

## Detailed Acceptance Review Checklist

- [ ] User can complete the happy path described by the story statement.
- [ ] User sees clear feedback when required data is missing or a workflow gate blocks progress.
- [ ] Unauthorized roles cannot perform the action through UI or API.
- [ ] Restricted data is not returned from the backend and is not rendered by the frontend.
- [ ] Important state changes create audit log or notification events where required by the business rules.
- [ ] Automated tests cover the success path and at least one failure or restricted path.

## Completion Rules

- [ ] All linked frontend tasks are complete.
- [ ] All linked backend tasks are complete.
- [ ] Acceptance criteria are verified by QA/review.
- [ ] Story count is updated in [Progress Tracker](../../../progress_tracker.md).
- [ ] EPIC progress is recalculated after this story is accepted.
