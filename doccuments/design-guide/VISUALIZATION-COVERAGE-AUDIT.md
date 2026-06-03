# Design Guide Visualization Coverage Audit

## Scope

This audit compares the business documentation under `doccuments/business/` against the current static prototype under `doccuments/design-guide/`.

The percentages measure UI visualization coverage, not backend readiness. A module scores higher when the prototype shows the main actor, primary flow, required fields, role boundaries, stage states, alternate paths, and business-rule blockers clearly enough for stakeholder review.

## Overall Result

Estimated Phase 1 visualization coverage after remediation: **94%**

The design guide now covers all major Phase 1 modules and the earlier depth gaps have been remediated with additional screens for notification tasks, exception decisions, open business questions, locked file states, payment ledgers, package versioning, named reports, admission timelines, visa reapplication, and commission audit. Remaining gaps are mostly implementation-level behavior or Phase 2/3 features that should remain clearly marked as future scope.

## Module Coverage

| Module | Business Source | Design Screens | Coverage | Assessment |
|---|---|---|---:|---|
| Design system and app shell | Phase 1 internal staff product | `00-design-system.html`, shared screen patterns | 88% | Covers tokens, stage gates, tables, forms, statuses, role badges, focus states, responsive shell. Remaining gaps are production behavior details for real drawers/modals. |
| Authentication and role entry | Users and Roles, Access Control | `01-login.html`, role dashboards, `16-staff-user-management.html` | 86% | Staff login, role routing, invite state, and user account setup are visible. Full password reset behavior remains implementation detail. |
| Staff and user management | Users and Roles, Access Control | `16-staff-user-management.html` | 94% | Covers Owner-only creation, role templates, data scope, activation/suspension, reassignment, permission preview, and access audit. |
| Catalog and package setup | Flow 01, Domain Section 5 | `05-catalog-package-management.html` | 96% | Adds package version history, draft/historical states, automatic active-package replacement, and existing-file snapshot protection. |
| Counselling and program selection | Flow 02 | `06-counselling-program-selection.html` | 93% | Adds side-by-side suitability comparison and unsuitable/no-active-package decision states. |
| File opening | Flow 03 | `07-file-opening.html`, `08-student-file-detail.html`, `19-business-decisions-open-questions.html` | 94% | Adds minimum-payment decision visibility and file-number format placeholder. |
| Payment and deposit confirmation | Flow 04, Financial Domain | `04-accounts-dashboard.html`, `09-payment-deposit-workbench.html`, `08-student-file-detail.html` | 95% | Adds multi-payment per-stage ledger, pending confirmation behavior, due formula, and owner override decision state. |
| Admission processing | Flow 05 | `10-admission-workbench.html`, `08-student-file-detail.html`, `17-notification-task-center.html` | 94% | Adds university submission timeline, expected response, offer-letter upload, and blocked offer/approval states. |
| Visa processing | Flow 06 | `11-visa-workbench.html`, `18-exception-closure-workbench.html`, `20-locked-file-state.html` | 95% | Adds pre-departure completion, rejection reason path, owner reapply/close decision, and same-file reapplication history. |
| Student file lifecycle workspace | Domain Section 8, all lifecycle flows | `08-student-file-detail.html`, `18-exception-closure-workbench.html`, `20-locked-file-state.html` | 94% | Adds locked completed/cancelled view, disabled edits, and owner correction authorization. |
| University commission tracking | Flow 07 | `12-commission-tracking.html`, owner dashboard, reports | 95% | Adds receipt/reference fields and commission adjustment audit. |
| Reporting and dashboards | Flow 08, Domain Section 13 | `02-owner-dashboard.html`, `03-consultant-dashboard.html`, `04-accounts-dashboard.html`, `13-reports-and-dashboards.html` | 94% | Adds all named business reports, filters, role visibility, monthly/yearly summaries, and university-wise enrollment. |
| Notifications and communication | Flow 09 | `14-notifications-access-exceptions.html`, `17-notification-task-center.html`, dashboards | 93% | Adds unread/read states, owner/assignee, linked file, due/SLA placeholder, completion state, and Phase 2 optional SMS/email labels. |
| Access control and role visibility | Flow 10, Users and Roles | `01-login.html`, role dashboards, `14-notifications-access-exceptions.html`, `16-staff-user-management.html`, `17-notification-task-center.html` | 93% | Role-specific screens, blocked examples, account scope, owner-only users/commission, and audit examples are visible. |
| Exception and file closure | Flow 11 | `18-exception-closure-workbench.html`, `20-locked-file-state.html`, `11-visa-workbench.html` | 95% | Adds hold reason, cancellation reason, owner reopening, reapply/close decision, completed/cancelled immutability, and preservation rules. |
| Future Phase 2/3 references | Phase Goals, Enhancements | `15-dark-mode-reference.html`, `17-notification-task-center.html`, `19-business-decisions-open-questions.html` | 68% | Future concepts are visible as scoped notes, not full Phase 2/3 screens, which matches the Phase 1 prototype boundary. |

