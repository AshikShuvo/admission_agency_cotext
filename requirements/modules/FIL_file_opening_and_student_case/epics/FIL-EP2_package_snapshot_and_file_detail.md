# FIL-EP2: Package Snapshot and File Detail
## Detailed EPIC

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Module Context

| Field | Value |
|---|---|
| Module ID | `FIL` |
| Module | File Opening and Student Case |
| Frontend Workspace | Consultant File Workspace |
| Backend Module Boundary | Students, Files / Cases, File Fees |

## EPIC Goal

Deliver this capability area as a coherent business workflow, not as isolated screens or endpoints. The EPIC is complete only when every linked user story is accepted, tested, and reflected in the progress tracker.

## Functional Scope

- Active package fees are copied to file-specific fee records.
- Later catalog package changes do not affect existing files.
- File detail shows stage, payments, documents, history, and next action.

## Business Rules To Preserve

- Consultants only manage assigned files.
- File numbers are unique.
- Package fees are copied at creation time.
- File history is preserved.

## Dependencies

- Depends on CAT active package and CNS selected program context.

## User Stories

- [ ] [FIL-EP2-US1: Snapshot Package Fees](../stories/FIL-EP2-US1_snapshot_package_fees.md)
- [ ] [FIL-EP2-US2: View Student File Detail](../stories/FIL-EP2-US2_view_student_file_detail.md)

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
