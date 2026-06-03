# Business Flows Index
## Student Abroad Admission Agency Management System

This folder breaks the full business domain into separate workflow documents so each solution flow can be reviewed independently.

Source document: `doccuments/business/business_domain_documentation.md`

## Flow Files

| # | Flow | File | Primary Owner |
|---|---|---|---|
| 1 | Catalog and Package Setup | `01_catalog_and_package_setup_flow.md` | Owner |
| 2 | Counselling and Program Selection | `02_counselling_and_program_selection_flow.md` | Consultant |
| 3 | File Opening | `03_file_opening_flow.md` | Consultant, Accounts |
| 4 | Payment and Deposit Confirmation | `04_payment_and_deposit_confirmation_flow.md` | Accounts |
| 5 | Admission Processing | `05_admission_processing_flow.md` | Admission Department |
| 6 | Visa Processing | `06_visa_processing_flow.md` | Visa Department |
| 7 | University Commission Tracking | `07_university_commission_tracking_flow.md` | Owner |
| 8 | Reporting and Dashboard | `08_reporting_and_dashboard_flow.md` | Owner, Accounts, Consultant |
| 9 | Notifications and Communication | `09_notifications_and_communication_flow.md` | System |
| 10 | Access Control and Role Visibility | `10_access_control_and_role_visibility_flow.md` | System, Owner |
| 11 | Exception and File Closure Handling | `11_exception_and_file_closure_flow.md` | Owner, Relevant Department |

## End-to-End Lifecycle

```text
Catalog Setup
  -> Counselling and Program Selection
  -> File Opening
  -> File Opening Payment Confirmation
  -> Admission Processing
  -> Admission Payment Confirmation
  -> Offer Letter and Admission Approval
  -> Visa Processing
  -> Visa Payment Confirmation
  -> Visa Outcome
  -> Student Departed / Completed
  -> Commission Tracking
  -> Reporting
```

## Cross-Cutting Flows

These flows apply across several lifecycle stages:

- Payment and deposit confirmation
- Access control and role visibility
- Notifications and communication
- Reporting and dashboards
- Exception handling, cancellation, hold, and visa rejection
