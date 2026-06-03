# Business Domain Documentation
## Student Abroad Admission Agency Management System

---

> **Document Type:** Business Domain Documentation  
> **Audience:** Software Developers, System Architects, Business Analysts  
> **Status:** Draft — Based on Initial Client Interview  
> **Last Updated:** May 2026 (Rev 2 — Program Package & Country/University Catalog added)  
> **Prepared By:** Business Analyst

---

## Table of Contents

1. [Business Overview](#1-business-overview)
2. [Business Goals & Objectives](#2-business-goals--objectives)
3. [Domain Glossary](#3-domain-glossary)
4. [Stakeholders & User Roles](#4-stakeholders--user-roles)
5. [Country, University & Program Catalog](#5-country-university--program-catalog)
6. [Core Business Processes](#6-core-business-processes)
7. [Financial Domain](#7-financial-domain)
8. [File Lifecycle & Status Model](#8-file-lifecycle--status-model)
9. [Data Entities & Relationships](#9-data-entities--relationships)
10. [Access Control & Permissions](#10-access-control--permissions)
11. [Business Rules](#11-business-rules)
12. [Notifications & Communication](#12-notifications--communication)
13. [Reporting Requirements](#13-reporting-requirements)
14. [Assumptions & Open Questions](#14-assumptions--open-questions)
15. [Recommended Enhancements](#15-recommended-enhancements)
16. [System Boundary Diagram (Textual)](#16-system-boundary-diagram-textual)

---

## 1. Business Overview

The agency is a **student abroad consultancy firm** operating primarily in Bangladesh. Its core business is to assist Bangladeshi students in gaining admission to universities in foreign countries, with **Malaysia** being the primary operational geography at this time.

The agency acts as an intermediary between prospective students and foreign universities. It:

- Counsels students on available programs and institutions
- Manages the student's application file from initial inquiry to departure
- Collects fees on behalf of itself and the universities
- Processes documentation for university admission and visa applications
- Earns revenue through **service charges from students** and **commissions from universities**

The agency operates as a **multi-department organization** with the following departments:

| Department | Primary Role |
|---|---|
| Consultant / Counselling | Student-facing; file creation and guidance |
| Accounts | Financial verification and payment tracking |
| Admission | Document management and university application |
| Visa | Visa document processing and submission |
| Management / Owner | Oversight, commission tracking, reporting |

---

## 2. Business Goals & Objectives

### Primary Business Goals

1. **Streamline the student file lifecycle** from first walk-in to university enrollment
2. **Ensure financial accuracy** by verifying all deposits before progressing a file
3. **Maintain departmental separation** — each department sees only what is relevant to their role
4. **Track revenue** from both student charges and university commissions
5. **Provide owner-level visibility** across all operations, revenue, and staff performance

### Software System Goals

1. Digitize and centralize all student file management
2. Enforce step-by-step approval workflows with payment gates
3. Restrict data visibility by role to protect business data and student privacy
4. Generate financial and operational reports for management decision-making
5. Track consultant-level performance (number of active files, completions)
6. Track partial payments and automatically compute dues

---

## 3. Domain Glossary

| Term | Definition |
|---|---|
| **File** | The central record of a student's journey through the agency. Created when a student is registered after showing interest in a program. Equivalent to a "Case" or "Application Record." |
| **Student** | A Bangladeshi individual seeking university admission abroad through the agency. |
| **Consultant** | An agency employee who counsels students, creates their file, and acts as the primary point of contact. Also called a Counsellor. |
| **Program** | A specific academic course/degree offered by a university (e.g., BSc Computer Science at XYZ University, Malaysia). |
| **University** | A foreign educational institution (primarily Malaysian) the student is seeking admission to. |
| **Admission Department** | Internal agency department that collects documents from consultants and submits official applications to universities. |
| **Visa Department** | Internal agency department that handles visa documentation and processing. |
| **Accounts Department** | Internal agency department responsible for receiving payments and confirming deposits. |
| **Agency Charge** | Fees collected by the agency for its consultancy and processing services. |
| **University Charge** | Admission fees and first-semester fees collected on behalf of the university. |
| **Commission** | A payment received by the agency from the university for each enrolled student. This is confidential — visible to the owner only. |
| **Partial Payment** | A payment made by the student that does not cover the total due amount for a given step. |
| **Due Amount** | The remaining balance owed by the student at any step (Total Charge - Amount Paid). |
| **Deposit Confirmation** | The act of the Accounts department verifying that a specific payment has been received into the agency's account. |
| **File Status** | The current stage of a student's file in the processing pipeline. |
| **Step Approval** | An internal approval action performed by a designated user/department to move a file to the next step. |
| **Country Catalog** | A managed list of destination countries (e.g., Malaysia, UK) that the agency supports. Universities are grouped under countries. |
| **University Catalog** | A managed list of partner universities, each linked to a country, containing general information about the institution. |
| **Program** | A specific academic course/degree offered by a university (e.g., BSc Computer Science at XYZ University, Malaysia). |
| **Program Package** | A pre-defined fee bundle attached to a specific program. It breaks down the total cost a student must pay — stage by stage (File Opening, Admission, Visa) — covering both agency charges and university charges. Used during counselling to give students full cost transparency. |
| **Stage-wise Fee Breakdown** | The portion of the Package that shows how much is due at each step of the process. Helps students plan finances and serves as a marketing tool for the agency. |
| **Total Package Cost** | The sum of all fees across all stages for a given program — i.e., everything a student will pay from file opening to departure. |

---

## 4. Stakeholders & User Roles

### 4.1 Role Definitions

#### Owner / Admin
- Top-level access to all data in the system
- Views all student files regardless of consultant
- Views all financial data including university commissions
- Views company-wide revenue reports (daily, monthly, yearly, date-range)
- Can configure the system (add users, set fee structures, register universities and programs)
- The only role that can input university commission data

#### Consultant (Counsellor)
- Agency employee who handles student-facing interactions
- Can create and manage files **only for students assigned to them**
- Can view the status of **only their own files**
- Cannot see other consultants' files or financial summaries beyond their own
- Responsible for gathering and submitting student documents to the admission department
- There may be **multiple consultants** working simultaneously

#### Accounts Department User
- Can view and manage **financial information only**
- Confirms payment deposits for any student file
- Can see all payment records, dues, and confirmation history
- Cannot see file status details, document content, or visa information beyond financial context
- Issues deposit confirmation that acts as a gate to proceed to the next step

#### Admission Department User
- Handles document collection and university application submission
- Views only the admission-relevant details of a file (required documents, document checklist, student academic info)
- Cannot see visa-specific details or commission data
- Requests documents from the consultant
- Approves the file to move to the visa stage after admission is confirmed

#### Visa Department User
- Handles visa-related documents (passport, university approval letter, etc.)
- Views only visa-relevant details of a file
- Cannot see admission-level document details or financial data (except what is needed for visa fee confirmation)
- Approves the file after visa processing is complete

---

### 4.2 Role Permission Matrix

| Feature / Data | Owner | Consultant | Accounts | Admission | Visa |
|---|:---:|:---:|:---:|:---:|:---:|
| View all files | ✅ | ❌ | ❌ | ❌ | ❌ |
| View own files | ✅ | ✅ | ❌ | ❌ | ❌ |
| Create file | ✅ | ✅ | ❌ | ❌ | ❌ |
| View financial data | ✅ | ❌ | ✅ | ❌ | ❌ |
| Confirm deposit | ✅ | ❌ | ✅ | ❌ | ❌ |
| View admission docs | ✅ | ✅ (own) | ❌ | ✅ | ❌ |
| Approve admission step | ✅ | ❌ | ❌ | ✅ | ❌ |
| View visa docs | ✅ | ✅ (own) | ❌ | ❌ | ✅ |
| Approve visa step | ✅ | ❌ | ❌ | ❌ | ✅ |
| View commissions | ✅ | ❌ | ❌ | ❌ | ❌ |
| Input commission | ✅ | ❌ | ❌ | ❌ | ❌ |
| View revenue report | ✅ | ❌ | ✅ (limited) | ❌ | ❌ |
| Manage users | ✅ | ❌ | ❌ | ❌ | ❌ |
| Manage countries | ✅ | ❌ | ❌ | ❌ | ❌ |
| Manage universities | ✅ | ❌ | ❌ | ❌ | ❌ |
| Manage programs | ✅ | ❌ | ❌ | ❌ | ❌ |
| Manage program packages | ✅ | ❌ | ❌ | ❌ | ❌ |
| View program catalog (browse) | ✅ | ✅ | ❌ | ❌ | ❌ |
| View package fee breakdown | ✅ | ✅ | ✅ (linked file only) | ❌ | ❌ |

---

## 5. Country, University & Program Catalog

### 5.1 Overview

The **Catalog** is the master reference layer of the system. Before any student file can be created, the agency owner must have populated the system with the countries they operate in, the universities they partner with in those countries, the programs each university offers, and the **Program Package** — the structured, stage-wise fee breakdown that tells a student exactly how much they will pay and at which step.

This catalog serves two distinct purposes:

1. **Internal Operational Use:** Consultants browse and select from the catalog when counselling students and creating files. The system auto-populates fee structures from the package when a file is created.
2. **Marketing & Transparency Tool:** The package's stage-wise cost breakdown gives prospective students a clear, trustworthy picture of the total investment required — what they pay upfront, at admission, and for visa processing — which aids the agency's counselling and marketing efforts.

Only the **Owner** can create, edit, or deactivate catalog entries. Consultants have read-only access to browse and select.

---

### 5.2 Country Management

Countries represent the destination nations the agency supports for university admissions.

**Managed by:** Owner only  
**Browsable by:** Consultants (read-only)

#### Country Entity

| Field | Type | Description |
|---|---|---|
| country_id | UUID | Unique identifier |
| name | String | Country name (e.g., Malaysia, United Kingdom, Canada) |
| code | String | ISO country code (e.g., MY, GB, CA) |
| currency | String | Primary currency for fees in that country (e.g., MYR, GBP, CAD) |
| visa_type | String | Type of student visa required (e.g., Malaysia Student Pass, UK Tier 4) |
| is_active | Boolean | Whether the agency currently operates in this country |
| notes | Text | Internal notes (embassy contacts, processing norms, etc.) |

#### Business Notes
- Currently only **Malaysia** is active. The system must support adding more countries as the business grows.
- Each country may have different visa rules, document requirements, and fee currencies — these are captured at the country and program levels.

---

### 5.3 University Management

Universities are the partner institutions within each country. Only universities added to the system can be selected when creating a student file.

**Managed by:** Owner only  
**Browsable by:** Consultants (read-only)

#### University Entity

| Field | Type | Description |
|---|---|---|
| university_id | UUID | Unique identifier |
| country_id | FK → Country | The country this university is in |
| name | String | Full university name |
| short_name | String | Abbreviation or commonly used name (e.g., UTM, MMU) |
| city | String | City where the university is located |
| address | Text | Full address |
| website | String | Official website URL |
| contact_email | String | Admission office email |
| contact_phone | String | Admission office phone |
| logo_url | String | Logo image path (for display in catalog) |
| commission_rate | Decimal | Default commission % or flat amount per student (Owner-visible only) |
| commission_type | Enum | PERCENTAGE / FLAT_AMOUNT |
| is_active | Boolean | Whether the agency is currently sending students here |
| notes | Text | Internal notes about the university relationship |

#### Business Notes
- Commission information on the university record is the **default**; individual student commission entries can override this if needed.
- Multiple universities per country are supported.

---

### 5.4 Program Management

Programs are the specific academic courses/degrees offered by a university. A university may have many programs. Programs are the unit the student selects during counselling.

**Managed by:** Owner only  
**Browsable by:** Consultants (read-only, with filter/search)

#### Program Entity

| Field | Type | Description |
|---|---|---|
| program_id | UUID | Unique identifier |
| university_id | FK → University | Linked university |
| name | String | Full program name (e.g., Bachelor of Computer Science) |
| short_name | String | Abbreviated name (e.g., BSc CS) |
| level | Enum | CERTIFICATE / DIPLOMA / BACHELOR / MASTER / PHD / SHORT_COURSE |
| field_of_study | String | Broad field (e.g., Engineering, Business, Health Sciences) |
| duration_years | Decimal | Program duration in years (e.g., 3.0, 3.5, 1.5) |
| intake_months | String | Months when intake is available (e.g., January, May, September) |
| entry_requirements | Text | Academic and language entry requirements |
| language_requirement | String | e.g., IELTS 6.0 / No IELTS required |
| is_active | Boolean | Whether this program is currently offered/available |
| notes | Text | Internal notes about the program |

#### Program Catalog — Consultant View
When a consultant is counselling a student, they need to **filter and search** programs by:
- Country
- University
- Level (Bachelor, Master, etc.)
- Field of study
- Intake month
- Student's academic background suitability

The consultant selects a program → the associated **Package** auto-loads to show the fee breakdown to the student.

---

### 5.5 Program Package (Fee Transparency)

The **Program Package** is the most important addition to the catalog. It is a structured, stage-wise fee template attached to each program. It defines:

- What the **total cost** is for a student to go through the entire process for this program
- How that cost is **split across the three processing stages**: File Opening, Admission, and Visa
- Within each stage, which portion goes to the **agency** and which portion goes to the **university**

When a student selects a program and the consultant creates a file, the system **automatically applies the package** to the file, pre-populating all fee amounts. This eliminates manual fee entry errors and ensures consistency.

**Managed by:** Owner only  
**Viewable by:** Consultants (during counselling), Accounts (linked to a specific file)

#### Package Entity

| Field | Type | Description |
|---|---|---|
| package_id | UUID | Unique identifier |
| program_id | FK → Program | The program this package belongs to |
| package_name | String | Display name (e.g., "BSc CS — Standard Package 2026") |
| currency | String | Primary currency (e.g., BDT, MYR) |
| is_active | Boolean | Whether this is the current valid package |
| valid_from | Date | Date from which this package is in effect |
| valid_until | Date | Expiry date (null = no expiry) |
| notes | Text | Internal notes |

#### Package Fee Line Items

Each package contains multiple **fee line items**, grouped by stage. This is the stage-wise breakdown:

| Field | Type | Description |
|---|---|---|
| line_item_id | UUID | Unique identifier |
| package_id | FK → Package | Parent package |
| stage | Enum | FILE_OPENING / ADMISSION / VISA |
| fee_label | String | Human-readable label (e.g., "Agency Service Charge", "University Admission Fee", "First Semester Fee", "Visa Processing Charge") |
| fee_type | Enum | AGENCY_CHARGE / UNIVERSITY_CHARGE / GOVERNMENT_FEE / OTHER |
| amount | Decimal | Fee amount in the package currency |
| is_mandatory | Boolean | Whether this fee is compulsory (some fees may be conditional) |
| description | Text | Explanation of what this fee covers |
| display_order | Integer | Order in which to show this line item to the student |

#### Package Summary View (for Counselling & Marketing)

The system must be able to generate a **Package Summary** — a clean, student-facing cost breakdown — from the package line items. Example:

```
PROGRAM:  Bachelor of Computer Science
UNIVERSITY:  XYZ University, Kuala Lumpur, Malaysia
DURATION:  3 Years  |  INTAKE: January, May, September

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
STAGE 1 — FILE OPENING
  Agency Service Charge         BDT 15,000
  ─────────────────────────────────────────
  Stage 1 Total                 BDT 15,000

STAGE 2 — ADMISSION
  University Admission Fee      BDT 30,000
  First Semester Fee            BDT 50,000
  Agency Admission Processing   BDT 10,000
  ─────────────────────────────────────────
  Stage 2 Total                 BDT 90,000

STAGE 3 — VISA PROCESSING
  Agency Visa Processing Fee    BDT 10,000
  Embassy / Government Visa Fee BDT  8,000
  ─────────────────────────────────────────
  Stage 3 Total                 BDT 18,000

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
TOTAL PACKAGE COST              BDT 1,23,000
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

> **Note:** Partial payments are accepted at each stage. The above amounts represent the total due per stage, not a single lump-sum payment requirement.

#### Package Versioning
- A program may have multiple packages over time (e.g., fees change year to year)
- Only one package should be **active** per program at a time
- When a file is created, the **current active package** is snapshot-copied onto the file so that future changes to the package do not affect existing files
- Historical files retain their original fee amounts

---

### 5.6 Package Use in Counselling & Marketing

#### During Counselling (Internal Use)
1. Consultant filters the program catalog to find suitable programs for the student
2. Consultant clicks a program → the Package Summary loads instantly, showing the stage-wise cost breakdown
3. Consultant presents this breakdown to the student
4. Student can see clearly: "I need to pay BDT 15,000 to open my file, then BDT 90,000 at admission, then BDT 18,000 for visa"
5. Student decides to proceed → Consultant creates a file → System auto-applies the package fees to the file

#### For Marketing (Future Use — see Section 15)
- The package summary could be displayed on a public-facing web page or printed as a brochure for each destination/program
- Students can compare total costs across programs before visiting the office
- This builds trust and differentiates the agency from competitors who are not transparent about costs

#### Key Business Value
- **Reduces consultant error** — fees are pre-configured, not typed manually each time
- **Builds student trust** — no surprise fees; everything is shown upfront per stage
- **Speeds up counselling** — consultant doesn't have to recall or calculate fees on the spot
- **Enables comparison** — students can compare packages across universities before deciding
- **Supports marketing** — a printed or digital package sheet is a powerful sales tool

---



## 6. Core Business Processes

### 6.1 File Opening Process

#### Trigger
A student walks into the agency office seeking guidance for university admission abroad.

#### Steps

1. **Student Walk-In & Counselling**
   - A consultant is assigned to the student (manually by management or via a queue)
   - The consultant shows the student a list of available programs across various universities (primarily Malaysian universities)
   - Programs are shown with relevant details: university name, program name, duration, tuition fees, entry requirements

2. **Program Selection**
   - The student selects a program they are interested in
   - If the student has not decided on a specific university, the consultant assists them in narrowing down options based on the student's academic background and preferences

3. **File Registration**
   - Once the student is convinced and decides to proceed, the consultant creates a **File** in the system
   - The file is linked to:
     - The student's personal details
     - The selected program and university
     - The assigned consultant
   - The file is assigned a unique **File ID / File Number**
   - File status is set to: `File Opened`

4. **Fee Quotation**
   - The consultant presents the student with the full fee breakdown:
     - Agency service charge (for file opening and processing)
     - University admission fee
     - University first-semester fee
   - The student may pay in full or make a partial payment at this stage

5. **Payment & Deposit Confirmation**
   - Student pays (fully or partially) the agency's file-opening charge
   - Payment is submitted to the **Accounts Department**
   - Accounts verifies the deposit and confirms it in the system
   - Upon confirmation, the file is eligible to progress to the Admission stage
   - If payment is partial, the due balance is recorded and tracked

#### File Opened — Checklist
- [ ] Student registered in system
- [ ] Program and university selected
- [ ] File created and assigned to consultant
- [ ] Fee quotation generated
- [ ] At least minimum payment received and confirmed by accounts

---

### 6.2 Admission Process

#### Trigger
The file has been confirmed (deposit verified by accounts) at the file opening stage.

#### Steps

1. **Document Request**
   - The **Admission Department** reviews the file and generates a checklist of required documents for the selected university/program
   - The admission officer sends a document request to the **Consultant** associated with the file

2. **Document Submission by Consultant**
   - The consultant collects the required documents from the student
   - Documents may include: academic certificates, transcripts, English language scores (IELTS/TOEFL), NID/birth certificate, photographs, etc.
   - Consultant uploads or submits documents through the system

3. **Document Verification**
   - The Admission Department verifies the documents are complete and valid
   - If documents are missing or incorrect, the admission officer sends a request back to the consultant for re-submission

4. **Fee Collection — Admission Stage**
   - University admission fees (and any additional agency processing fees for this stage) are collected from the student
   - Payments go to the **Accounts Department** for deposit confirmation
   - The file cannot proceed until the payment for this stage is confirmed

5. **University Application Submission**
   - Once documents are complete and fees are confirmed, the Admission Department submits the application to the university
   - The system records the submission date and expected response timeline

6. **University Acceptance**
   - The university issues an **Offer Letter** or **Acceptance Letter**
   - The admission officer uploads the acceptance letter to the file
   - The file status is updated

7. **Admission Stage Approval**
   - The Admission Department marks the admission step as **Approved**
   - The file progresses to the Visa Processing stage

#### Admission Stage — Fee Payment Gate
> **Rule:** The file cannot be approved for university submission without deposit confirmation from the Accounts Department for all admission-stage fees. Partial payments are allowed, but the due balance must be tracked.

#### Admission Stage — Checklist
- [ ] Document checklist generated
- [ ] All documents received from consultant
- [ ] Documents verified and complete
- [ ] Admission fees paid and confirmed by accounts
- [ ] University application submitted
- [ ] University acceptance/offer letter received
- [ ] Admission step approved

---

### 6.3 Visa Processing

#### Trigger
The Admission stage has been approved and the student has a university acceptance letter.

#### Steps

1. **Visa Document Request**
   - The **Visa Department** reviews the file and creates a checklist of visa-required documents
   - Typical documents: passport (valid), university acceptance letter, financial statements, medical certificate, police clearance, photographs, visa application form

2. **Document Collection**
   - The Visa Department works with the consultant (and directly with the student when needed) to gather the required documents
   - Documents are uploaded to the file

3. **Visa Fee Collection**
   - Visa-related charges are collected:
     - Agency visa processing fee
     - Government/Embassy visa fee (paid externally but tracked)
   - Payments go to **Accounts Department** for deposit confirmation
   - File cannot proceed without payment confirmation at this stage

4. **Visa Application Submission**
   - The Visa Department submits the visa application to the relevant embassy or immigration authority
   - Submission date is recorded

5. **Visa Outcome**
   - **Visa Approved:** Visa is stamped on the passport. The file is updated with the visa issue date and expiry date.
   - **Visa Rejected:** The file is flagged. A reason is recorded. The case may be re-applied or closed.

6. **Pre-Departure**
   - Flight and travel arrangements may be noted (optional, for record-keeping)
   - The file is marked **Completed / Student Sent** once the student departs

7. **Visa Stage Approval**
   - The Visa Department marks the visa step as **Approved / Completed**
   - The file status moves to `Completed`

#### Visa Stage — Checklist
- [ ] Visa document checklist generated
- [ ] All visa documents collected and verified
- [ ] Visa fees paid and confirmed by accounts
- [ ] Visa application submitted
- [ ] Visa outcome recorded (Approved / Rejected)
- [ ] Visa step approved / file closed

---

### 6.4 University Commission Tracking

#### Overview
After a student is successfully enrolled at a university, the university pays a **commission** to the agency. This is a revenue source that is **confidential** and visible only to the **Owner**.

#### Process

1. The university disburses commission (typically per enrolled student)
2. The **Owner** enters the commission amount into the system, linked to the specific student file
3. The system records:
   - Amount received
   - University name
   - Student file reference
   - Date received
4. Commission data is included in the Owner's revenue reports but is **hidden from all other roles**

---

## 7. Financial Domain

### 7.1 Fee Structure

Each student file may carry multiple types of fees across different stages:

| Fee Type | Stage | Paid By | Collected By | Visible To |
|---|---|---|---|---|
| Agency File Opening Fee | File Opening | Student | Accounts | Accounts, Owner |
| University Admission Fee | Admission | Student | Accounts | Accounts, Owner |
| Agency Admission Processing Fee | Admission | Student | Accounts | Accounts, Owner |
| Visa Processing Fee (Agency) | Visa | Student | Accounts | Accounts, Owner |
| Visa Fee (Embassy/Government) | Visa | Student | Accounts (tracked) | Accounts, Owner |
| University Commission | Post-Enrollment | University | Owner Entry | Owner only |

> **Note:** The exact fee amounts may vary by university, program, and student case. The system should support configurable fee templates per university/program.

---

### 7.2 Payment & Partial Payment

- A student may pay any fee **in full or partially** at any point during the process
- Each payment record must capture:
  - Amount paid
  - Date of payment
  - Payment method (cash, bank transfer, mobile banking — bKash/Nagad etc.)
  - Stage the payment belongs to (File Opening / Admission / Visa)
  - Reference / receipt number (if applicable)
  - Student file ID
  - Recorded by (which accounts user entered it)

- **Partial payments are allowed at every stage**
- The system must allow multiple payment entries against a single fee stage

---

### 7.3 Due Calculation

The system must automatically calculate and display the **due (outstanding) balance** for each stage:

```
Due Amount (per stage) = Total Fee for Stage - Sum of All Confirmed Payments for Stage
```

- Due amounts are displayed:
  - On the student file (per stage)
  - In the accounts department dashboard
  - In the owner's file summary view

- A stage is considered **financially cleared** when `Due Amount = 0`
- A stage **cannot be approved** if the due amount is greater than zero, unless the owner manually overrides (to be decided — see Open Questions)

---

### 7.4 Revenue Reporting

The system must provide revenue reports with the following capabilities:

| Report | Description | Available To |
|---|---|---|
| Total Revenue by Date Range | Sum of all student payments received within a period | Owner, Accounts |
| Revenue by Stage | Breakdown of income by File Opening / Admission / Visa stages | Owner |
| Commission Revenue | Total commissions received from universities | Owner only |
| Revenue by Consultant | Total fees collected for files handled by each consultant | Owner |
| Revenue by University | Total fees and commissions per university | Owner |
| Outstanding Dues Report | List of all files with pending payments | Owner, Accounts |
| Monthly Revenue Summary | Month-by-month revenue breakdown | Owner |
| Yearly Revenue Summary | Year-by-year revenue breakdown | Owner |

---

## 8. File Lifecycle & Status Model

### File Status Flow

```
[Student Walk-in]
      │
      ▼
[File Opened] ──── Pending Payment ──► [Payment Confirmed (File Opening)]
                                                    │
                                                    ▼
                                        [Admission In Progress]
                                          ├── Document Requested
                                          ├── Documents Submitted
                                          ├── Documents Verified
                                          ├── Payment Confirmed (Admission)
                                          └── Application Submitted to University
                                                    │
                                         [Offer Letter Received]
                                                    │
                                         [Admission Approved]
                                                    │
                                                    ▼
                                        [Visa In Progress]
                                          ├── Visa Documents Requested
                                          ├── Visa Documents Submitted
                                          ├── Payment Confirmed (Visa)
                                          └── Visa Application Submitted
                                                    │
                                        ┌───────────┴───────────┐
                                        ▼                       ▼
                               [Visa Approved]          [Visa Rejected]
                                        │
                               [Student Departed / Completed]
```

### File Status Definitions

| Status | Description |
|---|---|
| `File Opened` | File has been created; initial payment may be pending |
| `Pending Payment - File Opening` | Awaiting deposit confirmation for file opening fees |
| `Admission In Progress` | File has passed to admission department for processing |
| `Pending Payment - Admission` | Awaiting deposit confirmation for admission fees |
| `Documents Pending` | Admission department has requested documents from consultant |
| `Application Submitted` | University application has been submitted |
| `Offer Letter Received` | University has issued acceptance |
| `Admission Approved` | Admission step fully completed |
| `Visa In Progress` | File has passed to visa department |
| `Pending Payment - Visa` | Awaiting deposit confirmation for visa fees |
| `Visa Applied` | Visa application has been submitted to embassy |
| `Visa Approved` | Student's visa has been granted |
| `Visa Rejected` | Visa application was rejected |
| `Completed` | Student has departed / enrollment confirmed |
| `On Hold` | File is temporarily paused (reason must be noted) |
| `Cancelled` | File has been cancelled / student withdrew |

---

## 9. Data Entities & Relationships

### Core Entities

#### Student
| Field | Type | Description |
|---|---|---|
| student_id | UUID | Unique identifier |
| full_name | String | Student's full name |
| date_of_birth | Date | Date of birth |
| national_id | String | NID / Birth Certificate number |
| passport_number | String | Passport number (if available) |
| passport_expiry | Date | Passport expiry date |
| phone | String | Contact phone number |
| email | String | Email address |
| address | Text | Permanent address |
| guardian_name | String | Parent / guardian name |
| guardian_phone | String | Guardian contact number |
| academic_background | Text | Last completed qualification details |
| english_score | String | IELTS / TOEFL score (if any) |
| created_at | DateTime | Record creation timestamp |

#### File (Case)
| Field | Type | Description |
|---|---|---|
| file_id | UUID | Unique file identifier |
| file_number | String | Human-readable file number (e.g., AGN-2026-00123) |
| student_id | FK → Student | Linked student |
| consultant_id | FK → User | Assigned consultant |
| university_id | FK → University | Target university |
| program_id | FK → Program | Selected program |
| status | Enum | Current file status |
| opened_date | Date | Date the file was created |
| completed_date | Date | Date the file was completed (null if ongoing) |
| notes | Text | General notes |
| is_active | Boolean | Whether the file is active |

#### Country
| Field | Type | Description |
|---|---|---|
| country_id | UUID | Unique identifier |
| name | String | Country name (e.g., Malaysia, United Kingdom) |
| code | String | ISO country code (e.g., MY, GB) |
| currency | String | Primary currency for fees (e.g., MYR, GBP) |
| visa_type | String | Student visa type name |
| is_active | Boolean | Whether the agency currently operates here |
| notes | Text | Internal notes |

#### University
| Field | Type | Description |
|---|---|---|
| university_id | UUID | Unique identifier |
| country_id | FK → Country | Country this university is in |
| name | String | Full university name |
| short_name | String | Common abbreviation (e.g., UTM, MMU) |
| city | String | City |
| address | Text | Full address |
| website | String | University website |
| contact_email | String | Admission office email |
| contact_phone | String | Admission office phone |
| logo_url | String | Logo image for display |
| commission_rate | Decimal | Default commission per student (Owner-visible only) |
| commission_type | Enum | PERCENTAGE / FLAT_AMOUNT |
| is_active | Boolean | Active partner university |
| notes | Text | Internal notes |

#### Program
| Field | Type | Description |
|---|---|---|
| program_id | UUID | Unique identifier |
| university_id | FK → University | Linked university |
| name | String | Program name (e.g., BSc Computer Science) |
| short_name | String | Abbreviated name |
| level | Enum | CERTIFICATE / DIPLOMA / BACHELOR / MASTER / PHD |
| field_of_study | String | Broad academic field |
| duration_years | Decimal | Duration in years |
| intake_months | String | Available intake months |
| entry_requirements | Text | Academic and language requirements |
| language_requirement | String | Language score needed (e.g., IELTS 6.0) |
| is_active | Boolean | Currently available program |
| notes | Text | Internal notes |

#### Package
| Field | Type | Description |
|---|---|---|
| package_id | UUID | Unique identifier |
| program_id | FK → Program | Program this package belongs to |
| package_name | String | Display name (e.g., "BSc CS — Standard 2026") |
| currency | String | Currency for all amounts in this package |
| is_active | Boolean | Current active package for this program |
| valid_from | Date | Effective start date |
| valid_until | Date | Expiry date (null = open-ended) |
| notes | Text | Internal notes |

#### Package Fee Line Item
| Field | Type | Description |
|---|---|---|
| line_item_id | UUID | Unique identifier |
| package_id | FK → Package | Parent package |
| stage | Enum | FILE_OPENING / ADMISSION / VISA |
| fee_label | String | Display label (e.g., "Agency Service Charge") |
| fee_type | Enum | AGENCY_CHARGE / UNIVERSITY_CHARGE / GOVERNMENT_FEE / OTHER |
| amount | Decimal | Fee amount |
| is_mandatory | Boolean | Whether compulsory for all students |
| description | Text | What this fee covers |
| display_order | Integer | Sort order for display |



#### Payment
| Field | Type | Description |
|---|---|---|
| payment_id | UUID | Unique identifier |
| file_id | FK → File | Linked file |
| stage | Enum | FILE_OPENING / ADMISSION / VISA / OTHER |
| amount | Decimal | Amount paid |
| payment_date | Date | Date of payment |
| payment_method | Enum | CASH / BANK_TRANSFER / BKASH / NAGAD / OTHER |
| reference_number | String | Bank slip or transaction reference |
| recorded_by | FK → User | Accounts user who recorded it |
| is_confirmed | Boolean | Whether deposit has been confirmed |
| confirmed_by | FK → User | Accounts user who confirmed |
| confirmed_at | DateTime | Confirmation timestamp |
| notes | Text | Any notes |

#### Fee Structure (per File Stage)
| Field | Type | Description |
|---|---|---|
| fee_id | UUID | Unique identifier |
| file_id | FK → File | Linked file |
| stage | Enum | FILE_OPENING / ADMISSION / VISA |
| fee_type | String | Agency Fee / University Admission Fee / etc. |
| total_amount | Decimal | Total amount due for this fee |
| currency | String | BDT / USD / MYR |

#### Commission
| Field | Type | Description |
|---|---|---|
| commission_id | UUID | Unique identifier |
| file_id | FK → File | Linked student file |
| university_id | FK → University | Paying university |
| amount | Decimal | Commission amount received |
| received_date | Date | Date received |
| entered_by | FK → User (Owner only) | Who entered this record |
| notes | Text | Any notes |

#### Document
| Field | Type | Description |
|---|---|---|
| document_id | UUID | Unique identifier |
| file_id | FK → File | Linked file |
| stage | Enum | ADMISSION / VISA |
| document_type | String | Passport / Transcript / Offer Letter / etc. |
| uploaded_by | FK → User | Who uploaded |
| upload_date | DateTime | When uploaded |
| file_path | String | Storage path |
| status | Enum | PENDING / SUBMITTED / VERIFIED / REJECTED |
| notes | Text | Reviewer notes |

#### User
| Field | Type | Description |
|---|---|---|
| user_id | UUID | Unique identifier |
| full_name | String | Full name |
| email | String | Login email |
| phone | String | Contact phone |
| role | Enum | OWNER / CONSULTANT / ACCOUNTS / ADMISSION / VISA |
| is_active | Boolean | Account active |
| created_at | DateTime | Account creation date |

#### File Activity Log
| Field | Type | Description |
|---|---|---|
| log_id | UUID | Unique identifier |
| file_id | FK → File | Linked file |
| action | String | Description of action taken |
| performed_by | FK → User | Who performed the action |
| timestamp | DateTime | When the action occurred |
| notes | Text | Any additional context |

---

### Entity Relationship Summary

```
Country ──< University ──< Program ──< Package ──< Package Fee Line Items
                               │
User (Consultant) ──< File >── Student
                       │  └── package_snapshot (fee amounts copied at file creation)
               ┌───────┼────────────────────────┐
               │       │                        │
           University  Program              Payments
               │                         (multiple, per stage)
               │
          Commission (Owner only)
               │
           Documents (per stage)
               │
       File Activity Log
```

---

## 10. Access Control & Permissions

### Principle of Least Privilege
Every user role sees only the minimum data required to perform their job. This is a core business requirement.

### Consultant File Isolation
- A consultant can only see files they personally created or are assigned to
- Consultant A cannot see Consultant B's files in any view — not the list, not the detail, not reports
- The system must enforce this at the **query/data layer**, not just the UI layer

### Accounts Department Scope
- Accounts users can see **all files' financial data** (payments, dues, confirmations) but **only financial data**
- They see student names and file numbers for reference, but **not** document details, program specifics, or visa information

### Admission Department Scope
- Admission users see files that are in the **Admission In Progress** stage or later
- They see document checklists, student academic info, program details
- They do **not** see visa documents or commission data

### Visa Department Scope
- Visa users see files that are in the **Visa In Progress** stage
- They see visa-related documents, passport info, acceptance letters
- They do **not** see admission-stage documents or financial details (except the visa fee payment confirmation status)

### Owner / Admin
- Full unrestricted access to all data, all files, all departments, all reports
- Exclusive access to commission data

---

## 11. Business Rules

### BR-001: Payment Gate Rule
> A file **cannot be moved to the next processing stage** until all required payments for the current stage have been confirmed by the Accounts Department.

### BR-002: Partial Payment Allowed
> A student may make partial payments at any stage. The system must record each payment separately and calculate the outstanding due amount automatically.

### BR-003: Deposit Must Be Confirmed by Accounts
> Only a user with the **Accounts** role may confirm that a deposit has been received. Self-confirmation by a consultant is not permitted.

### BR-004: Consultant File Isolation
> A consultant may only view, edit, or take action on files assigned to them. Access to other consultants' files is strictly prohibited at the system level.

### BR-005: Step Approval Authority
> Each stage has a designated approving role:
> - File Opening Payment → Accounts Department
> - Admission Stage → Admission Department (after payment confirmed)
> - Visa Stage → Visa Department (after payment confirmed)
> - Overall visibility → Owner

### BR-006: Commission Confidentiality
> University commission amounts and records are accessible only to the **Owner** role. No other role may view, enter, or modify commission data.

### BR-007: File Number Uniqueness
> Every file must have a unique, system-generated file number (e.g., AGN-2026-00123) that is human-readable and can be referenced in physical correspondence.

### BR-008: Document Audit Trail
> All document uploads, status changes, and approvals must be logged with the user who performed the action and the timestamp.

### BR-009: File Status Immutability on Completion
> Once a file is marked `Completed` or `Cancelled`, it cannot be edited without explicit owner-level authorization.

### BR-010: Visa Rejection Handling
> If a visa is rejected, the file is flagged with status `Visa Rejected`. The owner must decide whether to re-apply or close the file. A re-application restarts the visa stage without losing existing records.

### BR-011: Due Calculation Automatic
> The system automatically calculates and displays `Due Amount = Total Fee - Total Confirmed Payments` at every stage. Manual overrides require owner approval (if allowed — see Open Questions).

### BR-012: Only One Active Package Per Program
> At any given time, only one Package may be marked `is_active = true` for a given program. When a new package is created and activated, the previous one is automatically deactivated.

### BR-013: Package Snapshot on File Creation
> When a consultant creates a file and links it to a program, the system must **copy (snapshot) the current active package's fee line items** directly onto the file's fee records. This ensures that future changes to the package template do not alter the agreed fees for existing student files.

### BR-014: Catalog Management is Owner-Only
> Only the Owner role may create, edit, or deactivate Country, University, Program, and Package records. Consultants have read-only browsing access to the catalog.

### BR-015: Program Must Have an Active Package Before File Creation
> A consultant cannot create a student file for a program that does not have an active Package attached to it. The Owner must configure the package first.

---

## 12. Notifications & Communication

> *(These are standard best-practice recommendations for a business of this type. To be confirmed with the client.)*

### Internal Notifications (In-App)

| Event | Notified To |
|---|---|
| New file created | Owner, Accounts |
| Payment confirmed | Consultant (their file), Admission/Visa (if relevant stage) |
| Document requested | Consultant |
| Document submitted | Admission/Visa department |
| File moved to Admission stage | Admission Department |
| File moved to Visa stage | Visa Department |
| Visa outcome received | Consultant, Owner |
| File completed | Owner |

### Optional: SMS / Email Notifications to Student
- Payment receipt confirmation
- Document requirement notification
- Offer letter received notification
- Visa outcome notification

---

## 13. Reporting Requirements

### Owner Dashboard
- Total open files (count)
- Files by status (breakdown)
- Files by consultant (count per consultant)
- Revenue summary: current month, current year
- Outstanding dues (total across all files)
- Recent activity log

### Consultant Dashboard
- My open files (count and list)
- Files by status (only their files)
- Pending document requests
- Upcoming tasks

### Accounts Dashboard
- Payments received today / this week / this month
- Files with outstanding dues
- Pending deposit confirmations (payments entered but not yet confirmed)
- Revenue by payment stage

### Operational Reports

| Report Name | Filter Options | Available To |
|---|---|---|
| File Status Report | Date range, Status, Consultant | Owner |
| Consultant Performance Report | Date range, Consultant name | Owner |
| Revenue Report | Date range, Stage, University | Owner, Accounts |
| Commission Report | Date range, University | Owner only |
| Outstanding Dues Report | Stage, Date range | Owner, Accounts |
| University-wise Enrollment Report | University, Year | Owner |

---

## 14. Assumptions & Open Questions

### Assumptions Made
1. The primary operational country is Malaysia; the system should be designed to support other countries in the future (e.g., UK, Canada, Australia) as the business grows.
2. Payments are currently made in-person (cash or bank transfer). Online payment gateway integration is not in scope for Phase 1 but should be architecturally feasible.
3. Mobile banking methods (bKash, Nagad) are common in Bangladesh and should be supported as payment method types.
4. The system is web-based and accessible from a browser; mobile app is not in Phase 1 scope.
5. Currency is primarily BDT (Bangladeshi Taka), but some fees may be in USD or MYR and should be storable.
6. The agency has a single office location currently.
7. File deletion is not permitted — only cancellation (soft delete), to maintain audit trails.

### Open Questions for Client

| # | Question | Impact |
|---|---|---|
| OQ-01 | Can a student be registered without selecting a specific program (undecided students)? How is the file handled until a program is chosen? | File creation flow |
| OQ-02 | Can a consultant be reassigned to a different student's file? If yes, who has authority to do this? | File management, access control |
| OQ-03 | Is there a minimum payment required before a file is formally opened, or can the file be opened and payment collected later? | Business rule, file opening flow |
| OQ-04 | Can the Owner override a payment gate (approve a stage even if full payment hasn't been confirmed)? | Business rule BR-011 |
| OQ-05 | How are rejected visa files handled? Can a student re-apply through the same file, or is a new file opened? | File lifecycle, visa process |
| OQ-06 | Are there any Service Level Agreement (SLA) timelines? (e.g., document submission within X days of request) | Notification and escalation logic |
| OQ-07 | Does the agency track student communication history (calls, messages, meetings)? | CRM scope |
| OQ-08 | Is there a specific format or number series required for file numbers? | File ID generation |
| OQ-09 | Are university commission rates fixed per university or variable per student? | Commission data model |
| OQ-10 | Do multiple students ever share a file (e.g., sibling applications)? | Data model assumption |
| OQ-11 | Should the system support document expiry tracking? (e.g., passport expiry, IELTS validity) | Document management |
| OQ-12 | Is there a referral system? (students referred by others) | Revenue and marketing tracking |
| OQ-13 | Can a consultant propose a custom fee for a specific student (deviation from the package)? If yes, who approves it? | Package flexibility, business rule |
| OQ-14 | Should the package summary be printable as a PDF brochure / quotation letter for the student to take home? | Feature scope, document generation |
| OQ-15 | When fees change (e.g., university raises admission fee), should existing open files be updated or remain at the original quoted amount? | Package versioning business rule |

---

## 15. Recommended Enhancements

Based on standard practice for similar consultancy agencies in Bangladesh, the following enhancements are recommended for consideration:

### Phase 1 (Core)
- All features described above

### Phase 2 (Enhancement)
1. **Student Portal (Read-Only):** Allow students to log in and view their own file status and payment receipts — reduces consultant workload for status inquiries
2. **Document Expiry Alerts:** Alert the relevant department when key documents (passport, IELTS) are nearing expiry
3. **SMS/Email Automation:** Automated messages to students on key milestones
4. **Referral Tracking:** Track which students came through referrals for marketing analysis
5. **University Program Catalog:** A searchable, filterable program catalog for consultants to use during counselling
6. **Package PDF Export:** Generate a printable, branded quotation/brochure PDF from any Package — for the student to take home or share with family
7. **Public Program Catalog Page:** A public-facing web page showing available programs and their package cost summaries — serves as a digital marketing tool for the agency

### Phase 3 (Scale)
1. **Multi-Country Support:** Expand beyond Malaysia to UK, Canada, Australia, etc.
2. **Multi-Branch Support:** Support for multiple office locations
3. **Mobile App:** For consultants to manage files on the go
4. **Analytics Dashboard:** Advanced insights — conversion rates, average processing time, student source analysis

---

## 16. System Boundary Diagram (Textual)

```
┌──────────────────────────────────────────────────────────────────────────┐
│                        AGENCY MANAGEMENT SYSTEM                          │
│                                                                          │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐    │
│  │  Consultant  │  │  Accounts   │  │  Admission  │  │    Visa     │    │
│  │   Module    │  │   Module    │  │   Module    │  │   Module    │    │
│  │             │  │             │  │             │  │             │    │
│  │ - File Mgmt │  │ - Payments  │  │ - Doc Mgmt  │  │ - Visa Docs │    │
│  │ - Program   │  │ - Dues      │  │ - Checklist │  │ - Checklist │    │
│  │   Browsing  │  │ - Confirm   │  │ - Approval  │  │ - Approval  │    │
│  │ - Student   │  │ - Reports   │  │             │  │             │    │
│  │   Profile   │  │             │  │             │  │             │    │
│  └──────┬──────┘  └──────┬──────┘  └──────┬──────┘  └──────┬──────┘    │
│         │                │                │                │            │
│         └────────────────┴────────────────┴────────────────┘            │
│                                    │                                     │
│                          ┌─────────▼──────────┐                         │
│                          │    File & Student   │                         │
│                          │    Core Database    │                         │
│                          └─────────┬──────────┘                         │
│                                    │                                     │
│                          ┌─────────▼──────────┐                         │
│                          │   Owner / Admin     │                         │
│                          │   Dashboard         │                         │
│                          │ - All files         │                         │
│                          │ - All financials    │                         │
│                          │ - Commissions       │                         │
│                          │ - Full Reports      │                         │
│                          └────────────────────┘                         │
└──────────────────────────────────────────────────────────────────────────┘
         │                                          │
         ▼                                          ▼
  [Student]                               [Universities (External)]
  Walks in, pays,                         Receive applications,
  submits docs                            issue offers, pay commissions
```

---

*End of Document*

---

> **Note to Developers:** This document reflects the business domain as understood from an initial client conversation. Some requirements may be subject to change upon further client review. All Open Questions (Section 13) should be resolved before development of affected features begins. It is strongly recommended to review this document with the client and obtain sign-off before commencing development.
