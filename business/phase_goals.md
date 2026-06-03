# Phase Goals
## Student Abroad Admission Agency Management System

This document describes the business expectations for building the software in three phases. It is not a technical document. It explains what the business should be able to achieve in each phase and which business flows should be completed in that phase.

Source documents:

- [Business Domain Documentation](business_domain_documentation.md)
- [Business Flows Index](flows/00_business_flows_index.md)
- [Users and Roles](users_and_roles.md)

## Overall Goal

The goal is to build the software step by step so the agency can first run its daily operation reliably, then improve efficiency and visibility, and finally scale the business with better automation, public-facing services, and multi-country or multi-branch support.

## Phase Summary

| Phase | Main Goal | Business Expectation |
|---|---|---|
| Phase 1 | Core Operation | Run the complete student file lifecycle from counselling to completion with payments, documents, role access, and basic reporting. |
| Phase 2 | Efficiency and Communication | Reduce manual follow-up, improve student/consultant visibility, add better communication, and support marketing materials. |
| Phase 3 | Scale and Growth | Expand the business to multiple countries, branches, advanced analytics, and stronger public/customer-facing services. |

## Phase 1: Core Operation

### Goal

Build the minimum complete business system needed to run the agency's daily operation in a controlled and trackable way.

By the end of Phase 1, the agency should be able to manage a student from first counselling to file completion inside the system.

### Business Expectations

- Owner can set up countries, universities, programs, and program packages.
- Consultant can browse programs and explain package costs to students.
- Consultant can create student files.
- Each student file has a clear status and assigned consultant.
- Accounts can record payments, confirm deposits, and track dues.
- Admission Department can manage admission documents and university application steps.
- Visa Department can manage visa documents, visa application, and visa outcome.
- Owner can view all files, revenue, reports, and commission information.
- Each role can only see the information relevant to their job.
- The system can track completed, cancelled, on-hold, and visa-rejected files.

### Flows To Complete In Phase 1

| Flow | Why It Is Needed In Phase 1 |
|---|---|
| [Catalog and Package Setup](flows/01_catalog_and_package_setup_flow.md) | Needed before consultants can select programs and create files. |
| [Counselling and Program Selection](flows/02_counselling_and_program_selection_flow.md) | Needed to guide students and select the right program. |
| [File Opening](flows/03_file_opening_flow.md) | Needed to create the central student file and start processing. |
| [Payment and Deposit Confirmation](flows/04_payment_and_deposit_confirmation_flow.md) | Needed to enforce payment gates and track dues. |
| [Admission Processing](flows/05_admission_processing_flow.md) | Needed to submit university applications and receive offer letters. |
| [Visa Processing](flows/06_visa_processing_flow.md) | Needed to process visa applications and complete student cases. |
| [University Commission Tracking](flows/07_university_commission_tracking_flow.md) | Needed so the Owner can track confidential commission revenue. |
| [Reporting and Dashboard](flows/08_reporting_and_dashboard_flow.md) | Needed for basic business visibility and management decisions. |
| [Access Control and Role Visibility](flows/10_access_control_and_role_visibility_flow.md) | Needed to protect business data and separate department responsibilities. |
| [Exception and File Closure Handling](flows/11_exception_and_file_closure_flow.md) | Needed to handle cancelled, on-hold, rejected, and completed files properly. |

### Phase 1 Success Criteria

- A real student file can move from counselling to completed status.
- Payments and dues are visible and accurate at each stage.
- Files cannot move forward without required payment confirmation.
- Owner can see the full business picture.
- Consultants cannot see each other's files.
- Commission data is visible only to the Owner.
- The agency can stop using manual notebooks or scattered spreadsheets for the main file lifecycle.

## Phase 2: Efficiency and Communication

### Goal

Improve the experience for staff and students by reducing repeated manual follow-up, making communication clearer, and adding useful business-facing enhancements.

By the end of Phase 2, the agency should spend less time answering routine status questions and preparing manual package materials.

### Business Expectations

- Students can receive clearer updates about payment, documents, offer letters, and visa outcomes.
- Consultants can follow up faster on pending documents and tasks.
- Important document expiry dates can be tracked.
- Package summaries can be converted into printable or shareable materials.
- The agency can use program/package information for marketing more easily.
- Referral or source tracking can help the agency understand where students come from.

### Flows To Complete Or Improve In Phase 2

