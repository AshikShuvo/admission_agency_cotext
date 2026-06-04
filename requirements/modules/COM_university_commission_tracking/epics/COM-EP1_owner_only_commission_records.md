# COM-EP1: Owner-only Commission Records
## Detailed EPIC

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Module Context

| Field | Value |
|---|---|
| Module ID | `COM` |
| Module | University Commission Tracking |
| Frontend Workspace | Owner Reports and Settings |
| Backend Module Boundary | Commissions |

## EPIC Goal

Deliver this capability area as a coherent business workflow, not as isolated screens or endpoints. The EPIC is complete only when every linked user story is accepted, tested, and reflected in the progress tracker.

## Functional Scope

- Owner can create commission records linked to student file and university.
- Commission can use default university rate or student-specific override.
- Non-owner users cannot see commission data.

## Business Rules To Preserve

- Commission is Owner-only.
- Commission records link to file and university.
- Non-owner responses must exclude commission data.

## Dependencies

- Depends on VIS completion/enrollment and ACL Owner-only access.

## User Stories

- [ ] [COM-EP1-US1: Record Commission Payment](../stories/COM-EP1-US1_record_commission_payment.md)
- [ ] [COM-EP1-US2: Protect Commission Confidentiality](../stories/COM-EP1-US2_protect_commission_confidentiality.md)

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
