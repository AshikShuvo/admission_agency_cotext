# CAT-EP1: Master Catalog Management
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

- Owner can create, edit, activate, and deactivate destination countries.
- Owner can create and maintain partner universities under a country.
- Owner can create and maintain university programs.
- Consultants can browse active catalog records without editing them.

## Business Rules To Preserve

- Only Owner can mutate catalog records.
- Consultants browse active records only.
- Only one active package is allowed per program.
- File creation must snapshot active package fees.

## Dependencies

- None for core catalog setup. It is an upstream dependency for counselling and file opening.

## User Stories

- [ ] [CAT-EP1-US1: Manage Countries and Universities](../stories/CAT-EP1-US1_manage_countries_and_universities.md)
- [ ] [CAT-EP1-US2: Manage Programs](../stories/CAT-EP1-US2_manage_programs.md)

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
