# Testing Strategy
## Student Abroad Admission Agency Management System

This document describes how the software should be tested across frontend, backend, APIs, access control, and business workflows.

Source documents:

- [Architecture Overview](architecture_overview.md)
- [Module Boundaries](module_boundaries.md)
- [API Design](api_design.md)
- [Access Control](access_control.md)
- [Phase Goals](../business/phase_goals.md)

## Testing Decision

Phase 1 must include both:

- **Frontend end-to-end testing with Playwright**
- **Backend unit and integration testing for NestJS modules**

The highest-risk areas are payment gates, role access, file lifecycle status changes, document handling, and commission confidentiality. Tests should focus there first.

## Test Layers

| Layer | Tool | Purpose |
|---|---|---|
| Backend unit tests | Jest or NestJS testing utilities | Validate business rules inside services and domain logic. |
| Backend integration tests | Jest + test database | Validate API behavior, database writes, permissions, and workflow transitions. |
| Frontend component tests | Optional, only where useful | Validate complex reusable UI components if they become risky. |
| Frontend E2E tests | Playwright | Validate complete role-based user flows through the browser. |
| Manual acceptance testing | Business checklist | Confirm workflows match agency expectations before release. |

## Backend Unit Test Scope

Backend unit tests should cover business rules without needing a browser.

Required areas:

- File creation requires selected program with active package.
- Package fee line items are snapshot-copied onto file fees.
- Custom fee changes require Owner approval.
- Due amount calculation uses only confirmed payments.
- Phase 1 does not allow payment-gate override.
- Stage approval is blocked when dues remain.
- Stage approval is blocked when required documents are incomplete.
- Completed and cancelled files reject normal edits.
- Visa rejection stays on the same file and preserves history.
- Commission access is Owner-only.

## Backend Integration Test Scope

Integration tests should use a separate test database and validate API-level behavior.

Required scenarios:

- Owner can create country, university, program, package, and active package line items.
- Consultant can browse active catalog but cannot mutate it.
- Consultant can create a file only when an active package exists.
- Accounts can record and confirm payments.
- Admission cannot approve a file before admission payment clearance.
- Visa cannot complete a file before visa payment clearance.
- Consultant cannot list or open another consultant's file.
- Accounts cannot fetch document content.
- Non-owner cannot access commission endpoints.
- Reports return role-scoped results.

## Frontend Playwright Scope

Playwright should test the most important user journeys through the browser.

Required Phase 1 Playwright flows:

| Flow | Scenario |
|---|---|
| Owner catalog setup | Owner logs in, creates catalog records, activates package, verifies package summary. |
| Consultant file opening | Consultant logs in, browses catalog, creates student file, sees assigned file only. |
| Accounts payment confirmation | Accounts logs in, records payment, confirms deposit, verifies due changes. |
| Admission processing | Admission logs in, sees eligible file, requests/verifies documents, records offer letter, approves admission after payment clearance. |
| Visa processing | Visa logs in, sees eligible file, verifies visa documents, records visa outcome, completes or rejects file. |
| Owner commission tracking | Owner logs in, records commission, verifies non-owner roles cannot see it. |
| Role isolation | Each role logs in and cannot access restricted screens or direct URLs. |

## Frontend UI Expectations To Test

Playwright tests should verify:

- Navigation changes based on role.
- Consultants see only assigned files.
- Accounts workspace does not expose document content.
- Admission workspace does not expose commission data.
- Visa workspace does not expose full financial data.
- Owner sees full reports and commission features.
- Forms show clear errors for blocked workflow transitions.
- File status visibly changes after valid stage actions.

## Test Data Strategy

Use deterministic seed data for automated tests:

- One Owner
- Two Consultants
- One Accounts user
- One Admission user
- One Visa user
- One active country
- One university
- One program
- One active package with File Opening, Admission, and Visa fee lines
- At least two student files assigned to different consultants

Test data must make consultant isolation easy to verify.

## CI Expectations

When CI/CD is added, the minimum checks should be:

```text
Backend:
  - type check
  - unit tests
  - integration tests

Frontend:
  - type check
  - Playwright smoke/e2e tests

Shared:
  - lint if configured
```

For local-first Phase 1, these checks can initially run manually. Before production deployment, they should run automatically in CI.

## Acceptance Criteria

Phase 1 is not ready for real business use until:

- Backend tests prove payment gates and role access rules.
- Playwright tests prove the full file lifecycle from catalog setup to file completion.
- Playwright tests prove direct URL access does not bypass role restrictions.
- Document upload/download access is tested by role.
- Commission data is tested as Owner-only.
- Backup restore testing is completed separately as described in [File Storage and Documents](file_storage_and_documents.md).
