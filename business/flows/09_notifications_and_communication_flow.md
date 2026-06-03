# Notifications and Communication Flow

## Purpose

Notify the correct role when a file changes stage, payment is confirmed, documents are requested, or outcomes are received.

## Primary Actors

- System
- Consultant
- Accounts Department
- Admission Department
- Visa Department
- Owner
- Student, optional SMS/email

## Trigger

A tracked business event occurs.

## Preconditions

- User roles and file assignment are known.
- Notification preferences or delivery channels are configured.
- The triggering event is recorded.

## Main Flow

1. A business event occurs in the system.
2. System identifies the related file, stage, and actor.
3. System determines who should be notified.
4. System creates an in-app notification.
5. Optional future channels may send SMS or email to the student.
6. Notification remains linked to the file or task for follow-up.

## Notification Events

| Event | Notified To |
|---|---|
| New file created | Owner, Accounts |
| Payment confirmed | Consultant for own file, Admission or Visa if relevant |
| Document requested | Assigned Consultant |
| Document submitted | Admission or Visa Department |
| File moved to Admission | Admission Department |
| File moved to Visa | Visa Department |
| Visa outcome received | Consultant, Owner |
| File completed | Owner |

## Optional Student Communication

Future SMS or email notifications may include:

- Payment receipt confirmation
- Document requirement notification
- Offer letter received notification
- Visa outcome notification

## Business Rules

- Notifications must respect role visibility.
- Consultants should receive notifications only for assigned files.
- Commission-related notifications must be Owner-only.
- Student messaging is optional for Phase 1 unless confirmed by the client.

## Outputs

- In-app notification
- Optional SMS/email message
- Follow-up task indicator

## Related Data

- File
- User
- Document
- Payment
- Notification
- File Activity Log

## Source Sections

- Section 12: Notifications and Communication
- Section 10: Access Control and Permissions
