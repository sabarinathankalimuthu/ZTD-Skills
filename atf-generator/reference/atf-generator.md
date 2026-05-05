# ServiceNow ATF (Automated Test Framework) Guidelines

## Objective

Define a **standard, consistent approach** to design, create, and manage Automated Test Framework (ATF) test cases in ServiceNow — written to the standard of a **professional QA tester**.

**Goals:**
- Think like a tester: **break the system, not just confirm the happy path**
- Create **every meaningful test case** — positive, negative, boundary, role-based, and edge cases
- **Challenge the developer's implementation** at every step
- Ensure **end-to-end validation** covering UI behavior and backend data integrity
- Configure every OOB step with **all attributes fully mapped**
- Maintain **reusability, consistency, and zero duplication**
- Keep all test cases **organized in a Test Suite** per feature or module

---

## Prerequisite

Before creating any ATF test case, confirm:

- Required ATF system properties are enabled in ServiceNow
- Test data is prepared and available in the target environment
- The feature under test has been developed and deployed to the test environment
- Provide a summary of the Test Steps in Approver Plan Mode.
- Sign-off on the test scenario list has been obtained before ATF creation begins
- Once the step is approved use ServiceNow SDK to create the ATF in the instance

---

## How Many Test Cases to Create

- **Create every test case that is meaningful, possible, and would catch a real defect. Think like a professional tester — if a scenario can fail, it must be tested.**

There is no minimum or maximum. The right number depends entirely on the complexity of the feature. A simple field change may need 3–4 tests. A catalog item with role-based access, mandatory fields, UI policies, and a workflow may need 10–15 or more.

**Every test case must have a clear, distinct purpose.** Do not create duplicates. Do not skip scenarios because they seem unlikely — edge cases are where defects hide.

The minimum set for any feature includes:
- At least one **Positive** test case (valid submission, happy path)
- At least one **Negative** test case (invalid data, mandatory field missing)
- Additional cases for each **distinct condition, role, state, or rule** that warrants independent validation
- Make sure that all the **ATF test crested are mapped to the Proper Test Suite**.
- Arrange test steps in the correct sequence.

---

## Phase 1 — Test Case Identification (Before Creation)

### Step 1: Analyze the Story or Requirement

If a Story or Story number is provided:
- Read the **Description** and **Acceptance Criteria** in full
- Extract every condition, business rule, and validation stated or implied
- Identify all **fields, roles, states, transitions, and integrations** involved
- Map out all possible user journeys through the feature


### Step 2: Challenge the Development

Before accepting any implementation, validate every item below. This is **not optional** — mark each as verified or explicitly not applicable.

**Developer Challenge Checklist:**

- [ ] Does every mandatory field enforce a hard stop on form submission?
- [ ] Are UI policies applying and hiding fields correctly for each condition?
- [ ] Do client scripts trigger on the correct events — onChange, onLoad, onSubmit?
- [ ] Are business rules firing in the correct order, scope, and timing (before/after, insert/update/delete)?
- [ ] Does the workflow or Flow Designer complete end-to-end without gaps or missing transitions?
- [ ] Are role-based access restrictions enforced — authorized user can access, unauthorized user is blocked?
- [ ] Is data written to the correct table and fields with exactly the right values?
- [ ] Are boundary values handled — empty optional fields, maximum-length input, special characters?
- [ ] Are error messages specific, accurate, and visible to the user?
- [ ] Does the form behave correctly after submission — correct redirect, state reset, or confirmation?
- [ ] Are catalog variables mapped correctly to record fields if a catalog item is involved?
- [ ] Are related records (tasks, approvals, child records) created where expected?
- [ ] Is the correct notification or email triggered if applicable?
- [ ] Does re-submission or duplicate submission behave correctly?

Any gap found must be raised with the developer **before** ATF creation proceeds.

### Step 3: Define All Test Scenarios

Identify and document every scenario before writing a single test step. Group by type:

