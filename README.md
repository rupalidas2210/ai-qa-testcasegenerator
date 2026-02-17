# ai-qa-testcasegenerator

This repository generates comprehensive test plans and Zephyr-ready test cases for QA testing.

## Quick Start

1. **Create requirements**: Add your requirements to `requirement.md` (see location below)
2. **Run agent**: Use GitHub Copilot agent "Test Case Generator" and say "Start test generation"
3. **Get outputs**: Receive 3 files automatically:
   - Test Plan (comprehensive test scenarios and RTM)
   - Zephyr CSV (import-ready test cases)
   - Gap Report (coverage analysis)

## Features

✅ **Automated Test Plan Generation**: Creates detailed test plans with RTM, coverage models, and test scenarios  
✅ **Zephyr CSV Export**: Generates test cases in Zephyr Scale import-ready CSV format  
✅ **Coverage Gap Analysis**: Automatically identifies missing requirements, orphan tests, and weak coverage areas  
✅ **Template Enforcement**: Strict validation ensures 100% Zephyr format compliance  
✅ **Multi-Type Coverage**: Functional, Regression, Smoke, E2E, Integration, Negative, and Edge test cases  
✅ **100% Traceability**: Complete requirements-to-test-cases mapping with gap detection  
  


### Generate Test Cases

The generator follows a **3-step sequential workflow**:

1. **Step 1: Generate Test Plan** - Analyzes requirements and creates comprehensive test plan
2. **Step 2: Generate Zephyr Test Cases** - Creates test cases from the test plan
3. **Step 3: Coverage Gap Analysis** - Validates completeness and identifies any gaps

#### Usage

1. Place requirements in: `.github/agents/Test Case Generator/agents-context/skills/Test Case/Requirement/requirement.md`
2. Run the test case generator (via GitHub Copilot agent or CLI)
3. Output files automatically created:
   - **Test Plan**: `.github/agents/Test Case Generator/agents-context/TestPlan/[ProjectName]_TestPlan.md`
   - **Zephyr CSV**: `.github/agents/Test Case Generator/agents-context/ZephyrReadyTestCases/[ProjectName]_Zephyrimportready.csv`
   - **Gap Report**: `.github/agents/Test Case Generator/agents-context/GapAnalysis/[ProjectName]_GapReport.md`
   - **Missing Tests CSV** (if gaps found): `.github/agents/Test Case Generator/agents-context/GapAnalysis/[ProjectName]_MissingTests.csv`


## Zephyr Template Enforcement

All generated CSV files **must** match the `ZephyrTestCaseTemplate.csv` format with exactly **16 columns**:

1. Name
2. Objective
3. Pre-condition
4. Test Step
5. Test Data
6. Test Result
7. Labels
8. Components
9. QA Engineer
10. Fix versions
11. Affect versions
12. Automated
13. API
14. Jira
15. Sub Domain
16. Requirement ID

⚠️ **No extra columns allowed** (Priority, Owner, Status, etc. are forbidden)


## Coverage Gap Analysis

The generator automatically performs comprehensive gap analysis to ensure 100% requirements coverage:

### What It Analyzes
- ✅ **Missing Requirements**: Requirements with zero test case coverage
- ✅ **Missing Scenarios**: Test scenarios without corresponding test cases
- ✅ **Orphan Tests**: Test cases not traceable to any requirement
- ✅ **Weak Coverage**: Requirements lacking specific test types (Negative/Edge/Integration)
- ✅ **Test Distribution**: Validates test type percentages match targets

### Gap Report Contents
- Requirements coverage matrix with test case counts
- Test scenario coverage details
- Test type distribution analysis
- Orphan test identification
- Coverage strength assessment
- Actionable recommendations

### Outputs
- **Gap Report** (`[ProjectName]_GapReport.md`): Detailed analysis with metrics and recommendations
- **Missing Tests CSV** (`[ProjectName]_MissingTests.csv`): Additional test cases to fill gaps (generated only if gaps found)

## Automation

- **CI Validation**: GitHub Actions automatically validates all CSV files on push/PR
- **Pre-commit Hooks**: Optional local validation before commits
- **Generator Enforcement**: Skill instructions require template compliance

## Documentation

- **Agent Configuration**: `.github/agents/Test Case Generator.agent.md`
- **Validation Guide**: `.github/agents/Test Case Generator/agents-context/VALIDATION_GUIDE.md`
- **Skills Documentation**:
  - Generate Test Plan: `.github/agents/Test Case Generator/agents-context/skills/Generate Test Plan/Skill/SKILL.md`
  - Generate Zephyr Test Case: `.github/agents/Test Case Generator/agents-context/skills/Generate Zephyr Test Case/Skill/SKILL.md`
  - TestCase Coverage Gap: `.github/agents/Test Case Generator/agents-context/skills/TestCase Coverage Gap/Skill/SKILL.md`
- **Template File**: `.github/agents/Test Case Generator/agents-context/skills/Test Case/Template/ZephyrTestCaseTemplate.csv`

## Contributing

When adding CSV files:
1. Use the Zephyr template (16 columns only)
2. Run validation script locally
3. Ensure CI validation passes
4. No extra/missing columns allowed
 
