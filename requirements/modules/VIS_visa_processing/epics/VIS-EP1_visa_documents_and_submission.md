# VIS-EP1: Visa Documents and Submission
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

- Visa department generates visa checklist after admission approval.
- Consultant and student provide visa documents.
- Visa department verifies documents and submits the visa application only when documents and payments are clear.

## Business Rules To Preserve

- Visa approval/completion requires documents and payment clearance.
- Visa rejection preserves history.
- Visa users cannot see commission data.

## Dependencies

- Depends on ADM approval, offer letter, and PAY clearance.

## User Stories

- [ ] [VIS-EP1-US1: Generate Visa Checklist](../stories/VIS-EP1-US1_generate_visa_checklist.md)
- [ ] [VIS-EP1-US2: Submit Visa Application](../stories/VIS-EP1-US2_submit_visa_application.md)

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
