# Admissions OS Design Handoff

## Summary

This folder contains a static HTML/CSS prototype for the Phase 1 internal admissions-agency system. The screens follow the documented business lifecycle: staff setup, catalog setup, counselling, file opening, payment confirmation, admission processing, visa processing, file completion, commission tracking, reporting, notifications, access control, and exceptions.

Start review from `index.html`. It acts as the clickable prototype menu, and every HTML screen includes Previous, Flow Index, and Next controls near the bottom of the page.

Read `VISUALIZATION-COVERAGE-AUDIT.md` for the business-flow coverage percentages and remaining visualization gaps.

Design direction:

- Palette: neutral-dominant Green + Navy with a restrained gold accent for owner-only commission.
- Typography: Source Serif 4 for headings and Manrope for dense operational body text.
- Layout: compact B2B dashboard shell for repeated staff workflows.
- Dark mode: `15-dark-mode-reference.html` provides reference tokens and components only; the main Phase 1 prototype remains light by default.

## Screen Inventory

| File | Purpose |
|---|---|
| `index.html` | Clickable prototype menu and recommended review path. |
| `00-design-system.html` | Tokens, components, status badges, stage gates, table, empty/loading examples. |
| `01-login.html` | Staff login and role-based product framing. |
| `02-owner-dashboard.html` | Owner-wide files, revenue, dues, commission, activity, and decisions. |
| `03-consultant-dashboard.html` | Consultant own-file scope, document requests, and follow-up work. |
| `04-accounts-dashboard.html` | Accounts payment metrics, pending confirmations, and dues. |
| `05-catalog-package-management.html` | Owner setup flow for country, university, program, and stage-wise active package pricing. |
| `06-counselling-program-selection.html` | Consultant program search, package review, and file-opening readiness. |
| `07-file-opening.html` | Student registration, package snapshot, quotation, and initial payment gate. |
| `08-student-file-detail.html` | Central file workspace with lifecycle gates, role tabs, and activity history. |
| `09-payment-deposit-workbench.html` | Payment recording, verification, due calculation, and stage clearance. |
| `10-admission-workbench.html` | Admission document checklist, payment gate, university submission, and approval. |
| `11-visa-workbench.html` | Visa document queue, submission, outcome recording, completion or rejection. |
| `12-commission-tracking.html` | Owner-only commission entry and reports after completion. |
| `13-reports-and-dashboards.html` | Role-scoped filters, operational metrics, financial reports, and performance views. |
| `14-notifications-access-exceptions.html` | Notifications, unauthorized states, on-hold, cancelled, rejected, and completed states. |
| `15-dark-mode-reference.html` | Dark-mode reference for tokens, shell, tables, forms, statuses, and stage gates. |
| `16-staff-user-management.html` | Owner-only staff user creation, role assignment, activation/suspension, consultant file transfer, and access audit. |
| `17-notification-task-center.html` | In-app notification lifecycle, unread/read states, assigned follow-up tasks, SLA placeholders, and optional Phase 2 SMS/email states. |
| `18-exception-closure-workbench.html` | On-hold, cancellation, visa rejection, reapplication, closure, and owner authorization decisions. |
| `19-business-decisions-open-questions.html` | Open business questions OQ-01 to OQ-15 with recommended Phase 1 defaults and impact areas. |
| `20-locked-file-state.html` | Completed/cancelled immutable file state, disabled edits, owner correction request, and preserved activity history. |

## Component Guidance

- Use the app shell for all authenticated staff workflows: sidebar, topbar, page header, primary action, and dense content area.
- Use stage gate rows for lifecycle progression. Each gate must show label, business requirement, and status text.
- Use badges for compact statuses, but never rely on color alone.
- Use tables for queues, reports, payment records, and file lists.
- Use right-side panels for selected record details, confirmation forms, checklist actions, and outcome entry.
- Use anchor-target modal references in the static prototype for setup flows that would become drawers or modals in production, such as adding countries, universities, programs, and package line items.
- Use document tables for any stage that collects scans or PDFs. Each row should show required document name, upload control, owning stage, verification status, and correction/review note.
- Use staff management forms for Owner-only account creation. Each new user must receive one role, a default data scope, invitation/password reset state, and a permission preview.
- Use disabled buttons for blocked business actions such as admission approval while dues or documents are incomplete.
- Use exception decision forms for on-hold, cancellation, visa rejection, reapplication, and owner reopening authorization.
- Use notification task tables for event follow-up. Each task should show linked file, owner, read state, due/SLA placeholder, and completion state.

## Role And Visibility Rules

- Owner: full access to files, catalog, users, reports, financials, commissions, and overrides.
- Consultant: own assigned files, catalog browsing, package summaries, and student follow-up tasks.
- Accounts: payment records, dues, confirmation history, and limited file/student identifiers.
- Admission: admission documents, academic details, application submission, offer letter, and admission approval.
- Visa: visa documents, passport/offer-letter context, visa submission, outcome, completion, and rejection.
- Commission data is represented with gold owner-only badges and must not appear in non-owner screens.
- Consultants upload or attach student-provided scans/PDFs, while Admission and Visa verify, request corrections, and preserve the document history in the file vault.
- Owner creates and suspends Consultant, Accounts, Admission, and Visa staff accounts. Non-owner roles must not see or use user-management actions.

## Responsive And Accessibility Notes

- Each screen is standalone and can be opened directly in a browser.
- Layouts collapse to a single column on small screens.
- Controls include visible focus states.
- Form fields use labels, tables use headers, and buttons keep visible text.
- Production implementation should add keyboard behavior for drawers, modals, dropdowns, and mobile navigation.

## Acceptance Checklist

- Catalog setup exists before counselling.
- Owner-only staff setup exists before staff can log in and work inside role-scoped dashboards.
- Counselling selection can lead to file opening only when the program has an active package.
- File opening creates the payment gate before admission.
- Admission approval is blocked by missing documents or unpaid admission dues.
- Visa outcome supports approved, rejected, and completion paths.
- Admission and visa screens show scan/PDF upload rows for required documents and correction-request states.
- Completed files become eligible for owner-only commission tracking.
- Reports and dashboards respect role scope.
- Notifications, access restrictions, on-hold, cancelled, visa-rejected, and completed states are visible in the prototype.
- Payment ledger shows multiple payment entries per stage and due calculation behavior.
- Package history shows active, historical, and draft packages with existing-file snapshot protection.
- All named reports from the business documentation are visible in the report catalog.
- Open business questions are visualized before development sign-off.
- Completed/cancelled files have a locked-state screen with owner-only correction authorization.
