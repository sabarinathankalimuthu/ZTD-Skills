# User Story Conversion Guidelines (FRD → User Stories)

## Objective
Convert Functional Requirement Documents (FRD) or raw requirements into structured, actionable, and development-ready user stories.

Each user story must be:
- Clearly defined
- Independently workable
- Small enough to be completed within a sprint
- Contain all required implementation details

---

## User Story Structure

### 1. Number
- Format: `STORY-<SeriesNumber>`
- Example: `STORY-001`, `STORY-002`

---

### 2. Short Description
- Provide a **professional and simple summary**
- Should clearly represent the purpose of the story in one line

**Example:**
> Create Incident Submission Catalog Form

---

### 3. Description (Detailed Paragraph)
This section must include:

#### Purpose
- Clearly explain **why this story exists**
- Define the business or functional goal

#### Implementation Details
Include all necessary details required for development:

- **Entities to be created**
  - Example:
    - User Group: `Incident Management Team`
    - Role: `incident_user`

- **Application / Module Details**
  - Application Name: `<App Name>`
  - Scope: `<Scope>`
  - Modules: `<Module List>`

- **Catalog / Form Details (if applicable)**
  - Form Name: `<Form Name>`
  - Table: `<Table Name>`

- **Variables / Fields (Mandatory to list all)**
  - Variable Name
  - Type (Text, Dropdown, Checkbox, etc.)
  - Mandatory (Yes/No)
  - Conditions (if any)

**Example:**
- Short Description (Text, Mandatory)
- Description (Text Area, Mandatory)
- Priority (Dropdown: High, Medium, Low)
- Attachment (Attachment field)

- **UI Policies / Client Scripts (if required)**
  - Define visibility rules
  - Define mandatory conditions

- **Workflow / Flow Designer (if applicable)**
  - Approval flow
  - Notifications
  - Task creation

- **Dependencies**
  - Any prerequisite configurations
  - Existing tables, APIs, or integrations

---

### 4. Acceptance Criteria (HTML Format)

- Must be written in **HTML format**
- Each condition should be labeled sequentially:
  - `AC1`, `AC2`, `AC3`, etc.
- Include both:
  - ✅ Positive scenarios
  - ❌ Negative scenarios

---

### Acceptance Criteria Template

```html
<ul>
  <li><b>AC1:</b> System should allow user to submit the form with all mandatory fields filled.</li>
  <li><b>AC2:</b> System should prevent submission if mandatory fields are empty.</li>
  <li><b>AC3:</b> System should display validation message for missing fields.</li>
  <li><b>AC4:</b> System should trigger approval workflow upon submission.</li>
  <li><b>AC5:</b> System should restrict access to unauthorized users.</li>
</ul>