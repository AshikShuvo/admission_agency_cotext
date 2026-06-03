# Access Control and Role Visibility Flow

## Purpose

Ensure each user can access only the data needed for their role and cannot view restricted student, financial, document, or commission information.

## Primary Actors

- System
- Owner
- Consultant
- Accounts Department
- Admission Department
- Visa Department

## Trigger

A user logs in, opens a screen, performs an action, or requests data.

## Preconditions

- User account exists.
- User role is assigned.
- User is authenticated.

## Main Flow

1. User logs in.
2. System identifies the user's role.
3. User requests a list, detail page, report, or action.
4. System checks role permission for the requested feature.
5. System applies data scope filters:
   - Owner: all data
   - Consultant: assigned files only
   - Accounts: financial data only
   - Admission: admission-relevant data only
   - Visa: visa-relevant data only
6. If authorized, system returns the allowed data.
7. If unauthorized, system blocks access and records the attempt if needed.

## Role Visibility Summary

| Role | Allowed Scope |
|---|---|
| Owner | All files, all financials, commissions, users, catalog, reports |
| Consultant | Own assigned files, student profile, admission and visa status for own files, catalog browsing |
| Accounts | Payment records, dues, deposit confirmations, limited file/student identifiers |
| Admission | Admission documents, academic info, program details, admission approval actions |
| Visa | Visa documents, passport info, offer letter, visa approval actions |

## Restricted Data

- Consultant cannot view other consultants' files.
- Accounts cannot view document content or visa details beyond financial context.
- Admission cannot view commission data or visa-specific documents.
- Visa cannot view commission data or full financial details.
- Commission is Owner-only.

## Business Rules

- Least privilege is a core requirement.
- Access restrictions must be enforced at the query/data layer.
- UI hiding is not enough.
- Owner has unrestricted access.

## Outputs

- Authorized data response
- Blocked unauthorized action
- Optional access audit log

## Related Data

- User
- Role / Permission
- File
- Payment
- Document
- Commission

## Source Sections

- Section 4: Stakeholders and User Roles
- Section 10: Access Control and Permissions
- Section 11: Business Rules BR-004 and BR-006
