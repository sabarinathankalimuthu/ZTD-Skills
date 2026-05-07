# ServiceNow Development Workflow — Pre & Post Development Standards

## Objective
Define a **mandatory, repeatable workflow** for all ServiceNow development — covering Update Set setup, scope management, volatility checks, conflict resolution, and deployment approval.

> For module-specific rules (ACL, ATF, Flow Designer, etc.) → **Refer to the ServiceNow Best Practices RAG file named as (servicenow_development_best_practices) **

**Goals:**
- No development starts without an active, correctly named Update Set
- Every change is scoped, risk-checked, and approved before deployment
- Volatile or OOB records are never directly modified without user confirmation
- All decisions are documented and communicated to the user

## Step 1 — Update Set Setup (Mandatory Before Any Work)
> **No development or configuration change begins without an active Update Set.**

### Naming Convention
```
[ProjectCode/Feature] - [ShortDescription]
Examples:
  ITSM-001 - Incident Auto-Assignment Rule
  HR-Portal - Leave Request Workflow Fix
```
### Description Template
```
Purpose       : [What is being changed and why]
Related Req   : [Story / Ticket ID if applicable]
```
### AI Behavior
1. Ask if an Update Set already exists — if not, generate name + description from the templates above
2. Confirm the Update Set **Application** matches the intended development scope
3. All changes must be captured under this Update Set — no exceptions
---
## Step 2 — Application Scope
> Always develop in the correct scope. The Update Set Application must match the active development scope.

### Scope Decision Logic
| Situation | Scope |
|---|---|
| User specifies a custom app/scope | Use that exact scope |
| Modifying existing global config | Global |
| New feature, no scope mentioned | Global |
| User explicitly says "create new app" | New scope — only then |

### AI Behavior
- Ask the user once upfront: *does this belong to a specific application scope?*
- If no scope is mentioned → proceed in **Global**. Do not suggest creating a new one.

## Step 3 — Volatility Check (Mandatory Before Editing Any Existing Record)
> Before modifying any existing record, check its volatility level in `sys_metadata_volatility` using the record's `sys_id`.

### Decision Gate
```
IF record found in sys_metadata_volatility (Low / Medium / High):
  → Do NOT edit directly
  → Present Volatility Alert to user
  → Wait for user decision → proceed to Step 4
IF record NOT found:
  → Safe to proceed with modification
```
### Volatility Alert (Present to User)
```
⚠️ VOLATILITY ALERT
Record     : [Record Name]
Table      : [Table Name]
Volatility : [LOW / MEDIUM / HIGH]
This record carries a volatility risk.
→ Refer to Section 4 for resolution options before proceeding.
```
> For full volatility check API usage → **Refer to the RAG file.**

## Step 4 — Conflict Resolution
> Never directly edit a volatile record. Assess the conflict and present options to the user.

### Assess First
```
Does the existing record conflict with the new requirement?
  YES → Pattern B: Deactivate & Replace
  NO  → Pattern A: Extend (create alongside)
```

### Pattern A — Extend *(no conflict)*
- Create a new record that handles the new requirement independently
- Set conditions/order so both records coexist without conflict
- Leave the original completely untouched

### Pattern B — Deactivate & Replace *(conflict exists)*
- Create a new record with the correct configuration
- Set the original to `active = false` — **never delete**
- Capture both records in the Update Set
- Add a description to the new record: *"Replaces [original name]. Original deactivated [date] because [reason]."*

### Present to User Before Proceeding
```
Options:
  Option 1 — Extend (no conflict exists)
    New [record type] created alongside the original.
    Risk: None to existing behavior.
  Option 2 — Deactivate & Replace (conflict exists)
    New [record type] created; original deactivated (not deleted).
    Risk: Existing behavior replaced; original preserved but inactive.
Which option should I proceed with?
```
> For detailed pattern examples → **Refer to the RAG file.**

## Step 5 — Implementation Plan & Approval (Before Any Deployment)
> Generate the plan, present it to the user, and **wait for explicit approval**. No deployment without confirmation.

### Implementation Plan Template
```markdown

## Implementation Plan — [Feature / Task Name]

### Overview
[One paragraph: what is being built or changed and the business purpose]

### Scope
- Update Set     : [Name]
- Application    : [Global / App Name]
- Target Instance: [Dev / Test / UAT / Prod]

### Components
| # | Type | Name | Action | Table |
|---|---|---|---|---|
| 1 | [Business Rule / Script / Flow etc.] | [Name] | Create / Modify / Deactivate | [table] |

### Volatility Summary
| Record | Volatility | Action Taken |
|---|---|---|
| [Record Name] | Low / Medium / High | Extended / Replaced / Deactivated |

### Logic Summary
[Plain language: what triggers this, what it does, what the outcome is]

### Risks & Considerations
- [Dependencies on other configurations]
- [Records being deactivated and why]
- [Anything that could affect other parts of the instance]

### Rollback Plan
[Steps to reverse this deployment if needed]
✅ Please confirm: Approve this plan and proceed with deployment?
```
### AI Behavior
1. Fill **all sections** with real content — no empty placeholders
2. Present the plan clearly before taking any deployment action
3. After deployment, confirm which records were created/modified and that all changes are in the Update Set

## Step 6 — Development Field Standards
> Every record created or modified must have all necessary fields populated — no system defaults left without intent.

### Universal Fields (All Record Types)
| Field | Standard |
|---|---|
| **Name** | Clear, descriptive; follows naming convention |
| **Description** | Purpose-based statement — not ticket numbers or story references |
| **Active** | Set explicitly — never left at system default without intent |
| **Application** | Must match the active development scope |
| **Condition** | Narrowed to exact use case — avoid always-run/open-ended conditions |

> For module-specific field standards (Business Rules, Notifications, Script Includes, etc.) → **Refer to the RAG file.**

## Quick Reference Checklist

### Before Development
- [ ] Update Set created — correct name, description, and Application scope set
- [ ] Application scope confirmed — Global unless user specified otherwise

### Before Editing Any Existing Record
- [ ] Queried `sys_metadata_volatility` for the record's `sys_id`
- [ ] If volatile → alert shown, user confirmed resolution pattern before proceeding

### During Development
- [ ] All mandatory and recommended fields populated
- [ ] Description is purpose-based — not ticket/story references
- [ ] Conditions narrowed to exact use case; Order/Priority set explicitly
- [ ] Script header comment block included on every script

### Before Deployment
- [ ] Implementation Plan generated with all sections filled (no empty placeholders)
- [ ] Volatility checks documented in the plan
- [ ] Risks and rollback steps documented
- [ ] User has given explicit approval to deploy

### After Deployment
- [ ] Deployed records match the approved Implementation Plan
- [ ] All changes confirmed captured in the Update Set
- [ ] Deactivated records documented in the Update Set description

## Workflow at a Glance
| Step | Action | Gate |
|---|---|---|
| 1 | Create Update Set with correct name, description, scope | Mandatory — no work starts without it |
| 2 | Confirm Application Scope | Global unless user specifies otherwise 
| 3 | Volatility Check on any existing record | Mandatory — check `sys_metadata_volatility` first |
| 4 | Conflict Resolution | User chooses Pattern A or B — never decide alone |
| 5 | Implementation Plan + Approval | Present plan, wait for explicit user confirmation |
| 6 | Field Standards | All fields complete — description is purpose-based |
---
*This document governs the development workflow for all ServiceNow work. For module-specific best practices (ACL, ATF, Flow Designer, Script Include, Entitlement, Documentation) refer to the ServiceNow Best Practices RAG file.*

