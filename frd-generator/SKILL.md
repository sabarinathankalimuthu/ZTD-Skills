---
name: servicenow-frd-generator
description: Convert user input into a fully structured Functional Requirement Document (FRD) delivered as a Word (.docx) file. Use when Codex receives plain text requirements, rough notes, meeting notes, uploaded BRDs, or partial business requirements and needs to transform them into a professional FRD or functional requirement document with the standard 16 sections: title page, overview, functional overview, system architecture, functional requirements, use cases, UI/UX requirements, data requirements, business rules, integration requirements, security requirements, non-functional requirements, reporting requirements, testing considerations, traceability matrix, and version history. Apply this skill especially for ServiceNow work such as ITSM, HRSD, CSM, platform workflows, or module design where the FRD should include ServiceNow-specific tables, roles, business rules, integrations, and implementation assumptions where applicable.
---

# ServiceNow FRD Generator

## Overview

Turn incomplete requirement inputs into a polished FRD that is ready for stakeholder review. Preserve source facts, fill structural gaps with explicit assumptions or `TBD` markers, and produce the final deliverable as a `.docx` file rather than stopping at notes or markdown.

## Workflow

1. Identify the source material.
2. Normalize the requirements into a complete FRD structure.
3. Enrich the content with ServiceNow-specific detail when the domain warrants it.
4. Render the FRD as a Word document and verify the output before delivering it.

## Read The Input

- Accept plain text, bullet lists, pasted notes, user stories, BRDs, or mixed artifacts.
- Extract the business objective, actors, process scope, module or application name, constraints, and any named integrations.
- Distinguish confirmed facts from inferred material.
- If the input is sparse, make reasonable assumptions to keep momentum, but label them clearly in the document.
- Do not invent product capabilities that conflict with the provided source.

## Build The FRD

- Always produce all 16 standard sections.
- Read [references/frd-sections.md](references/frd-sections.md) before drafting the document body. Use it as the minimum content checklist for each section.
- Keep the writing implementation-ready. Prefer specific statements over vague business prose.
- Convert raw notes into structured requirements, use cases, rule statements, data definitions, and acceptance-oriented testing considerations.
- When the source does not provide enough detail for a section, add a concise assumption, dependency, open question, or `TBD` marker instead of leaving the section empty.
- Use tables where they improve clarity, especially for functional requirements, roles, data elements, integrations, reports, traceability, and version history.

## Apply ServiceNow Enrichment

- Use ServiceNow-specific content only when the request concerns ServiceNow or a workflow that clearly maps to it.
- Include likely tables such as `incident`, `task`, `sc_req_item`, `sc_task`, `sys_user`, `cmdb_ci`, or custom scoped tables only when relevant to the requested module.
- Describe personas in ServiceNow terms when appropriate, such as requester, fulfiller, agent, assignment group, approver, admin, integration user, and reporting consumer.
- Convert process logic into explicit business rules, flow logic, notifications, approvals, SLAs, data policies, and integration touchpoints when those are implied by the request.
- Mention integrations concretely: direction, trigger, payload theme, frequency, authentication style, failure handling, and reconciliation behavior.
- Call out platform constraints or assumptions when needed, such as scoped app boundaries, ACL expectations, workspace usage, portal experience, CMDB dependencies, or auditability requirements.
- Do not force ServiceNow vocabulary into a non-ServiceNow request.

## Create The Word Deliverable

- Produce the final artifact as a `.docx` file.
- If the Documents skill is available, use it to create or edit the Word document and visually verify the rendered output.
- Preserve clear heading hierarchy, readable tables, and consistent labels across all 16 sections.
- Name the output file to reflect the module or process, for example `Incident-Management-FRD.docx` or `Employee-Onboarding-FRD.docx`.
- Ensure the final document is review-ready, not just a content dump.

## Quality Bar

- Keep terminology consistent across sections.
- Ensure functional requirements map cleanly to use cases, business rules, integrations, testing considerations, and the traceability matrix.
- Make architecture, security, reporting, and non-functional sections specific to the solution rather than generic boilerplate.
- Surface assumptions explicitly so reviewers can resolve them quickly.
- Prefer concise, business-friendly language that still gives implementation teams enough specificity to build from the document.
