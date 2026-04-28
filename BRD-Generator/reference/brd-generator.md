## Usage

IMPORTANT: _Always_ read the section reference before drafting content. Skipping it risks producing incomplete or inconsistent sections.

To identify the source material type before processing:
- Plain text / bullet notes → extract business objective, actors, scope, constraints, and integrations directly
- Uploaded BRD draft or document → read it fully, then normalize into BRD structure
- Mixed artifacts (ERDs, field lists, workflows, notes) → consolidate into a single source of truth before drafting

To produce the Word deliverable after drafting:
- Use the Documents skill (`docx`) to render and visually verify the `.docx` output
- Name the file to reflect the module, e.g. `Incident-Management-BRD.docx` or `Employee-Onboarding-BRD.docx`

## What to Include

- **14 standard sections** — header section, executive summary, business objectives, problem statement, scope definition, stakeholders, business requirements, business process overview, data requirements, validation rules, workflow/approval requirements, additional business rules, assumptions, version history
- **Data entities** — core tables/entities with purpose and relationships, and detailed field definitions including: Field Name, Label, Description, Type, Mandatory (Yes/Conditional/No), Default/Auto Value, Validation/Conditions, Remarks
- **Personas** — stakeholder roles and responsibilities mapped to each requirement area
- **Workflow specifics** — approval flows, decision points, roles involved, task assignments, and detailed tables for workflows, tasks, and responsible roles/groups
- **Business rules** — field-level validations, conditional logic, constraints, and numbered business rules (BR-01, BR-02 format)

## Prerequisite Knowledge and Guidelines

- Always analyze the full source material provided by the user (documents, notes, ERD, field lists, workflows, etc.) before drafting the BRD. Consolidate all inputs into a single source of truth.
- Do not add any requirements, features, or details that are not explicitly mentioned or clearly implied in the user's provided source material. Never silently invent capabilities.
- Use business-level language. Focus on **what** the system must do rather than **how** it will be technically implemented.
- Use tables extensively for clarity: field definitions, stakeholders, requirements, workflows, reports, and version history all benefit from tabular formatting.
- Write implementation-ready content. Be extremely detailed — especially when describing data fields, workflows, approvals, business rules, and validations — so business and technical stakeholders can review directly from the document.

## For Any Task — Always Start Here

- Start by reading the source input carefully: extract the business objective, actors, process scope, module name, constraints, and named integrations.
- Draft all 14 sections in order, filling gaps with explicit assumptions or `TBD` markers rather than omitting sections.
- Ensure exhaustive coverage of all tables, fields, workflows, approvals, and business rules from the source material. Make field definitions highly detailed — do not summarize or skip any fields provided in the input.
- Once content is complete, invoke the Documents (`docx`) skill to render the final `.docx` file and visually verify heading hierarchy, table formatting, and label consistency.
- Deliver the named `.docx` file as the final output — do not stop at markdown or notes.

## If a Section Cannot Be Completed

Do **not** leave a section empty or skip it. Instead:

- Add a concise **Assumption:** statement if a reasonable inference can be made
- Add an **Open Question:** marker if the gap requires stakeholder input
- Add `TBD` if the information is simply not yet available

Do **not** treat sparseness as a reason to abort — a well-structured BRD with clearly labelled gaps is more valuable to reviewers than an incomplete draft.