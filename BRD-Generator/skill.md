---
name: BRD-generator
description: Use this whenever the user provides raw requirements, meeting notes, an existing BRD draft, ER diagram, functional documents, or any partial business inputs and wants a complete, professional Business Requirements Document (BRD).
argument-hint: "[module or process name]"
---
## Usage

Always analyze the full source material provided by the user (documents, notes, ERD, field lists, workflows, etc.) before drafting the BRD. Consolidate all inputs into a single source of truth.

Produce a comprehensive, well-structured, and highly detailed Business Requirements Document suitable for business stakeholders, project managers, solution architects, and development teams.

## Strict Guidelines

- Do not add any requirements, features, or details that are not explicitly mentioned or clearly implied in the user's provided source material.
- Stick to business-level language. Focus on **what** the system must do rather than **how** it will be technically implemented.
- Be extremely detailed — especially when describing data fields, workflows, approvals, business rules, and validations.
- Use tables extensively for clarity (field definitions, stakeholders, requirements, workflows, etc.).
- Maintain consistent formatting throughout the document.

## Core Sections to Include

1. **Header Section**
   - Document Title, Version, Author, Date, Reviewed By, Approved By, Purpose of the Document

2. **Executive Summary**
   - Business problem being solved
   - High-level solution approach
   - Expected business outcomes

3. **Business Objectives**
   - Present objectives in a table with Description and Success Criteria

4. **Problem Statement**
   - Current challenges and pain points
   - Impact if not resolved

5. **Scope Definition**
   - In Scope (list and describe all items)
   - Out of Scope (list all excluded items)

6. **Stakeholders**
   - Table with Role and Responsibilities

7. **Business Requirements**
   - Categorized or numbered requirements (use BR-01, BR-02 format where appropriate)

8. **Business Process Overview** (if applicable)
   - AS-IS Process (if provided)
   - TO-BE Process

9. **Data Requirements**
   - Core Tables / Entities (with purpose and relationships)
   - Detailed Field Definitions for each major table/entity:
     - Use a comprehensive table format including: Field Name, Label, Description, Type, Mandatory (Yes/Conditional/No), Default/Auto Value, Validation/Conditions, Remarks
   - Pay special attention to listing **every field** when source material provides table structures

10. **Validation Rules**
    - List all business and field-level validation rules

11. **Workflow / Approval Requirements**
    - Describe approval flows, decision points, roles involved, and task assignments
    - Include detailed tables for workflows, tasks, and responsible roles/groups

12. **Additional Business Rules**
    - Any specific rules, conditional logic, or constraints mentioned in the source

13. **Assumptions**
    - List any necessary assumptions (mark clearly)

14. **Version History**

## Output Instructions

- Generate a complete, professional BRD in clean markdown format.
- Ensure exhaustive coverage of all tables, fields, workflows, approvals, and business rules from the source material.
- Make field definitions highly detailed — do not summarize or skip any fields provided in the input.
- Use consistent, readable table formatting across all sections.
- Focus on making the document self-contained and ready for review by business and technical stakeholders.

Generate the BRD now based on the user's provided source materials.