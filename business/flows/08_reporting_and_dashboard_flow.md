# Reporting and Dashboard Flow

## Purpose

Give each role the operational and financial visibility required for their responsibilities while enforcing role-based data boundaries.

## Primary Actors

- Owner
- Accounts Department
- Consultant

## Trigger

A user opens a dashboard or generates a report.

## Preconditions

- User is authenticated.
- User role is known.
- File, payment, document, and activity records exist.

## Main Flow

1. User opens their dashboard or report screen.
2. System identifies the user's role.
3. System applies role-specific data filters.
4. User selects report filters where applicable:
   - Date range
   - File status
   - Consultant
   - Stage
   - University
5. System queries only authorized data.
6. System calculates totals, counts, dues, or summaries.
7. System displays dashboard metrics or report results.

## Owner Dashboard

Owner can view:

- Total open files
- Files by status
- Files by consultant
- Current month and current year revenue
- Outstanding dues
- Recent activity
- Commission revenue
- University-wise enrollment

## Consultant Dashboard

Consultant can view:

- Own open files
- Own files by status
- Pending document requests
- Upcoming tasks

## Accounts Dashboard

Accounts can view:

- Payments received today, this week, and this month
- Outstanding dues
- Pending deposit confirmations
- Revenue by payment stage

## Business Rules

- Owner has full reporting access.
- Accounts can view financial reports but not commission data unless explicitly owner-only reports are excluded.
- Consultants can view only their assigned files.
- Access filtering must happen at the data/query layer, not only in the UI.

## Outputs

- Dashboard metrics
- Operational reports
- Financial reports
- Outstanding dues report
- Owner-only commission reports

## Related Data

- File
- Payment
- Commission
- Document
- User
- File Activity Log

## Source Sections

- Section 7.4: Revenue Reporting
- Section 10: Access Control and Permissions
- Section 13: Reporting Requirements
