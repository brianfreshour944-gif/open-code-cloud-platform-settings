---
name: code-coverage
description: This skill should be used when the user asks to "run coverage", "measure test coverage", "generate a coverage report", "find untested code", or mentions pytest-cov, coverage.py, or jest coverage.
triggers:
- coverage
- code coverage
- coverage report
- untested code
- pytest-cov
---

# Code Coverage

Run the project's tests under coverage, report the result, and use it to
find untested code. Never change the coverage target to make a number look
better.

## Workflow

1. Detect the language and the test runner already in use. Read the project
   files before running anything:
   - Python: `pyproject.toml`, `setup.cfg`, `pytest.ini`, `tox.ini`
   - JavaScript/TypeScript: `package.json` scripts
   - Java: `pom.xml`, `build.gradle`
   - Go: `go test ./... -cover`
2. Use the existing test command. Do not introduce a new runner.
3. Run tests with coverage and capture both the summary and the report.
4. Report total coverage and the lowest-covered modules.
5. Point at specific untested lines or branches worth covering, with file and
   line numbers.
6. If the user asked for new tests, add focused tests for the highest-risk
   uncovered paths and re-run to confirm the increase.

## Common commands

- Python: `pytest --cov=<package> --cov-report=term-missing`
- Python (existing tooling): `coverage run -m pytest && coverage report -m`
- JavaScript: `npm test -- --coverage` or `npx jest --coverage`
- Go: `go test ./... -coverprofile=coverage.out && go tool cover -func=coverage.out`

Install a coverage tool only if it is missing and the user agrees.

## Report format

```
Command run: <exact command>
Total coverage: NN%
Lowest covered modules:
  path/to/module - NN% (lines X-Y uncovered)
Suggested next tests:
  - path/to/file:line - what to assert
```

## Rules

- Never lower a coverage threshold or exclude files to raise the number.
- Do not add tests that assert nothing or only execute code without checking
  behavior.
- If the project has no test setup, say so and propose one before building it.
