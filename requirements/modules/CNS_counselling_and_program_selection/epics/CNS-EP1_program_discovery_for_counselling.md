# CNS-EP1: Program Discovery for Counselling
## Detailed EPIC

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Module Context

| Field | Value |
|---|---|
| Module ID | `CNS` |
| Module | Counselling and Program Selection |
| Frontend Workspace | Consultant File Workspace |
| Backend Module Boundary | Catalog, Students, Files / Cases |

## EPIC Goal

Deliver this capability area as a coherent business workflow, not as isolated screens or endpoints. The EPIC is complete only when every linked user story is accepted, tested, and reflected in the progress tracker.

## Functional Scope

- Consultant can search and filter active programs.
- Consultant can inspect university, program, intake, duration, and package summary.
- Search results exclude inactive programs and programs without active packages for file creation.

## Business Rules To Preserve

- Consultants cannot edit catalog records.
- File opening requires active package.
- Counselling can exist before formal file creation.

## Dependencies

- Depends on CAT active catalog and active package lookup.

## User Stories

- [ ] [CNS-EP1-US1: Search Active Programs](../stories/CNS-EP1-US1_search_active_programs.md)
- [ ] [CNS-EP1-US2: View Program and Package Details](../stories/CNS-EP1-US2_view_program_and_package_details.md)

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