#### Positive Scenarios
- Submit with all mandatory and optional fields filled with valid data
- Submit with only mandatory fields filled (optional fields blank)
- Submit as each authorized role or user group
- Verify correct field visibility and UI policy behavior on form load
- Verify dependent fields populate or hide correctly when a trigger field changes
- Verify successful record creation with correct field values in the backend
- Verify workflow or flow executes correctly after submission
- Verify related records are created where expected
- Verify the correct confirmation message, redirect, or email is triggered

#### Negative Scenarios
- Submit with each mandatory field blank — test individually where behavior differs per field
- Submit with invalid data format in key fields (wrong date format, string in number field, etc.)
- Submit with a value exceeding the maximum allowed length
- Attempt submission as an unauthorized role — verify access is blocked
- Verify no record is created in the backend when submission is blocked
- Verify error messages are accurate and user-facing
- Verify form state is preserved after a failed submission (fields not cleared unexpectedly)
- Attempt to bypass a UI policy or mandatory check where applicable

#### Boundary & Edge Case Scenarios
- Submit with the minimum accepted value for a field
- Submit with special characters, numeric strings, or unusually long text in free-text fields
- Re-submit the same record to check duplicate prevention logic
- Submit in an unexpected order of steps if workflow state-gating applies

#### Role-Based & Access Scenarios
- Authorized role can view, fill, and submit the form
- Unauthorized role cannot access the catalog item or form
- Read-only role can view but cannot edit or submit
- Admin override behavior if applicable

### Step 4: Sign-Off on Scenario List

Present the complete scenario list to the story owner or QA lead for **sign-off before any ATF test cases are created**. No test creation begins without this approval.

---

## Phase 2 — Test Case Documentation Standard

Every individual test case must be documented with all of the following before being built in ServiceNow:

| Field | Requirement |
|---|---|
| **Test Name** | Format: `[Feature Name] — [Scenario]` e.g. `VPN Catalog — Submit with valid inputs` |
| **Short Description** | One sentence: what this test validates |
| **Description** | Full scenario description — what is being tested and why |
| **Pre-requisites** | Specific test data, roles, and environment state required |
| **Test Suite** | Linked to the shared Test Suite for this feature or module |
| **Steps** | Ordered OOB steps with every attribute explicitly set |
| **Expected Result** | Clear, specific, measurable outcome for each step and the final result |

---

## Phase 3 — ATF Step Configuration Rules

### Rule 1: Always Use OOB Steps — Every Attribute Must Be Filled

Always use **Out-of-the-Box (OOB) ATF steps**. When configuring any OOB step, **every available attribute must be explicitly set**. Never leave a field at its default without deliberate intention. Unmapped attributes are a primary cause of false test failures.Instead of just check the values by using Recod qurey , check it's functionality.

---

### OOB Step Attribute Reference

#### Open a Record
| Attribute | Requirement |
|---|---|
| Table | Set explicitly — never blank |
| Record | Provide sys_id or a precise filter query |
| View | Set explicitly: default, ess, mobile, or the specific named view |

#### Open a Catalog Item
| Attribute | Requirement |
|---|---|
| Catalog Item | Exact catalog item name or sys_id |
| View | Set explicitly |

#### Set Field Value
| Attribute | Requirement |
|---|---|
| Table | Set explicitly |
| Field | Internal field name — not the display label |
| Value | For reference fields use sys_id; for choice fields use the exact choice value |
| Trigger onChange | Set explicitly — true if a client script or UI policy depends on this field |

#### Submit Form
| Attribute | Requirement |
|---|---|
| Table | Set explicitly |
| Expected Behavior | Define the expected post-submit state: redirect URL, confirmation message, or form state |

#### Validate Field Value (UI)
| Attribute | Requirement |
|---|---|
| Table | Set explicitly |
| Field | Exact internal field name |
| Operator | is / is not / contains / starts with / is empty / is not empty |
| Expected Value | Define the exact expected value — never vague or assumed |

#### Record Query (Backend Assertion)
| Attribute | Requirement |
|---|---|
| Table | Set explicitly |
| Conditions | All filter conditions explicitly defined: table + field + operator + value |
| Expected Record Count | Exact count — 1 for a created record, 0 for a blocked or negative scenario |
| Fail test if no records found | Set to true for all positive assertion queries |

