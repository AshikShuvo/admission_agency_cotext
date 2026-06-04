# CAT-EP2: Package and Fee Configuration
## Detailed EPIC

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Module Context

| Field | Value |
|---|---|
| Module ID | `CAT` |
| Module | Catalog and Packages |
| Frontend Workspace | Catalog Management |
| Backend Module Boundary | Catalog |

## EPIC Goal

Deliver this capability area as a coherent business workflow, not as isolated screens or endpoints. The EPIC is complete only when every linked user story is accepted, tested, and reflected in the progress tracker.

## Functional Scope

- Owner can configure one active package per program.
- Package line items are grouped by file opening, admission, and visa stages.
- System calculates stage totals and total package cost.
- File creation receives a snapshot of the active package.

## Business Rules To Preserve

- Only Owner can mutate catalog records.
- Consultants browse active records only.
- Only one active package is allowed per program.
- File creation must snapshot active package fees.

## Dependencies

- None for core catalog setup. It is an upstream dependency for counselling and file opening.

## User Stories

- [ ] [CAT-EP2-US1: Configure Stage-wise Packages](../stories/CAT-EP2-US1_configure_stage_wise_packages.md)
- [ ] [CAT-EP2-US2: Activate One Package per Program](../stories/CAT-EP2-US2_activate_one_package_per_program.md)

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
