# ServiceNow ATF (Automated Test Framework) Guidelines

## Objective
Define a standard approach to design, create, and manage Automated Test Framework (ATF) test cases in ServiceNow to ensure complete validation of developed features and configurations.

The goal is to:
- Ensure **end-to-end validation**
- Cover **UI + backend logic**
- Maintain **consistency and reusability**
- Reduce dependency on scripting

---

## Prerequisite

Before creating ATF test cases, ensure:

- Required ATF system properties are enabled

---

## Test Design Approach

### 1. Test Case Identification

Before creating ATF:
- Analyze the **use case / requirement**
- if Story or Story number is perovide for creating the ATF , Analyze the Description and Acceptance criteria for the story and create the steps 
- Understand the **development/configuration changes**
- Identify all scenarios required and provide the summary of the Test steps to  **sign-off**
- After the sign-off create the ATF test using ServiceNow SDK

---

### 2. Test Case Coverage

You must define **all possible scenarios**, including:
Always create Positive and Negative Testcase for ATF and link it to a same Test Suite
#### Positive Test Cases
- Valid inputs
- Expected successful flows
- Standard user actions

#### Negative Test Cases
- Invalid inputs
- Missing mandatory fields
- Unauthorized access
- Failure scenarios

---

### 3. Test Case Documentation

Each test case should include:

- Test Name
- Description
- Pre-requisites
- Test Steps
- Expected Result
-Test Suiite 

---

## ATF Creation Guidelines

### 1. Use Native OOB Steps

- Always prefer **Out-of-the-Box (OOB) ATF steps**
- fill and map all the Attribute properly
- Avoid unnecessary scripting
- Use scripting **only when no OOB option exists**

**Examples of OOB Steps:**
- Open a Catalog Item
- Set Field Values
- Submit Form
- Validate Field Values
- Record Query
- Assert Values

---

### 2. Avoid Overuse of Scripts

- Do NOT implement full logic using scripts
- Scripts should be used only for:
  - Complex validations
  - Edge cases not supported by OOB steps

---

### 3. UI + Backend Validation

Each test must cover:

#### UI Validation
- Form behavior
- Field visibility
- Mandatory checks
- UI policies
- Client scripts

#### Backend Validation
- Record creation/update
- Business rules execution
- Workflow / Flow Designer execution
- Data integrity

---

### 4. End-to-End Scenario Coverage

- Always validate **complete business flow**
- Do not test isolated steps unless required
- Ensure real-world usage scenarios are covered

---

## Test Suite Strategy

### 1. Grouping Test Cases

- Create **Test Suites** for similar test cases
- Group based on:
  - Module
  - Feature
  - Use case

**Example:**
- Incident Management Suite
- Catalog Request Suite
- Non-Employee Management Suite

---

### 2. Reusability

- Reuse existing test steps where possible
- Avoid duplication of test logic

---

## Execution Guidelines

- Ensure test data is available before execution
- Validate execution results clearly
- Fix failing tests before sign-off

---

## Example ATF Approach

### Use Case: Catalog Form Submission

#### Identified Test Cases:

**Positive:**
- Submit form with all valid inputs
- Submit form with optional fields empty

**Negative:**
- Submit form with mandatory fields missing
- Submit form with invalid data
- Unauthorized user attempting submission

---

## Key Guidelines

- Always start with **test case identification**
- Cover **both positive and negative scenarios**
- Prefer **OOB steps over scripting**
- Validate **UI + backend**
- Use **test suites for organization**
- Ensure **end-to-end coverage**
- Tests must be **ready for sign-off validation**
- Test should have both the positive and Negative test and linke to 1 Test suite
- Fill all the attribute in the OOB Test Steps

---

## Usage

This document should be used as:
- A **standard ATF creation guideline**
- A **reference for AI-generated test cases**
- A **RAG knowledge base for automated testing**

---