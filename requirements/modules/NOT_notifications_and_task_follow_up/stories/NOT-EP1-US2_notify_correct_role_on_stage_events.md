# NOT-EP1-US2: Notify Correct Role on Stage Events
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

As staff, I want the right department notified when files move stages so that work continues without manual handoff.

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

- [ ] New file created notifies Owner and Accounts.
- [ ] Payment confirmed notifies assigned Consultant and relevant department.
- [ ] File moved to Admission or Visa notifies the relevant department.

## Business Rules

- Notifications must respect role visibility.
- Consultants receive notifications only for assigned files.
- Commission notifications are Owner-only.

## Dependencies and Preconditions

- Depends on business events from FIL, PAY, ADM, VIS, and EXC.

## Frontend Tasks

- [ ] [NOT-EP1-US2-FE1](../tasks/NOT-EP1-US2-FE1.md): Add stage-event notification display with clear file number and next action.
- [ ] [NOT-EP1-US2-FE2](../tasks/NOT-EP1-US2-FE2.md): Add links from notification to the correct workspace route.
- [ ] [NOT-EP1-US2-FE3](../tasks/NOT-EP1-US2-FE3.md): Add tests for file-stage notification navigation.

## Backend Tasks

- [ ] [NOT-EP1-US2-BE1](../tasks/NOT-EP1-US2-BE1.md): Wire notification events from file creation, payment confirmation, admission approval, and visa outcome services.
- [ ] [NOT-EP1-US2-BE2](../tasks/NOT-EP1-US2-BE2.md): Resolve target users by role, department, and assigned consultant.
- [ ] [NOT-EP1-US2-BE3](../tasks/NOT-EP1-US2-BE3.md): Add integration tests for notification targets across lifecycle events.

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
