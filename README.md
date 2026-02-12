# ai-qa-testcasegenerator

This repository generates comprehensive test plans and Zephyr-ready test cases for QA testing.

## Features

✅ **Automated Test Plan Generation**: Creates detailed test plans with RTM, coverage models, and test scenarios  
✅ **Zephyr CSV Export**: Generates test cases in Zephyr Scale import-ready CSV format  
✅ **Template Enforcement**: Strict validation ensures 100% Zephyr format compliance  
✅ **Multi-Type Coverage**: Functional, Regression, Smoke, E2E, Integration, Negative, and Edge test cases  
  


### Generate Test Cases

1. Place requirements in: `.github/agents/Test Case Generator/agents-context/skills/Test Case/Requirement/requirement.md`
2. Run the test case generator (via GitHub Copilot or CLI)
3. Output files created:
   - Test Plan: `.github/agents/Test Case Generator/agents-context/TestPlan/[ProjectName]_TestPlan.md`
   - Zephyr CSV: `.github/agents/Test Case Generator/agents-context/ZephyrReadyTestCases/[ProjectName]_Zephyrimportready.csv`

### Validate CSV Format

Validate a single CSV file:
```powershell
python ".github/agents/Test Case Generator/agents-context/scripts/validate_zephyr_csv.py" "path/to/file.csv"
```

Validate all CSV files:
```powershell
python ".github/agents/Test Case Generator/agents-context/scripts/validate_zephyr_csv.py" --validate-all
```

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

For detailed documentation, see: [VALIDATION_GUIDE.md](.github/agents/Test%20Case%20Generator/agents-context/VALIDATION_GUIDE.md)

## Automation

- **CI Validation**: GitHub Actions automatically validates all CSV files on push/PR
- **Pre-commit Hooks**: Optional local validation before commits
- **Generator Enforcement**: Skill instructions require template compliance

## Documentation

- **Validation Guide**: `.github/agents/Test Case Generator/agents-context/VALIDATION_GUIDE.md`
- **Generator Skill**: `.github/agents/Test Case Generator/agents-context/skills/Generate Zephyr Test Case/Skill/SKILL.md`
- **Template File**: `.github/agents/Test Case Generator/agents-context/skills/Test Case/Template/ZephyrTestCaseTemplate.csv`

## Contributing

When adding CSV files:
1. Use the Zephyr template (16 columns only)
2. Run validation script locally
3. Ensure CI validation passes
4. No extra/missing columns allowed
 
