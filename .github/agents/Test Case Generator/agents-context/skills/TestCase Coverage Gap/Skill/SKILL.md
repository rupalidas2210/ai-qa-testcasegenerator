---
name : TestCase Coverage Gap
Description : A skill that compares requirement.md (and/or the generated Test Plan) vs Zephyr CSV test cases to find missing coverage, orphan tests, and weak coverage areas. Produces a gap report + optional delta CSV.
---

# TestCase Coverage Gap

## Goal
Given `requirement.md` and a Zephyr Scale-ready test case CSV, identify:
- Missing requirements / missing scenarios (gaps)
- Orphan test cases (not traceable to any requirement)
- Weak coverage (e.g., validations without Negative/Edge coverage)

## Inputs
1. `requirement.md` in workspace root (MANDATORY)
2. Zephyr CSV test cases file (MANDATORY)
   - Prefer newest file under:
     `.github/agents/Test Case Generator/agents-context/ZephyrReadyTestCases/`
   - Or user-provided CSV path.

## Optional Input (Preferred if exists)
- Generated Test Plan:
  `.github/agents/Test Case Generator/agents-context/TestPlan/<ProjectName>_TestPlan.md`
  If present, use it to read:
  - RTM table (REQ -> TS list)
  - Test Scenario Catalog (TS rows with desc/expected result)

## Workflow

### Step 1: Load Requirements Model and Determine Test Plan Location
1. Parse `requirement.md`.
2. **Determine Test Plan File Name** (Follow Generate Test Plan naming convention):
   - Read the first line from `requirement.md`
   - Remove `#` symbols and extra spaces to extract the **Project Name**
   - Replace spaces with underscores
   - Format the file name as: `ProjectName_TestPlan.md`
   - Full path: `.github/agents/Test Case Generator/agents-context/TestPlan/ProjectName_TestPlan.md`
   - Example:
     - First line: `# Spectrum Brand Manager`
     - File name: `Spectrum_Brand_Manager_TestPlan.md`
     - Full path: `.github/agents/Test Case Generator/agents-context/TestPlan/Spectrum_Brand_Manager_TestPlan.md`

3. **Check if Test Plan exists**:
   - If Test Plan file exists, parse RTM:
     - Req ID
     - Acceptance Criteria
     - Test Scenario IDs (TS-xxx)
   - If Test Plan file does NOT exist:
     - **CREATE the Test Plan first** using "Generate Test Plan" skill
     - Wait for Test Plan creation to complete
     - Then parse the newly created Test Plan for RTM and Test Scenario Catalog
   
4. If RTM is incomplete or missing in Test Plan:
   - Create Requirement IDs (REQ-001...) and derive scenarios:
   - Split acceptance criteria/business rules into atomic test scenarios
   - Assign TS IDs (TS-001...)

### Step 2: Load & Normalize Zephyr CSV
1. Read the Zephyr CSV.
2. Group rows into test cases:
   - A new test case starts when the `Name` column is non-empty.
   - Step 2+ rows have empty metadata columns and only `Test Step` populated.
3. For each test case, build a searchable text blob:
   - Name + Objective + Pre-condition + Steps + Test Result + Components + Sub Domain + Requirement ID + Labels

### Step 3: Extract Traceability Tags (Deterministic Mapping)
Preferred mapping method (highest accuracy):
- From `Requirement ID` column, detect tags like:
  - `REQ-###`
  - `TS-###`

Rules:
- Requirement ID column can contain multiple values, comma-separated with NO spaces.
- Example: `REQ-009,TS-010`

### Step 4: Fallback Mapping (If tags are missing)
If no REQ/TS tags exist:
- Match using:
  1) Exact error/expected-message matches from acceptance criteria / expected results
  2) Keyword overlap (facility ID, lockout, scanner pairing, etc.)
  3) Semantic similarity (scenario description vs test case text)
- Produce a confidence score (High/Med/Low) for each mapping.

### Step 5: Compute Gaps
1. Missing Requirements:
   - REQ with zero mapped test cases
2. Missing Scenarios:
   - TS with zero mapped test cases
3. Orphan Tests:
   - Test cases with no mapped REQ (confidence too low or no tags)
4. Weak Coverage:
   - For validation-heavy REQs, ensure at least one Negative or Edge exists
   - For critical flows, ensure at least one Smoke or E2E exists

### Step 6: Output Artifacts
Create folder:
`.github/agents/Test Case Generator/agents-context/GapAnalysis/`

Write:
1. `<ProjectName>_GapReport.md`
   Must include:
   - Summary counts (REQ total/covered/missing, TS total/covered/missing, orphan tests)
   - Missing REQ list with acceptance criteria
   - Missing TS list with expected result
   - Orphan tests list
   - Weak coverage list (REQ -> recommended test types)

2.  `<ProjectName>_MissingTests.csv`
   - Generate only missing tests as Zephyr-ready rows
   - Follow the same CSV formatting rules as the main generator.

## Error Handling
- If `requirement.md` missing → stop and ask user to provide it.
- If CSV missing → stop and ask user to provide it.
- If mapping confidence is Low (no tags + poor text match) → report as "Needs review" and recommend adding REQ/TS tags in Requirement ID column for deterministic traceability.

## Response Format
- Confirm:
  - Gap report created (full path)
  - Missing test cases CSV created (if generated)
- Print top 5 most critical gaps (REQ/TS) in the chat response.