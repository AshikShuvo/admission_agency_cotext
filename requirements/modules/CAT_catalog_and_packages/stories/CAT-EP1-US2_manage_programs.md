# CAT-EP1-US2: Manage Programs
## Detailed User Story

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `CAT` - Catalog and Packages |
| EPIC | [CAT-EP1: Master Catalog Management](../epics/CAT-EP1_master_catalog_management.md) |

## Story Statement

As an Owner, I want to manage programs under universities so that consultants can select the correct study option for a student.

## Business Expectation

This story must convert the business expectation into a working system behavior that staff can use without relying on manual spreadsheets, side notes, or hidden process knowledge. The implementation must preserve the role boundaries, lifecycle rules, and data ownership described in the source business flow.

## Primary Actors

- Owner / Admin
- Consultant, read-only
- Accounts, limited package view when linked to a file

## Source Documents

- [Catalog and Package Setup Flow](../../../../business/flows/01_catalog_and_package_setup_flow.md)
- [Module Boundaries](../../../../architecture/module_boundaries.md)
- [Catalog Package Management Design](../../../../design-guide/05-catalog-package-management.html)

## Acceptance Criteria

- [ ] Programs are linked to exactly one university.
- [ ] Program details include level, field of study, duration, intake, and entry requirement notes.
- [ ] Inactive programs cannot be selected for new files.

## Business Rules

- Only Owner can mutate catalog records.
- Consultants browse active records only.
- Only one active package is allowed per program.
- File creation must snapshot active package fees.

## Dependencies and Preconditions

- None for core catalog setup. It is an upstream dependency for counselling and file opening.

## Frontend Tasks

- [ ] [CAT-EP1-US2-FE1](../tasks/CAT-EP1-US2-FE1.md): Build program table and program form scoped to the selected university.
- [ ] [CAT-EP1-US2-FE2](../tasks/CAT-EP1-US2-FE2.md): Add filters for country, university, program level, field, and active status.
- [ ] [CAT-EP1-US2-FE3](../tasks/CAT-EP1-US2-FE3.md): Add frontend coverage for creating, editing, filtering, and read-only browsing.

## Backend Tasks

- [ ] [CAT-EP1-US2-BE1](../tasks/CAT-EP1-US2-BE1.md): Create program entity linked to university with searchable fields and active status.
- [ ] [CAT-EP1-US2-BE2](../tasks/CAT-EP1-US2-BE2.md): Implement program CRUD, browse, and filter APIs with owner-only mutation guards.
- [ ] [CAT-EP1-US2-BE3](../tasks/CAT-EP1-US2-BE3.md): Add tests for university ownership, active filtering, and program selection eligibility.

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
