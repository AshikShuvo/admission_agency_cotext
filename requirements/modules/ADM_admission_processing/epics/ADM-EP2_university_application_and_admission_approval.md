# ADM-EP2: University Application and Admission Approval
## Detailed EPIC

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Module Context

| Field | Value |
|---|---|
| Module ID | `ADM` |
| Module | Admission Processing |
| Frontend Workspace | Admission Workspace |
| Backend Module Boundary | Admission, Documents |

## EPIC Goal

Deliver this capability area as a coherent business workflow, not as isolated screens or endpoints. The EPIC is complete only when every linked user story is accepted, tested, and reflected in the progress tracker.

## Functional Scope

- Admission submits university applications only when documents and payments are clear.
- Offer letters are uploaded and linked to the file.
- Admission approval moves the file to Visa Processing.

## Business Rules To Preserve

- Admission approval requires documents and payment clearance.
- Admission users cannot see commission data.
- All document status changes are logged.

## Dependencies

- Depends on FIL file status and PAY clearance.

## User Stories

- [ ] [ADM-EP2-US1: Submit University Application](../stories/ADM-EP2-US1_submit_university_application.md)
- [ ] [ADM-EP2-US2: Upload Offer Letter and Approve Admission](../stories/ADM-EP2-US2_upload_offer_letter_and_approve_admission.md)

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
