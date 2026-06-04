# FIL-EP1: Student Profile and File Creation
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

- Consultant records student identity, guardian, academic, passport, and contact details.
- System creates a unique human-readable file number.
- File is assigned to the creating consultant unless Owner assigns otherwise.

## Business Rules To Preserve

- Consultants only manage assigned files.
- File numbers are unique.
- Package fees are copied at creation time.
- File history is preserved.

## Dependencies

- Depends on CAT active package and CNS selected program context.

## User Stories

- [ ] [FIL-EP1-US1: Register Student Profile](../stories/FIL-EP1-US1_register_student_profile.md)
- [ ] [FIL-EP1-US2: Create Student File](../stories/FIL-EP1-US2_create_student_file.md)

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