#### Assert Field Value (Backend)
| Attribute | Requirement |
|---|---|
| Table | Set explicitly |
| Record | Reference the record from a prior step — use output variable or sys_id |
| Field | Exact internal field name |
| Operator | Set explicitly |
| Expected Value | Exact stored value — not display value unless testing a display field |

#### Impersonate User
| Attribute | Requirement |
|---|---|
| User | sys_id or exact username of the test user |
| Role Validation | Confirm the impersonated user has only the intended roles for this scenario |

#### Run Server-Side Script
| Attribute | Requirement |
|---|---|
| Script | Minimal, single-purpose logic only |
| Inline comment | Required — must explain why no OOB step was sufficient |
| Output variable | Always define and assert the output in a subsequent validation step |

---

### Rule 2: Scripting Policy

Scripts are **only permitted** when:
- No OOB step exists for the required action or validation
- Complex multi-condition logic cannot be expressed via OOB steps

Scripts must:
- Be minimal and single-purpose
- Include an inline comment explaining why OOB was insufficient
- Always produce an assertable output variable verified in the next step

**Never** use scripts to replicate what an OOB step already handles.

---

### Rule 3: UI Validation — Required in Every Test Case

Validate all applicable UI behaviors for the scenario under test:

- [ ] Correct fields are visible or hidden based on conditions
- [ ] Mandatory fields are enforced — form blocks submission when blank
- [ ] Read-only fields cannot be edited
- [ ] UI policies trigger correctly on field change and on form load
- [ ] Client scripts execute on the correct event
- [ ] Correct error or info messages appear when expected
- [ ] Field values display correctly — format, label, reference lookup

---

### Rule 4: Backend Validation — Required in Every Test Case

Validate all applicable backend behaviors for the scenario under test:

- [ ] Record is created or updated in the correct table with correct field values
- [ ] No record is created when submission is blocked (negative tests)
- [ ] Business rules executed in the expected scope and order
- [ ] Workflow or Flow Designer reached the expected state or completion
- [ ] Related records (tasks, approvals, child records) created where expected
- [ ] No orphaned, duplicate, or unintended records after execution
- [ ] Correct notification or email generated if applicable

---

## Phase 4 — Test Suite Organization

All test cases for a feature or module are grouped into **one Test Suite**.

| Field | Requirement |
|---|---|
| **Suite Name** | `[Module/Feature Name] — Test Suite` |
| **Description** | Brief description of what the suite validates |
| **Test Cases** | All positive, negative, boundary, and role-based cases for this feature |
| **Execution Order** | Positive cases first, then negative, then boundary and role-based |

**Example Suite Names:**
- `Incident Management — Test Suite`
- `VPN Access Catalog Item — Test Suite`
- `Non-Employee Onboarding — Test Suite`
- `Change Request Approval Flow — Test Suite`

---

## Phase 5 — Test Case Templates

Use these templates when documenting and building each test case in ServiceNow.

---

### Positive Test Case Template

**Test Name:** `[Feature Name] — Submit with all valid inputs`

**Short Description:**
Validates that a record is created correctly with all expected field values and workflow execution when all inputs are valid.

**Pre-requisites:**
- Test user with role: [Role]
- Catalog item or form: [Name] exists in the environment
- [Any required test data — records, users, groups, reference data]

**Steps:**

| # | OOB Step | Table | Attributes | Expected Result |
|---|---|---|---|---|
| 1 | Open Catalog Item | — | Item: [Name], View: [View] | Form opens correctly |
| 2 | Set Field Value | [Table] | Field: [field_name], Value: [value], Trigger onChange: true | Field set correctly |
| 3 | Set Field Value | [Table] | Field: [field_name], Value: [value], Trigger onChange: true | Dependent behavior triggered |
| 4 | Validate Field Value | [Table] | Field: [field_name], Operator: is, Expected: [value] | UI displays correct value |
| 5 | Submit Form | [Table] | Expected: [confirmation/redirect] | Submission successful |
| 6 | Record Query | [Table] | Conditions: [field=value], Count: 1, Fail if not found: true | Record created in DB |
| 7 | Assert Field Value | [Table] | Record: [var], Field: [field_name], Operator: is, Expected: [value] | Correct value stored |
| 8 | Assert Field Value | [Table] | Record: [var], Field: state, Operator: is, Expected: [expected_state] | Correct state set |
| 9 | Record Query | [Flow/Workflow Table] | Conditions: [parent=record, state=complete], Count: 1 | Flow completed |

