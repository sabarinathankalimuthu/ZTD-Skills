# FRD Sections

Use this file as the section-by-section checklist when generating an FRD. Produce all sections in the final `.docx` even if some sections contain assumptions, dependencies, or `TBD` markers.

## 1. Header / Title Page

- Document title
- Project, module, or process name
- Customer or business unit
- Author or preparing team
- Reviewers or approvers if known
- Document date
- Version number
- Confidentiality note if applicable

## 2. Overview

- Problem statement or business need
- Objective of the solution
- Scope summary
- In-scope and out-of-scope notes when available

## 3. Functional Overview

- End-to-end capability summary
- Primary actors and their goals
- High-level process flow
- Key lifecycle states, decisions, or handoffs

## 4. System Architecture

- Major system components
- User channels such as portal, workspace, mobile, or email
- Platform components, custom apps, flows, integrations, and data stores
- Environment or deployment assumptions if relevant

For ServiceNow:
- Mention the application or module boundary
- Identify core platform components such as tables, flows, business rules, ACLs, notifications, portals, workspaces, and integrations

## 5. Functional Requirements

Capture each requirement with an identifier and outcome-focused statement.

Recommended columns:
- ID
- Requirement
- Actor
- Trigger
- Expected System Behavior
- Priority

## 6. Use Cases

Describe the main user interactions.

Recommended fields:
- Use Case ID
- Use Case Name
- Primary Actor
- Preconditions
- Main Flow
- Alternate Flow
- Postconditions

## 7. UI / UX Requirements

- Page, form, or screen expectations
- Layout or navigation needs
- Field behavior, validation, visibility, and mandatory rules
- Accessibility, responsiveness, and usability expectations

For ServiceNow:
- Mention workspace, service portal, catalog item, form, list, related list, or record producer behavior where relevant

## 8. Data Requirements

- Data entities
- Key fields
- Relationships
- Source of truth
- Retention, archival, or audit needs if known

Recommended table:
- Entity or Table
- Key Fields
- Description
- Source
- Notes

For ServiceNow:
- Include standard tables or custom tables where applicable

## 9. Business Rules

- Rule identifier
- Trigger condition
- Rule logic
- Outcome
- Exception handling if needed

For ServiceNow:
- Include assignment rules, approval logic, state transitions, SLA triggers, validation logic, notifications, and automation conditions when relevant

## 10. Integration Requirements

- External or internal systems involved
- Trigger direction and timing
- Data exchanged
- Authentication or connection expectations
- Error handling and retry expectations

Recommended table:
- Integration
- Direction
- Trigger
- Data Exchanged
- Protocol or Method
- Failure Handling

## 11. Security Requirements

- Roles and access model
- Sensitive data handling
- Segregation of duties if relevant
- Auditability and logging expectations

For ServiceNow:
- Mention roles, ACL expectations, impersonation restrictions, attachment handling, encryption, and least-privilege access where relevant

## 12. Non-Functional Requirements

- Performance
- Availability
- Reliability
- Maintainability
- Scalability
- Compliance
- Localization if relevant

## 13. Reporting Requirements

- Operational reports
- Dashboard or KPI expectations
- Audience
- Data source and refresh cadence

Recommended columns:
- Report Name
- Consumer
- Purpose
- Metrics
- Frequency

## 14. Testing Considerations

- Functional test themes
- Integration test themes
- Negative scenarios
- Security or role-based checks
- Performance or usability checks where needed

## 15. Traceability Matrix

Map business goals or source requirements to FRD requirements and test coverage.

Recommended columns:
- Source Requirement
- FRD Requirement ID
- Use Case ID
- Test Scenario
- Notes

## 16. Version History

Recommended columns:
- Version
- Date
- Author
- Summary of Changes

## ServiceNow Enrichment Checklist

When the request is ServiceNow-related, look for opportunities to add:

- Relevant standard or custom tables
- User roles and assignment groups
- Business rules and approval logic
- Flow Designer or automation behavior
- Notifications and SLA behavior
- Integrations with surrounding enterprise systems
- Security roles and ACL considerations
- Reporting and dashboard expectations
- Testing scenarios tied to personas and platform behavior
