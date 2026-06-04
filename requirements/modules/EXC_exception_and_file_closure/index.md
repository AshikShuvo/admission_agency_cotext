# Exception and File Closure
## Independent Requirement Module Folder

Module ID: `EXC`

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Module Goal

Handle files that pause, cancel, complete, or receive visa rejection without deleting business history, payments, documents, or audit records.

## Primary Actors

- Owner
- Consultant
- Admission
- Visa
- Accounts, financial visibility only

## Source Documents

- [Exception and File Closure Flow](../../../business/flows/11_exception_and_file_closure_flow.md)
- [Module Boundaries](../../../architecture/module_boundaries.md)
- [Exception Closure Workbench Design](../../../design-guide/18-exception-closure-workbench.html)
- [Locked File State Design](../../../design-guide/20-locked-file-state.html)

## Architecture Routing

| Area | Owner |
|---|---|
| Frontend workspace | File Detail Workspaces |
| Backend module boundary | Files / Cases |
| Design reference | ../../../design-guide/18-exception-closure-workbench.html and ../../../design-guide/20-locked-file-state.html |

## Business Rules

- Files are not deleted.
- Cancelled and completed files are locked from normal edits.
- Visa reapplication preserves previous history.

## Dependencies

- Depends on FIL status model, VIS rejection, and COM completion eligibility.

## EPIC Files

- [ ] [EXC-EP1: Hold and Cancellation](epics/EXC-EP1_hold_and_cancellation.md)
- [ ] [EXC-EP2: Rejection and Final Closure](epics/EXC-EP2_rejection_and_final_closure.md)

## User Story Files

- [ ] [EXC-EP1-US1: Put File On Hold and Resume](stories/EXC-EP1-US1_put_file_on_hold_and_resume.md)
- [ ] [EXC-EP1-US2: Cancel File Without Deletion](stories/EXC-EP1-US2_cancel_file_without_deletion.md)
- [ ] [EXC-EP2-US1: Review Visa Rejection and Reapplication](stories/EXC-EP2-US1_review_visa_rejection_and_reapplication.md)
- [ ] [EXC-EP2-US2: Lock Completed Files](stories/EXC-EP2-US2_lock_completed_files.md)

## Task Implementation Plans

- [ ] [EXC-EP1-US1-FE1](tasks/EXC-EP1-US1-FE1.md): Build on-hold action and reason form in file detail.
- [ ] [EXC-EP1-US1-FE2](tasks/EXC-EP1-US1-FE2.md): Show on-hold banner, reason, and resume action where authorized.
- [ ] [EXC-EP1-US1-FE3](tasks/EXC-EP1-US1-FE3.md): Add tests for hold, hold banner, and resume states.
- [ ] [EXC-EP1-US1-BE1](tasks/EXC-EP1-US1-BE1.md): Implement hold status transition with reason and previous-stage metadata.
- [ ] [EXC-EP1-US1-BE2](tasks/EXC-EP1-US1-BE2.md): Implement resume transition with authorization and audit log.
- [ ] [EXC-EP1-US1-BE3](tasks/EXC-EP1-US1-BE3.md): Add tests for hold/resume history preservation.
- [ ] [EXC-EP1-US2-FE1](tasks/EXC-EP1-US2-FE1.md): Build cancel action with confirmation and required reason.
- [ ] [EXC-EP1-US2-FE2](tasks/EXC-EP1-US2-FE2.md): Show cancelled locked-file state with preserved history.
- [ ] [EXC-EP1-US2-FE3](tasks/EXC-EP1-US2-FE3.md): Add tests for cancel flow and blocked normal edits.
- [ ] [EXC-EP1-US2-BE1](tasks/EXC-EP1-US2-BE1.md): Implement cancellation transition with reason and audit log.
- [ ] [EXC-EP1-US2-BE2](tasks/EXC-EP1-US2-BE2.md): Enforce cancelled-file edit restrictions and no-delete business rule.
- [ ] [EXC-EP1-US2-BE3](tasks/EXC-EP1-US2-BE3.md): Add tests for cancellation, edit blocking, and record preservation.
- [ ] [EXC-EP2-US1-FE1](tasks/EXC-EP2-US1-FE1.md): Build Owner rejection review panel with reapply or close decision.
- [ ] [EXC-EP2-US1-FE2](tasks/EXC-EP2-US1-FE2.md): Show previous visa attempt history in the file detail.
- [ ] [EXC-EP2-US1-FE3](tasks/EXC-EP2-US1-FE3.md): Add tests for reapplication decision and history display.
- [ ] [EXC-EP2-US1-BE1](tasks/EXC-EP2-US1-BE1.md): Implement visa reapplication decision API with Owner-only authorization.
- [ ] [EXC-EP2-US1-BE2](tasks/EXC-EP2-US1-BE2.md): Create new visa attempt records while preserving previous rejection history.
- [ ] [EXC-EP2-US1-BE3](tasks/EXC-EP2-US1-BE3.md): Add tests for reapplication, history preservation, and owner-only decision.
- [ ] [EXC-EP2-US2-FE1](tasks/EXC-EP2-US2-FE1.md): Show completed locked-file state with limited available actions.
- [ ] [EXC-EP2-US2-FE2](tasks/EXC-EP2-US2-FE2.md): Build Owner exceptional correction request path.
- [ ] [EXC-EP2-US2-FE3](tasks/EXC-EP2-US2-FE3.md): Add tests for completed lock and owner correction UI.
- [ ] [EXC-EP2-US2-BE1](tasks/EXC-EP2-US2-BE1.md): Enforce completed-file mutation restrictions across core services.
- [ ] [EXC-EP2-US2-BE2](tasks/EXC-EP2-US2-BE2.md): Implement Owner exceptional correction authorization with reason and audit log.
- [ ] [EXC-EP2-US2-BE3](tasks/EXC-EP2-US2-BE3.md): Add tests for completed lock, owner exception, and commission eligibility flag.

## Folder Completion Rules

- [ ] Every EPIC file is complete.
- [ ] Every story file is accepted.
- [ ] Every task implementation plan is completed or explicitly deferred with an approved blocker.
- [ ] Module row is updated in [Progress Tracker](../../progress_tracker.md).
- [ ] Completion log records meaningful milestone completion.