**Expected Final Result:**
Record created with all correct field values. Workflow or flow triggered and completed. Correct confirmation shown to user.

**Test Suite:** `[Module] — Test Suite`

---

### Negative Test Case Template — Mandatory Field Blank

**Test Name:** `[Feature Name] — Submit with [Field Name] blank`

**Short Description:**
Validates that form submission is blocked and no record is created when [Field Name] is left empty.

**Pre-requisites:**
- Test user with role: [Role]
- [Any required test data]

**Steps:**

| # | OOB Step | Table | Attributes | Expected Result |
|---|---|---|---|---|
| 1 | Open Catalog Item | — | Item: [Name], View: [View] | Form opens |
| 2 | Set Field Value | [Table] | Field: [other_field], Value: [value], Trigger onChange: false | Other fields populated |
| 3 | Leave mandatory field blank | — | Field: [mandatory_field] — intentionally not set | Field remains empty |
| 4 | Submit Form | [Table] | Expected: blocked | Submission blocked |
| 5 | Validate Field Value | [Table] | Field: [error_field], Operator: contains, Expected: [error text] | Error message visible |
| 6 | Record Query | [Table] | Conditions: [field=value], Count: 0, Fail if not found: false | No record created |

**Expected Final Result:**
Submission blocked by mandatory field validation. Correct error message visible. No record created in the database.

**Test Suite:** `[Module] — Test Suite`

---

### Negative Test Case Template — Invalid Data

**Test Name:** `[Feature Name] — Submit with invalid value in [Field Name]`

**Short Description:**
Validates that form submission is blocked and an appropriate error is shown when [Field Name] contains invalid data.

**Steps:**

| # | OOB Step | Table | Attributes | Expected Result |
|---|---|---|---|---|
| 1 | Open Catalog Item | — | Item: [Name], View: [View] | Form opens |
| 2 | Set Field Value | [Table] | Field: [field_name], Value: [invalid_value], Trigger onChange: true | Invalid value entered |
| 3 | Submit Form | [Table] | Expected: blocked | Submission blocked |
| 4 | Validate Field Value | [Table] | Field: [error_field], Operator: contains, Expected: [error text] | Correct error shown |
| 5 | Record Query | [Table] | Conditions: [field=invalid_value], Count: 0 | No record created |

**Expected Final Result:**
Submission blocked. Correct error message displayed. No record written to the database.

**Test Suite:** `[Module] — Test Suite`

---

### Role-Based Test Case Template — Authorized Access

**Test Name:** `[Feature Name] — Authorized role can submit`

**Short Description:**
Validates that a user with the required role can access and successfully submit [Feature Name].

**Steps:**

| # | OOB Step | Table | Attributes | Expected Result |
|---|---|---|---|---|
| 1 | Impersonate User | — | User: [authorized_test_user] | Impersonation active |
| 2 | Open Catalog Item | — | Item: [Name], View: [View] | Form accessible |
| 3 | Set Field Value | [Table] | Field: [field_name], Value: [value], Trigger onChange: true | Field set |
| 4 | Submit Form | [Table] | Expected: [confirmation] | Submission successful |
| 5 | Record Query | [Table] | Conditions: [submitted_by=user], Count: 1 | Record created |

**Expected Final Result:**
Authorized user can access the form and submit successfully. Record created correctly.

**Test Suite:** `[Module] — Test Suite`

---

### Role-Based Test Case Template — Unauthorized Access Blocked

**Test Name:** `[Feature Name] — Unauthorized role cannot access`

**Short Description:**
Validates that a user without the required role cannot access or submit [Feature Name].

**Steps:**

