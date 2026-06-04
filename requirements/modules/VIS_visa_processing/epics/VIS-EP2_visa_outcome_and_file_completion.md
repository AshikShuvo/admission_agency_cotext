# VIS-EP2: Visa Outcome and File Completion
## Detailed EPIC

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Module Context

| Field | Value |
|---|---|
| Module ID | `VIS` |
| Module | Visa Processing |
| Frontend Workspace | Visa Workspace |
| Backend Module Boundary | Visa, Documents |

## EPIC Goal

Deliver this capability area as a coherent business workflow, not as isolated screens or endpoints. The EPIC is complete only when every linked user story is accepted, tested, and reflected in the progress tracker.

## Functional Scope

- Visa department records approval or rejection.
- Approved visa records issue and expiry dates.
- Rejection preserves history and supports Owner reapplication decision.
- Completed files become locked except Owner-authorized changes.

## Business Rules To Preserve

- Visa approval/completion requires documents and payment clearance.
- Visa rejection preserves history.
- Visa users cannot see commission data.

## Dependencies

- Depends on ADM approval, offer letter, and PAY clearance.

## User Stories

- [ ] [VIS-EP2-US1: Record Visa Outcome](../stories/VIS-EP2-US1_record_visa_outcome.md)
- [ ] [VIS-EP2-US2: Complete Student File](../stories/VIS-EP2-US2_complete_student_file.md)

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
