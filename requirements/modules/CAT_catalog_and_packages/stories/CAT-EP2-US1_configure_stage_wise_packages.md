# CAT-EP2-US1: Configure Stage-wise Packages
## Detailed User Story

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `CAT` - Catalog and Packages |
| EPIC | [CAT-EP2: Package and Fee Configuration](../epics/CAT-EP2_package_and_fee_configuration.md) |

## Story Statement

As an Owner, I want to configure stage-wise package fees so that each program has a clear cost structure before counselling starts.

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

- [ ] Package line items are assigned to File Opening, Admission, or Visa.
- [ ] Stage totals and total package cost are calculated automatically.
- [ ] Owner can save draft packages before activation.

## Business Rules

- Only Owner can mutate catalog records.
- Consultants browse active records only.
- Only one active package is allowed per program.
- File creation must snapshot active package fees.

## Dependencies and Preconditions

- None for core catalog setup. It is an upstream dependency for counselling and file opening.

## Frontend Tasks

- [ ] [CAT-EP2-US1-FE1](../tasks/CAT-EP2-US1-FE1.md): Build package editor with grouped fee line item sections for each processing stage.
- [ ] [CAT-EP2-US1-FE2](../tasks/CAT-EP2-US1-FE2.md): Show automatic stage totals, total package cost, and validation for missing or negative amounts.
- [ ] [CAT-EP2-US1-FE3](../tasks/CAT-EP2-US1-FE3.md): Add frontend tests for adding, editing, removing, and validating fee line items.

## Backend Tasks

- [ ] [CAT-EP2-US1-BE1](../tasks/CAT-EP2-US1-BE1.md): Create package and package fee line item entities with stage enum and amount validation.
- [ ] [CAT-EP2-US1-BE2](../tasks/CAT-EP2-US1-BE2.md): Implement package draft save and calculated summary APIs.
- [ ] [CAT-EP2-US1-BE3](../tasks/CAT-EP2-US1-BE3.md): Add tests for stage totals, invalid fee amounts, and package line item persistence.

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
