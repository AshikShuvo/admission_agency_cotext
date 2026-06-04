# CNS-EP1-US1: Search Active Programs
## Detailed User Story

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `CNS` - Counselling and Program Selection |
| EPIC | [CNS-EP1: Program Discovery for Counselling](../epics/CNS-EP1_program_discovery_for_counselling.md) |

## Story Statement

As a Consultant, I want to search active programs by counselling criteria so that I can find suitable options for a student.

## Business Expectation

This story must convert the business expectation into a working system behavior that staff can use without relying on manual spreadsheets, side notes, or hidden process knowledge. The implementation must preserve the role boundaries, lifecycle rules, and data ownership described in the source business flow.

## Primary Actors

- Consultant
- Student
- Owner, oversight

## Source Documents

- [Counselling and Program Selection Flow](../../../../business/flows/02_counselling_and_program_selection_flow.md)
- [Module Boundaries](../../../../architecture/module_boundaries.md)
- [Counselling Program Selection Design](../../../../design-guide/06-counselling-program-selection.html)

## Acceptance Criteria

- [ ] Consultant can filter by country, university, level, field, intake, and active status.
- [ ] Results clearly show whether a program has an active package.
- [ ] Consultant cannot edit catalog data from counselling screens.

## Business Rules

- Consultants cannot edit catalog records.
- File opening requires active package.
- Counselling can exist before formal file creation.

## Dependencies and Preconditions

- Depends on CAT active catalog and active package lookup.

## Frontend Tasks

- [ ] [CNS-EP1-US1-FE1](../tasks/CNS-EP1-US1-FE1.md): Build searchable program browser with filters and result list.
- [ ] [CNS-EP1-US1-FE2](../tasks/CNS-EP1-US1-FE2.md): Add empty, loading, no-package, and read-only states.
- [ ] [CNS-EP1-US1-FE3](../tasks/CNS-EP1-US1-FE3.md): Add frontend tests for filtering and read-only catalog behavior.

## Backend Tasks

- [ ] [CNS-EP1-US1-BE1](../tasks/CNS-EP1-US1-BE1.md): Add program search API with filters and active-package indicator.
- [ ] [CNS-EP1-US1-BE2](../tasks/CNS-EP1-US1-BE2.md): Enforce consultant read-only access and active catalog visibility rules.
- [ ] [CNS-EP1-US1-BE3](../tasks/CNS-EP1-US1-BE3.md): Add tests for search filters, role access, and no-package indicators.

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
