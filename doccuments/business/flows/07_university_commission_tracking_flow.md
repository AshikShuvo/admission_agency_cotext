# University Commission Tracking Flow

## Purpose

Track confidential university commission revenue after successful student enrollment.

## Primary Actors

- Owner
- University

## Trigger

A university pays commission to the agency for an enrolled student.

## Preconditions

- Student file exists.
- Student has enrolled or the file is completed.
- Commission amount is known.
- Owner has permission to enter commission data.

## Main Flow

1. University disburses commission to the agency.
2. Owner identifies the related student file and university.
3. Owner enters commission details:
   - Student file reference
   - University
   - Amount
   - Received date
   - Notes, if any
4. System stores the commission record.
5. System includes commission in owner-only revenue reports.
6. System hides commission data from all non-owner roles.

## Business Rules

- Commission records are visible only to the Owner.
- Only Owner can enter or modify commission data.
- Commission can use the university default rate or a student-specific override if needed.
- Commission revenue is included in Owner reports only.

## Outputs

- Commission record
- Owner-only commission report data
- Updated revenue summary

## Related Data

- Commission
- File
- University
- User

## Source Sections

- Section 6.4: University Commission Tracking
- Section 7.4: Revenue Reporting
- Section 10: Access Control and Permissions
- Section 11: Business Rules BR-006
