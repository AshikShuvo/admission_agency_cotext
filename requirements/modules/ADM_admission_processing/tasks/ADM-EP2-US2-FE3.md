# ADM-EP2-US2-FE3: Add tests for offer upload, approval blocking, and visa handoff state.
## Detailed Frontend Task Plan

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Traceability

| Level | Reference |
|---|---|
| Module | `ADM` - Admission Processing |
| EPIC | [ADM-EP2: University Application and Admission Approval](../epics/ADM-EP2_university_application_and_admission_approval.md) |
| User Story | [ADM-EP2-US2: Upload Offer Letter and Approve Admission](../stories/ADM-EP2-US2_upload_offer_letter_and_approve_admission.md) |
| Task Type | `FE` |

## Business Context

As an Admission user, I want to upload the offer letter and approve admission so that the file can move to visa processing.

This task supports the module goal: Manage admission document requests, document verification, university application submission, offer letter upload, and admission approval while enforcing document completeness and admission-stage payment clearance.

## Source Documents

- [Admission Processing Flow](../../../../business/flows/05_admission_processing_flow.md)
- [Module Boundaries](../../../../architecture/module_boundaries.md)
- [Admission Workbench Design](../../../../design-guide/10-admission-workbench.html)

## Acceptance Criteria Impact

- [ ] Offer letter is uploaded and linked to the file.
- [ ] Admission approval requires offer letter and admission payment clearance.
- [ ] Approved file moves to `Visa In Progress` or equivalent visa-ready status.

## Business Rules To Preserve

- Admission approval requires documents and payment clearance.
- Admission users cannot see commission data.
- All document status changes are logged.

## Dependencies To Check First

- Depends on FIL file status and PAY clearance.

## Implementation Plan

1. Locate or create the Admission Workspace route or workspace section that owns this behavior.
2. Create typed UI models for the data needed by the story; keep field names aligned with the backend DTO/API contract.
3. Build the screen, panel, form, table, queue, or state component described by the task with loading, empty, success, and error states.
4. Apply role-aware behavior using authenticated user role and backend permission response; do not rely on visual hiding for security decisions.
5. Connect mutation actions to API calls only after backend contract exists; otherwise document the missing contract as a blocker.
6. Add user-visible validation for required fields, invalid transitions, duplicate warnings, and blocked workflow states mentioned by acceptance criteria.
7. Add frontend coverage for the happy path and at least one blocked/error path. Prefer Playwright for full role flows and component tests only for risky reusable pieces.
8. Write tests that assert the visible business outcome, not only that components render.

## UI and Contract Expectations

- Frontend workspace: `Admission Workspace`.
- Use Next.js, TypeScript, Tailwind CSS, and React Query patterns when implementation begins.
- Prefer API-driven permissions and response fields over hardcoded role assumptions.
- Required states: loading, empty, successful data, validation error, authorization-restricted, and server error.
- Design reference: `../../../../design-guide/10-admission-workbench.html`.

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
Module: ADM
Story: ADM-EP2-US2
Completed task: ADM-EP2-US2-FE3
Files changed:
Tests run:
Tracker updated:
Open blockers:
Next recommended task:
```