## Business Rule Coverage

| Business Rule | Visualization Coverage | Notes |
|---|---:|---|
| BR-001 Payment gates | 92% | Stage gates and disabled approval actions are visible. |
| BR-002 Partial payment | 94% | Per-stage payment ledger now shows multiple payments and pending confirmation. |
| BR-003 Accounts-only confirmation | 90% | Accounts workbench owns confirmation; other roles show clearance only. |
| BR-004 Consultant file isolation | 88% | Consultant dashboard and blocked access states show own-file scope. |
| BR-005 Step approval authority | 86% | Approval roles are visible, but every approval action could show role ownership more explicitly. |
| BR-006 Commission confidentiality | 94% | Owner-only commission badges and screens are clear. |
| BR-007 Unique file number | 88% | File number appears and format placeholder is visible for sign-off. |
| BR-008 Document audit trail | 90% | Document vault, activity log, task center, and locked file history are visible. |
| BR-009 Completed/cancelled immutability | 95% | Dedicated locked file state now shows disabled edits and owner correction authorization. |
| BR-010 Visa rejection handling | 95% | Reapplication versus closure decision and record preservation are visualized. |
| BR-011 Automatic due calculation | 88% | Due calculation appears in payments/file detail; formula is not deeply visualized. |
| BR-012 One active package per program | 90% | Catalog screen shows active package warning/rule. |
| BR-013 Package snapshot on file creation | 90% | File opening and file detail show snapshot copy. |
| BR-014 Owner-only catalog management | 92% | Owner setup UI and consultant read-only context are clear. |
| BR-015 Active package required before file creation | 92% | File opening validates selected active package and shows blocked no-package state. |

## Remediated Deficiencies

1. **Exception detail flows**
   Added `18-exception-closure-workbench.html` and `20-locked-file-state.html`.

2. **Communication depth**
   Added `17-notification-task-center.html` with unread/read, assignee, due/SLA, linked file, completion, and optional Phase 2 channels.

3. **Reporting completeness**
   Expanded `13-reports-and-dashboards.html` with all named business reports.

4. **Payment history detail**
   Expanded `09-payment-deposit-workbench.html` with per-file stage payment ledger and override decision state.

5. **Open-question visualization**
   Added `19-business-decisions-open-questions.html`.

6. **Package versioning**
   Expanded `05-catalog-package-management.html` with version history and snapshot protection.

7. **Completed/cancelled lock state**
   Added `20-locked-file-state.html`.

## Architectural Readiness Assessment

The design guide is ready for Phase 1 module planning because every core bounded area has at least one visualization:

- Identity and access
- Staff/user management
- Catalog and package management
- Counselling
- File lifecycle
- Payments and dues
- Admission documents
- Visa documents and outcomes
- Commission tracking
- Reporting
- Notifications
- Exceptions

The prototype is now strong enough for Phase 1 implementation planning. Remaining work before build should focus on translating these screens into frontend routes, backend modules, permissions, validation, and automated tests.
