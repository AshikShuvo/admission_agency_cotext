# User Management Flow

## Purpose

Create, update, suspend, and audit internal staff user accounts so each employee has the correct business role before they can access student files, payments, documents, reports, catalog records, or commission information.

This flow describes account lifecycle management. Runtime permission checks are covered separately in [Access Control and Role Visibility](10_access_control_and_role_visibility_flow.md).

## Primary Actors

- Owner / Admin
- System
- Consultant / Counsellor, managed user
- Accounts Department User, managed user
- Admission Department User, managed user
- Visa Department User, managed user

## Trigger

A staff member joins the agency, changes department or responsibility, temporarily loses access, or leaves the agency.

## Preconditions

- Owner has system access.
- The staff member's name, contact details, department, and business role are known.
- The role model is already defined in [Users and Roles](../users_and_roles.md).

## Main Flow: Create Staff User

1. Owner opens user management.
2. Owner enters the staff member's full name, email, phone, and department.
3. Owner assigns exactly one primary business role:
   - Consultant / Counsellor
   - Accounts Department User
   - Admission Department User
   - Visa Department User
   - Owner / Admin, only for trusted owner-level users
4. System shows the access scope and restricted areas for the selected role.
5. Owner confirms the account creation.
6. System creates the user account as active or invited, depending on the login setup.
7. System records the Owner action in the audit or activity history.
8. Staff user can log in and sees only the screens, actions, and data allowed for their role.

## Main Flow: Update Staff Role or Details

1. Owner selects an existing active user.
2. Owner updates contact details, department, role, or account status.
3. System shows the new role scope before the change is confirmed.
4. Owner provides a business reason when changing role or access status.
5. System applies the new role from the next access check onward.
6. System keeps previous user activity linked to the same staff account.
7. System records who changed the user, what changed, when it changed, and why.

## Main Flow: Suspend Staff Access

1. Owner selects a staff user who should no longer access the system.
2. System warns that suspension removes login access but keeps business history intact.
3. Owner enters the suspension reason.
4. Owner confirms suspension.
5. System marks the user inactive or suspended.
6. System blocks future login and access for that user.
7. System keeps prior file creation, document uploads, payment confirmations, approvals, and activity records visible for audit.

## Alternate Flows

### Duplicate Email

If the email address is already used by another user, the system blocks account creation and asks Owner to use a unique login email.

### Unauthorized User Management Attempt

If Consultant, Accounts, Admission, or Visa users try to create users, change roles, or suspend staff, the system blocks the action.

### Reassign Work Before Suspension

If the suspended user is a Consultant with active student files, Owner should reassign those files or define a follow-up owner before suspension is finalized.

## Business Rules

- Only Owner / Admin can create, edit, activate, suspend, or deactivate staff users.
- Each internal user must have exactly one primary role unless Owner explicitly configures an exception.
- Non-owner roles cannot manage users or change their own role.
- User deletion should be avoided because historical actions must remain auditable.
- Suspending a user must remove login access without deleting their previous work history.
- Role changes must not rewrite past activity history.
- Owner-level account creation should be rare and treated as a sensitive business action.
- User management actions should be logged with actor, timestamp, changed fields, and reason.
- Student and University are external actors in Phase 1 and are not direct system users unless a future portal is approved.

## Role Creation Summary

| Role Created | Default Data Scope | Key Restrictions |
|---|---|---|
| Owner / Admin | All business data | No functional restriction by default; sensitive actions should be audited |
| Consultant / Counsellor | Own assigned student files and catalog browsing | Cannot confirm payments, view other consultants' files, manage users, manage catalog, or view commissions |
| Accounts Department User | Payment records, dues, deposit confirmations, and limited file identifiers | Cannot view document content, approve admission or visa stages, manage users, or view commissions |
| Admission Department User | Admission-stage files, admission documents, academic information, and admission actions | Cannot confirm payments, manage users, view commissions, or approve visa stages |
| Visa Department User | Visa-stage files, visa documents, passport and offer letter information, and visa outcome actions | Cannot confirm payments, manage users, view commissions, or approve admission stage |

## Outputs

- Active staff user account
- Updated role or contact details
- Suspended or inactive staff account
- User access audit record
- Preserved historical activity linked to the staff user

## Related Data

- User
- Role / Permission
- File assignment
- File Activity Log
- Notification

## Source Sections

- Section 4: Stakeholders and User Roles
- Section 9: Data Entities and Relationships, User
- Section 10: Access Control and Permissions
- Section 11: Business Rules BR-004, BR-006, and BR-008