| Flow | Phase 2 Expectation |
|---|---|
| [Notifications and Communication](flows/09_notifications_and_communication_flow.md) | Complete in-app notifications and add optional SMS/email communication if the business confirms it. |
| [Reporting and Dashboard](flows/08_reporting_and_dashboard_flow.md) | Improve dashboards with better operational follow-up, pending tasks, and performance views. |
| [Counselling and Program Selection](flows/02_counselling_and_program_selection_flow.md) | Improve package comparison and counselling support. |
| [Catalog and Package Setup](flows/01_catalog_and_package_setup_flow.md) | Support better package presentation, PDF quotation, and marketing-friendly summaries. |
| [Admission Processing](flows/05_admission_processing_flow.md) | Improve document expiry alerts and missing-document follow-up. |
| [Visa Processing](flows/06_visa_processing_flow.md) | Improve visa document tracking, expiry alerts, and outcome communication. |
| [File Opening](flows/03_file_opening_flow.md) | Add optional referral/source tracking if approved by the business. |

### Phase 2 Success Criteria

- Staff receive useful notifications for payment, document, and stage changes.
- Students can be informed about key milestones without every update being fully manual.
- Consultants can quickly identify their pending work.
- Package cost summaries can be printed or shared professionally.
- The agency can start using the system as a stronger counselling and marketing tool.

## Phase 3: Scale and Growth

### Goal

Prepare the software for larger business operations, more locations, more countries, and stronger analytics.

By the end of Phase 3, the system should support business expansion beyond the first operating model.

### Business Expectations

- The agency can support multiple countries beyond Malaysia.
- The agency can manage multiple office branches if the business expands.
- Owner can compare performance across branches, consultants, universities, countries, and time periods.
- Public-facing program/package information can help attract students before they visit the office.
- Students may get a more complete self-service experience.
- Management can use analytics to improve conversion, processing speed, and revenue.

### Flows To Complete Or Expand In Phase 3

| Flow | Phase 3 Expectation |
|---|---|
| [Catalog and Package Setup](flows/01_catalog_and_package_setup_flow.md) | Expand to stronger multi-country and multi-currency support. |
| [Counselling and Program Selection](flows/02_counselling_and_program_selection_flow.md) | Support broader program comparison across countries and universities. |
| [Reporting and Dashboard](flows/08_reporting_and_dashboard_flow.md) | Add advanced analytics, branch performance, conversion tracking, and processing-time insights. |
| [Access Control and Role Visibility](flows/10_access_control_and_role_visibility_flow.md) | Expand access rules for branches, country teams, and possible additional roles. |
| [Notifications and Communication](flows/09_notifications_and_communication_flow.md) | Expand communication into stronger student self-service and automated milestone updates. |
| [File Opening](flows/03_file_opening_flow.md) | Support branch, source, and expanded student lifecycle tracking. |
| [University Commission Tracking](flows/07_university_commission_tracking_flow.md) | Support more detailed commission reporting across countries, universities, and branches. |

### Phase 3 Success Criteria

- The business can expand beyond one country and one office without redesigning its operating process.
- Owner can understand growth, performance, revenue, and bottlenecks through analytics.
- Public program/package information can support marketing and student acquisition.
- Students can receive more direct visibility into their own journey if a student portal is approved.

## Flows By Phase

| Flow | Phase 1 | Phase 2 | Phase 3 |
|---|:---:|:---:|:---:|
| Catalog and Package Setup | Complete core | Improve package presentation | Expand for scale |
| Counselling and Program Selection | Complete core | Improve comparison and marketing support | Expand across countries |
| File Opening | Complete core | Add referral/source if approved | Expand branch/source tracking |
| Payment and Deposit Confirmation | Complete core | Minor improvements only | Minor improvements only |
| Admission Processing | Complete core | Improve document follow-up | Scale with country/branch needs |
| Visa Processing | Complete core | Improve alerts and communication | Scale with country-specific visa rules |
| University Commission Tracking | Complete core | Improve reporting if needed | Expand by country/branch/university |
| Reporting and Dashboard | Basic reports | Better operational dashboards | Advanced analytics |
| Notifications and Communication | Basic internal events if needed | Complete communication improvements | Student self-service and automation |
| Access Control and Role Visibility | Complete core | Minor improvements only | Expand for branches and new roles |
| Exception and File Closure Handling | Complete core | Minor improvements only | Scale with expanded operations |

## What Is Not Expected In Each Phase

### Not Expected In Phase 1

- Public program catalog page
- Student portal
- Full SMS/email automation
- Multi-branch support
- Advanced analytics
- Mobile app

### Not Expected In Phase 2

- Full multi-branch business management
- Advanced predictive analytics
- Full mobile app
- Complex country-by-country automation beyond agreed improvements

### Not Expected In Phase 3

Phase 3 is the growth phase, so its exact scope should be finalized after Phase 1 and Phase 2 are reviewed with real business users.
