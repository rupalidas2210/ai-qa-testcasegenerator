---
name : Generate Test Plan
Description : A skill that generates a comprehensive Test Plan from requirement.md ensuring complete test coverage and traceability
---

# Generate Test Plan
A skill that generates a comprehensive Test Plan from requirement.md ensuring complete test coverage and traceability.
The skill creates a detailed Test Plan that serves as the foundation for generating test cases, ensuring **no missing test scenarios** by enforcing traceability and coverage.

## Workflow: Requirement → Test Plan

### 1. Read the requirement file requirement.md
- Parse and understand all functional and non-functional requirements.
- Identify features, sub-features, business rules, validations, integrations, workflows, and acceptance criteria.
- Assign unique Requirement IDs where missing.

---
### 2. Generate a Comprehensive Test Plan (MANDATORY STEP)
Create a **Test Case Plan** using `requirement.md` to ensure complete coverage and traceability. 
The Test Plan must be detailed enough that QA can derive **all test cases with no missing scenarios**.

The Test Plan **must include the following sections**:

#### 2.1 Purpose and Quality Objectives
- Testing goals and success criteria.
- Definition of "complete test coverage" for this system.

#### 2.2 Scope
- In-scope features, modules, and integrations.
- Explicit out-of-scope items.
- Assumptions, constraints, and dependencies.

#### 2.3 Requirements Traceability Matrix (RTM)
- Map:
  - Requirement ID  
  - Acceptance Criteria  
  - Test Scenario IDs  
  - Test Case IDs (to be generated later)
- Every requirement must be mapped.
- No scenario may exist without a linked requirement.

#### 2.4 System Overview and Test Boundaries
- High-level architecture (UI, API, DB, services, integrations).
- Data flow and external dependencies.
- Real vs mocked components.

#### 2.5 Feature and Business Rule Breakdown
For each feature:
- Sub-features
- Business rules
- Field-level validations (format, length, range, mandatory/optional)
- State transitions and workflow rules

#### 2.6 Coverage Model (Applied to Every Feature)
Define and apply:
- Functional coverage: happy path, alternate paths, negative cases
- Data coverage: boundaries, equivalence classes, null/empty, invalid formats
- State/workflow coverage
- Role and permission coverage
- Platform/API version coverage
- Integration success and failure scenarios
- Non-functional coverage (performance, security, accessibility if applicable)

#### 2.7 Test Scenario Catalog
Create a **complete list of test scenarios before writing test cases**.
Each scenario must include:
- Scenario ID
- Description
- Preconditions
- Input/data variations
- Expected result
- Linked Requirement ID

Group scenarios by:
- Happy paths
- Alternate paths
- Validation and negative cases
- Authorization and permission checks
- Error handling and recovery
- Integration scenarios

#### 2.8 Test Data Strategy
- Required data sets (valid, invalid, edge cases).
- Test users, roles, and permissions.
- Data setup and cleanup approach.

#### 2.9 Test Environment and Configuration
- Test environments and configurations.
- Feature flags, stubs, mocks.
- Versioning assumptions.

#### 2.10 Entry and Exit Criteria
- Conditions required to start testing.
- Conditions required to declare testing complete:
  - 100% RTM coverage
  - All scenarios executed
  - Defect thresholds met

#### 2.11 Defect Management
- Severity and priority definitions.
- Retest and regression rules.
- Stop-ship criteria.

#### 2.12 Test Levels and Types
-Functional,Smoke, API, UI, integration, end-to-end, regression.
- Manual vs automated test scope.

#### 2.13 Risk-Based Testing
- High-risk areas identified from requirements.
- Mandatory tests per risk.

#### 2.14 Rule
✅ **This skill generates the Test Plan only. Test cases are generated separately using the "Generate Zephyr Test Case" skill.**


### 3. Test Plan File Creation Rules (File Naming)
- The system must create a Test Plan markdown file.
- **The Test Plan must be saved in the folder**: `.github\agents\Test Case Generator\agents-context\Test Case\TestPlan`
- If the folder doesn't exist, create it automatically.

#### Test Plan File Naming:
- Read the first line from `requirement.md`.
- Remove `#` symbols and extra spaces to extract the **Project Name**.
- Replace spaces with underscores.
- Format the file name as: `ProjectName_TestPlan.md`
- **Full path example**: `.github\agents\Test Case Generator\agents-context\Test Case\TestPlan\Spectrum_Brand_Manager_TestPlan.md`
- Example:
  - First line in requirement.md: `# Spectrum Brand Manager`
  - Extracted Project Name: `Spectrum Brand Manager`
  - File name: `Spectrum_Brand_Manager_TestPlan.md`
  - **Full file path**: `.github\agents\Test Case Generator\agents-context\Test Case\TestPlan\Spectrum_Brand_Manager_TestPlan.md`

#### Confirmation Response:
- After creation, respond with:
  ```
  ✅ Test Plan Created: ProjectName_TestPlan.md in .github\agents\Test Case Generator\agents-context\skills\Test Case\TestPlan
  
  Next Step: Use "Generate Zephyr Test Case" skill to generate Zephyr-ready test cases from this Test Plan.
  ```
