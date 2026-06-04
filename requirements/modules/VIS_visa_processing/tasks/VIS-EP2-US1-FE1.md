# VIS-EP2-US1-FE1: Build visa outcome form with approved and rejected branches.
## Detailed Frontend Task Plan

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `VIS` - Visa Processing |
| EPIC | [VIS-EP2: Visa Outcome and File Completion](../epics/VIS-EP2_visa_outcome_and_file_completion.md) |
| User Story | [VIS-EP2-US1: Record Visa Outcome](../stories/VIS-EP2-US1_record_visa_outcome.md) |
| Task Type | `FE` |

## Business Context

As a Visa user, I want to record the visa outcome so that the file reflects the real application result.

This task supports the module goal: Manage visa document collection, visa application submission, payment clearance, outcome recording, rejection handling, and completion of the student file.

## Source Documents

- [Visa Processing Flow](../../../../business/flows/06_visa_processing_flow.md)
- [Module Boundaries](../../../../architecture/module_boundaries.md)
- [Visa Workbench Design](../../../../design-guide/11-visa-workbench.html)

## Acceptance Criteria Impact

- [ ] Outcome can be approved or rejected.
- [ ] Approved outcome records issue date and expiry date when available.
- [ ] Rejected outcome records rejection reason and does not delete previous records.

## Business Rules To Preserve

- Visa approval/completion requires documents and payment clearance.
- Visa rejection preserves history.
- Visa users cannot see commission data.

## Dependencies To Check First

- Depends on ADM approval, offer letter, and PAY clearance.

## Implementation Plan

1. Locate or create the Visa Workspace route or workspace section that owns this behavior.
2. Create typed UI models for the data needed by the story; keep field names aligned with the backend DTO/API contract.
3. Build the screen, panel, form, table, queue, or state component described by the task with loading, empty, success, and error states.
4. Apply role-aware behavior using authenticated user role and backend permission response; do not rely on visual hiding for security decisions.
5. Connect mutation actions to API calls only after backend contract exists; otherwise document the missing contract as a blocker.
6. Add user-visible validation for required fields, invalid transitions, duplicate warnings, and blocked workflow states mentioned by acceptance criteria.
7. Add frontend coverage for the happy path and at least one blocked/error path. Prefer Playwright for full role flows and component tests only for risky reusable pieces.
8. Define field-level validation messages, submit-disabled rules, dirty-state behavior, and reset behavior after successful save.

## UI and Contract Expectations

- Frontend workspace: `Visa Workspace`.
- Use Next.js, TypeScript, Tailwind CSS, and React Query patterns when implementation begins.
- Prefer API-driven permissions and response fields over hardcoded role assumptions.
- Required states: loading, empty, successful data, validation error, authorization-restricted, and server error.
- Design reference: `../../../../design-guide/11-visa-workbench.html`.

## Data, State, and Error Handling

- Identify all required fields from the story acceptance criteria before implementation.
- Keep IDs stable and use backend-generated identifiers for persisted records.
- Handle not found, forbidden, validation error, duplicate/conflict, and workflow-blocked responses.
- Preserve historical records when the business flow says data must not be deleted or overwritten.
- Do not expose restricted fields in UI state, API responses, logs, or test fixtures.

## Test Plan

- [ ] Add or update automated tests for the normal successful path.
- [ ] Add or update tests for at least one blocked or invalid path.
- [ ] Add role/access tests when task touches restricted data or actions.
- [ ] Confirm test data includes the minimum business objects needed for this story.
- [ ] Record the test command in the agent handoff note.

## Definition of Done

- [ ] Implementation matches this task plan and the linked story acceptance criteria.
- [ ] Required UI/API/service behavior is implemented in the correct module boundary.
- [ ] Authorization and data visibility are enforced where applicable.
- [ ] Tests are added or an explicit test gap is recorded as a blocker.
- [ ] This task checkbox is marked complete in the story file and source module summary.
- [ ] [Progress Tracker](../../../progress_tracker.md) is updated with the completed task count.

## Handoff Note Template

```text
Module: VIS
Story: VIS-EP2-US1
Completed task: VIS-EP2-US1-FE1
Files changed:
Tests run:
Tracker updated:
Open blockers:
Next recommended task:
```