| # | OOB Step | Table | Attributes | Expected Result |
|---|---|---|---|---|
| 1 | Impersonate User | — | User: [unauthorized_test_user] | Impersonation active |
| 2 | Open Catalog Item | — | Item: [Name], View: [View] | Access denied or item not visible |
| 3 | Record Query | [Table] | Conditions: [submitted_by=unauthorized_user], Count: 0 | No record created |

**Expected Final Result:**
Unauthorized user cannot access or submit the form. No record created.

**Test Suite:** `[Module] — Test Suite`

---

### Boundary Test Case Template

**Test Name:** `[Feature Name] — [Field Name] at [minimum/maximum] boundary`

**Short Description:**
Validates system behavior when [Field Name] is set to its [minimum/maximum] accepted value.

**Steps:**

| # | OOB Step | Table | Attributes | Expected Result |
|---|---|---|---|---|
| 1 | Open Catalog Item | — | Item: [Name], View: [View] | Form opens |
| 2 | Set Field Value | [Table] | Field: [field_name], Value: [boundary_value], Trigger onChange: true | Value set |
| 3 | Submit Form | [Table] | Expected: [accepted or blocked per rule] | Behavior matches business rule |
| 4 | Record Query | [Table] | Conditions: [field=boundary_value], Count: [0 or 1] | Record state correct |
| 5 | Assert Field Value | [Table] | Record: [var], Field: [field_name], Operator: is, Expected: [boundary_value] | Value stored correctly |

**Expected Final Result:**
System handles boundary value according to the business rule without unexpected behavior or error.

**Test Suite:** `[Module] — Test Suite`

---

## Phase 6 — Execution & Sign-Off

### Pre-Execution Checklist

- [ ] All test data is available in the target environment
- [ ] Every test case is linked to the correct Test Suite
- [ ] All OOB step attributes are fully configured — no unintentional defaults
- [ ] Developer challenge checklist from Phase 1 is complete
- [ ] Scenario list sign-off was obtained before ATF creation

### Execution

1. Run the full Test Suite — all test cases execute in order
2. Review each step result individually — do not mark a test passed until every step is confirmed
3. Capture screenshots and execution logs for any failure
4. Raise failures to the developer with step-level detail: step number, expected result, actual result
5. Re-execute only after the developer confirms the fix is deployed

### Sign-Off Criteria

- All test cases pass with zero failures
- No steps skipped or marked as acceptable failures
- UI and backend validations confirmed for all cases
- Test Suite execution log attached to the story before closure

---

## Non-Negotiable Rules Summary

| Rule | Requirement |
|---|---|
| Test case count | Create every meaningful test case — professional coverage, no arbitrary limit |
| Test case types | Must include positive, negative, boundary, and role-based cases as applicable |
| Test Suite | All test cases for a feature linked to one Test Suite |
| OOB preference | Always use OOB steps; script only when no OOB option exists |
| Field mapping | Every attribute in every OOB step must be explicitly configured |
| UI validation | Required in every test case |
| Backend validation | Required in every test case |
| Developer challenge | Checklist must be completed before ATF creation starts |
| Sign-off | Scenario sign-off before creation; execution sign-off before story closure |
| Test naming | Consistent format: `[Feature] — [Scenario]` |

---

## OOB Step Quick Reference

| OOB Step | Mandatory Attributes |
|---|---|
| Open a Record | Table, Record (sys_id or query), View |
| Open a Catalog Item | Catalog Item name or sys_id, View |
| Set Field Value | Table, Field (internal name), Value, Trigger onChange |
| Submit Form | Table, Expected post-submit behavior |
| Validate Field Value | Table, Field, Operator, Expected Value |
| Record Query | Table, Conditions, Expected Count, Fail if not found |
| Assert Field Value | Table, Record reference, Field, Operator, Expected Value |
| Impersonate User | User sys_id or username |
| Run Server-Side Script | Script with justification comment, Output variable |

---

*This document is the authoritative ATF standard for this ServiceNow instance. Every test case must conform to this guideline. Deviations require explicit justification and sign-off from the QA lead.*
 