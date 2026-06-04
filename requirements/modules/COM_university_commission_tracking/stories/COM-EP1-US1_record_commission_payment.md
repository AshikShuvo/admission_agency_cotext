# COM-EP1-US1: Record Commission Payment
## Detailed User Story

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `COM` - University Commission Tracking |
| EPIC | [COM-EP1: Owner-only Commission Records](../epics/COM-EP1_owner_only_commission_records.md) |

## Story Statement

As an Owner, I want to record commission received from a university so that agency revenue is complete.

## Business Expectation

This story must convert the business expectation into a working system behavior that staff can use without relying on manual spreadsheets, side notes, or hidden process knowledge. The implementation must preserve the role boundaries, lifecycle rules, and data ownership described in the source business flow.

## Primary Actors

- Owner
- University

## Source Documents

- [University Commission Tracking Flow](../../../../business/flows/07_university_commission_tracking_flow.md)
- [Module Boundaries](../../../../architecture/module_boundaries.md)
- [Commission Tracking Design](../../../../design-guide/12-commission-tracking.html)

## Acceptance Criteria

- [ ] Commission record links file, university, amount, received date, and notes.
- [ ] Commission can be recorded only by Owner.
- [ ] Commission can be linked only to eligible completed or enrolled files unless Owner records an exception note.

## Business Rules

- Commission is Owner-only.
- Commission records link to file and university.
- Non-owner responses must exclude commission data.

## Dependencies and Preconditions

- Depends on VIS completion/enrollment and ACL Owner-only access.

## Frontend Tasks

- [ ] [COM-EP1-US1-FE1](../tasks/COM-EP1-US1-FE1.md): Build owner-only commission entry form with file and university lookup.
- [ ] [COM-EP1-US1-FE2](../tasks/COM-EP1-US1-FE2.md): Add eligibility warning for non-completed files and required exception note.
- [ ] [COM-EP1-US1-FE3](../tasks/COM-EP1-US1-FE3.md): Add tests that non-owner workspaces never render commission entry.

## Backend Tasks

- [ ] [COM-EP1-US1-BE1](../tasks/COM-EP1-US1-BE1.md): Create commission entity linked to file, university, and owner actor.
- [ ] [COM-EP1-US1-BE2](../tasks/COM-EP1-US1-BE2.md): Implement owner-only create/update APIs with eligibility validation.
- [ ] [COM-EP1-US1-BE3](../tasks/COM-EP1-US1-BE3.md): Add tests for owner-only access, eligibility rules, and persistence.

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
