## Usage

IMPORTANT: _Always_ read the section reference before drafting content. Skipping it risks producing incomplete or inconsistent sections.

To check the minimum content checklist for all 16 FRD sections:
```bash
cat references/frd-sections.md
```

To identify the source material type before processing:
- Plain text / bullet notes → extract business objective, actors, scope, constraints, and integrations directly
- Uploaded BRD or document → read it fully, then normalize into FRD structure
- Mixed artifacts → consolidate into a single source truth before drafting

To produce the Word deliverable after drafting:
- Use the Documents skill (`docx`) to render and visually verify the `.docx` output
- Name the file to reflect the module, e.g. `Incident-Management-FRD.docx` or `Employee-Onboarding-FRD.docx`

## What to Include

- **16 standard sections** — title page, overview, functional overview, system architecture, functional requirements, use cases, UI/UX requirements, data requirements, business rules, integration requirements, security requirements, non-functional requirements, reporting requirements, testing considerations, traceability matrix, version history
- **ServiceNow tables** — `incident`, `task`, `sc_req_item`, `sc_task`, `sys_user`, `cmdb_ci`, or custom scoped tables (only when relevant to the requested module)
- **Personas** — requester, fulfiller, agent, assignment group, approver, admin, integration user, reporting consumer
- **Integration specifics** — direction, trigger, payload theme, frequency, authentication style, failure handling, reconciliation behavior
- **Platform constraints** — scoped app boundaries, ACL expectations, workspace usage, portal experience, CMDB dependencies, auditability

## Prerequisite Knowledge and Guidelines

- The first time this skill is invoked in a session, confirm whether the request is ServiceNow-specific or generic. Apply ServiceNow enrichment only when the domain clearly warrants it — do not force ServiceNow vocabulary into non-ServiceNow requests.
- Always distinguish confirmed facts from inferred material. Label assumptions explicitly using the word **Assumption:** or mark gaps as `TBD` — never silently invent capabilities.
- Use tables wherever they improve clarity: functional requirements, roles, data elements, integrations, reports, traceability matrix, and version history all benefit from tabular formatting.
- Write implementation-ready content. Prefer specific, actionable statements over vague business prose so development teams can build directly from the document.

## For Any Task — Always Start Here

- Start by reading the source input carefully: extract the business objective, actors, process scope, module name, constraints, and named integrations.
- Continue by reading `references/frd-sections.md` to confirm the minimum content bar for each of the 16 sections before drafting anything.
- Draft all 16 sections in order, filling gaps with explicit assumptions or `TBD` markers rather than omitting sections.
- Once content is complete, invoke the Documents (`docx`) skill to render the final `.docx` file and visually verify heading hierarchy, table formatting, and label consistency.
- Deliver the named `.docx` file as the final output — do not stop at markdown or notes.

## If a Section Cannot Be Completed

Do **not** leave a section empty or skip it. Instead:

- Add a concise **Assumption:** statement if a reasonable inference can be made
- Add an **Open Question:** marker if the gap requires stakeholder input
- Add `TBD` if the information is simply not yet available

Do **not** treat sparseness as a reason to abort — a well-structured FRD with clearly labelled gaps is more valuable to reviewers than an incomplete draft.