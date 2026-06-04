# Catalog and Packages
## Independent Requirement Module Folder

Module ID: `CAT`

Status: `Not Started`
Owner: `Unassigned`
Last updated: `2026-06-04`

## Module Goal

Allow the Owner to maintain countries, universities, programs, and active stage-wise packages so consultants can counsel students using accurate program and fee data.

## Primary Actors

- Owner / Admin
- Consultant, read-only
- Accounts, limited package view when linked to a file

## Source Documents

- [Catalog and Package Setup Flow](../../../business/flows/01_catalog_and_package_setup_flow.md)
- [Module Boundaries](../../../architecture/module_boundaries.md)
- [Catalog Package Management Design](../../../design-guide/05-catalog-package-management.html)

## Architecture Routing

| Area | Owner |
|---|---|
| Frontend workspace | Catalog Management |
| Backend module boundary | Catalog |
| Design reference | ../../../design-guide/05-catalog-package-management.html |

## Business Rules

- Only Owner can mutate catalog records.
- Consultants browse active records only.
- Only one active package is allowed per program.
- File creation must snapshot active package fees.

## Dependencies

- None for core catalog setup. It is an upstream dependency for counselling and file opening.

## EPIC Files

- [ ] [CAT-EP1: Master Catalog Management](epics/CAT-EP1_master_catalog_management.md)
- [ ] [CAT-EP2: Package and Fee Configuration](epics/CAT-EP2_package_and_fee_configuration.md)

## User Story Files

- [ ] [CAT-EP1-US1: Manage Countries and Universities](stories/CAT-EP1-US1_manage_countries_and_universities.md)
- [ ] [CAT-EP1-US2: Manage Programs](stories/CAT-EP1-US2_manage_programs.md)
- [ ] [CAT-EP2-US1: Configure Stage-wise Packages](stories/CAT-EP2-US1_configure_stage_wise_packages.md)
- [ ] [CAT-EP2-US2: Activate One Package per Program](stories/CAT-EP2-US2_activate_one_package_per_program.md)

## Task Implementation Plans

- [ ] [CAT-EP1-US1-FE1](tasks/CAT-EP1-US1-FE1.md): Build country and university list/detail screens with create, edit, activate, and deactivate actions.
- [ ] [CAT-EP1-US1-FE2](tasks/CAT-EP1-US1-FE2.md): Add form validation for required names, duplicate display warnings, and active/inactive state controls.
- [ ] [CAT-EP1-US1-FE3](tasks/CAT-EP1-US1-FE3.md): Add role-based UI states so consultants see read-only catalog data.
- [ ] [CAT-EP1-US1-BE1](tasks/CAT-EP1-US1-BE1.md): Create country and university entities with status fields, ownership timestamps, and unique constraints.
- [ ] [CAT-EP1-US1-BE2](tasks/CAT-EP1-US1-BE2.md): Implement owner-only CRUD APIs and read-only listing APIs for allowed staff roles.
- [ ] [CAT-EP1-US1-BE3](tasks/CAT-EP1-US1-BE3.md): Add tests for owner CRUD, non-owner blocking, inactive filtering, and duplicate handling.
- [ ] [CAT-EP1-US2-FE1](tasks/CAT-EP1-US2-FE1.md): Build program table and program form scoped to the selected university.
- [ ] [CAT-EP1-US2-FE2](tasks/CAT-EP1-US2-FE2.md): Add filters for country, university, program level, field, and active status.
- [ ] [CAT-EP1-US2-FE3](tasks/CAT-EP1-US2-FE3.md): Add frontend coverage for creating, editing, filtering, and read-only browsing.
- [ ] [CAT-EP1-US2-BE1](tasks/CAT-EP1-US2-BE1.md): Create program entity linked to university with searchable fields and active status.
- [ ] [CAT-EP1-US2-BE2](tasks/CAT-EP1-US2-BE2.md): Implement program CRUD, browse, and filter APIs with owner-only mutation guards.
- [ ] [CAT-EP1-US2-BE3](tasks/CAT-EP1-US2-BE3.md): Add tests for university ownership, active filtering, and program selection eligibility.
- [ ] [CAT-EP2-US1-FE1](tasks/CAT-EP2-US1-FE1.md): Build package editor with grouped fee line item sections for each processing stage.
- [ ] [CAT-EP2-US1-FE2](tasks/CAT-EP2-US1-FE2.md): Show automatic stage totals, total package cost, and validation for missing or negative amounts.
- [ ] [CAT-EP2-US1-FE3](tasks/CAT-EP2-US1-FE3.md): Add frontend tests for adding, editing, removing, and validating fee line items.
- [ ] [CAT-EP2-US1-BE1](tasks/CAT-EP2-US1-BE1.md): Create package and package fee line item entities with stage enum and amount validation.
- [ ] [CAT-EP2-US1-BE2](tasks/CAT-EP2-US1-BE2.md): Implement package draft save and calculated summary APIs.
- [ ] [CAT-EP2-US1-BE3](tasks/CAT-EP2-US1-BE3.md): Add tests for stage totals, invalid fee amounts, and package line item persistence.
- [ ] [CAT-EP2-US2-FE1](tasks/CAT-EP2-US2-FE1.md): Add activation action with confirmation text explaining snapshot behavior.
- [ ] [CAT-EP2-US2-FE2](tasks/CAT-EP2-US2-FE2.md): Show current active package status in program and package screens.
- [ ] [CAT-EP2-US2-FE3](tasks/CAT-EP2-US2-FE3.md): Add UI tests for package activation and active-package visibility.
- [ ] [CAT-EP2-US2-BE1](tasks/CAT-EP2-US2-BE1.md): Enforce one active package per program with transaction-safe activation logic.
- [ ] [CAT-EP2-US2-BE2](tasks/CAT-EP2-US2-BE2.md): Add active package lookup API used by counselling and file opening.
- [ ] [CAT-EP2-US2-BE3](tasks/CAT-EP2-US2-BE3.md): Add tests proving activation does not mutate existing file fee snapshots.

## Folder Completion Rules

- [ ] Every EPIC file is complete.
- [ ] Every story file is accepted.
- [ ] Every task implementation plan is completed or explicitly deferred with an approved blocker.
- [ ] Module row is updated in [Progress Tracker](../../progress_tracker.md).
- [ ] Completion log records meaningful milestone completion.
