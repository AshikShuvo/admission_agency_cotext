# University Commission Tracking
## Independent Requirement Module Folder

Module ID: `COM`

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Module Goal

Allow the Owner to record confidential university commission revenue for completed or enrolled student files and include it only in Owner-visible reports.

## Primary Actors

- Owner
- University

## Source Documents

- [University Commission Tracking Flow](../../../business/flows/07_university_commission_tracking_flow.md)
- [Module Boundaries](../../../architecture/module_boundaries.md)
- [Commission Tracking Design](../../../design-guide/12-commission-tracking.html)

## Architecture Routing

| Area | Owner |
|---|---|
| Frontend workspace | Owner Reports and Settings |
| Backend module boundary | Commissions |
| Design reference | ../../../design-guide/12-commission-tracking.html |

## Business Rules

- Commission is Owner-only.
- Commission records link to file and university.
- Non-owner responses must exclude commission data.

## Dependencies

- Depends on VIS completion/enrollment and ACL Owner-only access.

## EPIC Files

- [ ] [COM-EP1: Owner-only Commission Records](epics/COM-EP1_owner_only_commission_records.md)
- [ ] [COM-EP2: Commission Reporting](epics/COM-EP2_commission_reporting.md)

## User Story Files

- [ ] [COM-EP1-US1: Record Commission Payment](stories/COM-EP1-US1_record_commission_payment.md)
- [ ] [COM-EP1-US2: Protect Commission Confidentiality](stories/COM-EP1-US2_protect_commission_confidentiality.md)
- [ ] [COM-EP2-US1: View Commission List and Filters](stories/COM-EP2-US1_view_commission_list_and_filters.md)
- [ ] [COM-EP2-US2: Include Commission in Owner Revenue Summary](stories/COM-EP2-US2_include_commission_in_owner_revenue_summary.md)

## Task Implementation Plans

- [ ] [COM-EP1-US1-FE1](tasks/COM-EP1-US1-FE1.md): Build owner-only commission entry form with file and university lookup.
- [ ] [COM-EP1-US1-FE2](tasks/COM-EP1-US1-FE2.md): Add eligibility warning for non-completed files and required exception note.
- [ ] [COM-EP1-US1-FE3](tasks/COM-EP1-US1-FE3.md): Add tests that non-owner workspaces never render commission entry.
- [ ] [COM-EP1-US1-BE1](tasks/COM-EP1-US1-BE1.md): Create commission entity linked to file, university, and owner actor.
- [ ] [COM-EP1-US1-BE2](tasks/COM-EP1-US1-BE2.md): Implement owner-only create/update APIs with eligibility validation.
- [ ] [COM-EP1-US1-BE3](tasks/COM-EP1-US1-BE3.md): Add tests for owner-only access, eligibility rules, and persistence.
- [ ] [COM-EP1-US2-FE1](tasks/COM-EP1-US2-FE1.md): Ensure non-owner file detail and reports have no commission sections or fields.
- [ ] [COM-EP1-US2-FE2](tasks/COM-EP1-US2-FE2.md): Add restricted-state handling if a non-owner attempts direct navigation.
- [ ] [COM-EP1-US2-FE3](tasks/COM-EP1-US2-FE3.md): Add tests for commission visibility by role.
- [ ] [COM-EP1-US2-BE1](tasks/COM-EP1-US2-BE1.md): Add owner-only guards and query filters for commission APIs.
- [ ] [COM-EP1-US2-BE2](tasks/COM-EP1-US2-BE2.md): Remove commission fields from all non-owner aggregate report responses.
- [ ] [COM-EP1-US2-BE3](tasks/COM-EP1-US2-BE3.md): Add tests for direct API access blocking and response sanitization.
- [ ] [COM-EP2-US1-FE1](tasks/COM-EP2-US1-FE1.md): Build owner commission list with filters and summary count.
- [ ] [COM-EP2-US1-FE2](tasks/COM-EP2-US1-FE2.md): Add loading, empty, and filtered result states.
- [ ] [COM-EP2-US1-FE3](tasks/COM-EP2-US1-FE3.md): Add tests for filtering and owner-only route access.
- [ ] [COM-EP2-US1-BE1](tasks/COM-EP2-US1-BE1.md): Implement commission list API with filter DTOs and pagination.
- [ ] [COM-EP2-US1-BE2](tasks/COM-EP2-US1-BE2.md): Add owner-only authorization and efficient joins to file/university data.
- [ ] [COM-EP2-US1-BE3](tasks/COM-EP2-US1-BE3.md): Add tests for filters, pagination, and role blocking.
- [ ] [COM-EP2-US2-FE1](tasks/COM-EP2-US2-FE1.md): Add commission total cards and breakdowns to owner reports.
- [ ] [COM-EP2-US2-FE2](tasks/COM-EP2-US2-FE2.md): Add date and university filters for commission summaries.
- [ ] [COM-EP2-US2-FE3](tasks/COM-EP2-US2-FE3.md): Add tests proving accounts reports exclude commission totals.
- [ ] [COM-EP2-US2-BE1](tasks/COM-EP2-US2-BE1.md): Add owner revenue summary query with separate commission aggregation.
- [ ] [COM-EP2-US2-BE2](tasks/COM-EP2-US2-BE2.md): Ensure reporting module consumes commission totals only for Owner context.
- [ ] [COM-EP2-US2-BE3](tasks/COM-EP2-US2-BE3.md): Add tests for aggregation accuracy and accounts exclusion.

## Folder Completion Rules

- [ ] Every EPIC file is complete.
- [ ] Every story file is accepted.
- [ ] Every task implementation plan is completed or explicitly deferred with an approved blocker.
- [ ] Module row is updated in [Progress Tracker](../../progress_tracker.md).
- [ ] Completion log records meaningful milestone completion.
