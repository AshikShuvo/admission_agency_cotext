# PAY-EP2: Due Calculation and Stage Gates
## Detailed EPIC

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Module Context

| Field | Value |
|---|---|
| Module ID | `PAY` |
| Module | Payments and Financial Clearance |
| Frontend Workspace | Accounts Payment Workspace |
| Backend Module Boundary | Payments, File Fees |

## EPIC Goal

Deliver this capability area as a coherent business workflow, not as isolated screens or endpoints. The EPIC is complete only when every linked user story is accepted, tested, and reflected in the progress tracker.

## Functional Scope

- System calculates dues by stage.
- File Opening, Admission, and Visa stages require financial clearance.
- Relevant departments can see clearance without editing payments.

## Business Rules To Preserve

- Only Accounts or Owner can record/confirm payments.
- Unconfirmed payments do not reduce dues.
- Payment gates block stage advancement.

## Dependencies

- Depends on FIL file fee snapshot.

## User Stories

- [ ] [PAY-EP2-US1: Calculate Stage Dues](../stories/PAY-EP2-US1_calculate_stage_dues.md)
- [ ] [PAY-EP2-US2: Enforce Financial Clearance Gates](../stories/PAY-EP2-US2_enforce_financial_clearance_gates.md)

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
