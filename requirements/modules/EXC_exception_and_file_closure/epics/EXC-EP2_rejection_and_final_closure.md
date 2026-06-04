# EXC-EP2: Rejection and Final Closure
## Detailed EPIC

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Module Context

| Field | Value |
|---|---|
| Module ID | `EXC` |
| Module | Exception and File Closure |
| Frontend Workspace | File Detail Workspaces |
| Backend Module Boundary | Files / Cases |

## EPIC Goal

Deliver this capability area as a coherent business workflow, not as isolated screens or endpoints. The EPIC is complete only when every linked user story is accepted, tested, and reflected in the progress tracker.

## Functional Scope

- Visa rejection records reason and preserves visa history.
- Owner decides whether reapplication is allowed.
- Completed files are locked and eligible for commission tracking.

## Business Rules To Preserve

- Files are not deleted.
- Cancelled and completed files are locked from normal edits.
- Visa reapplication preserves previous history.

## Dependencies

- Depends on FIL status model, VIS rejection, and COM completion eligibility.

## User Stories

- [ ] [EXC-EP2-US1: Review Visa Rejection and Reapplication](../stories/EXC-EP2-US1_review_visa_rejection_and_reapplication.md)
- [ ] [EXC-EP2-US2: Lock Completed Files](../stories/EXC-EP2-US2_lock_completed_files.md)

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
