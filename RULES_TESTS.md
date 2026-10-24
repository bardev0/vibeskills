# Universal testing CI rules

## Rule 1: Quiet test execution

All tests must run in quiet mode by default. In quiet mode, the only console output for each test is:

```text
test xxx started
```

Replace `xxx` with the test name. Suppress all other test output.

## Rule 2: Quiet and verbose modes

Each test script must support two execution modes:

- **Quiet (default):** Follow Rule 1.
- **Verbose:** Show full test output and diagnostic details. Use this mode only when explicitly specified by the user; never enable it automatically, including after a test failure.

Both modes must run the same tests and use the same pass/fail criteria. Only the output verbosity changes.

## Rule 3: Enable or disable tests through `.env`

The `.env` variable `TESTS_ENABLED` controls whether tests run:

- `TESTS_ENABLED=true`: Enable tests.
- `TESTS_ENABLED=false`: Disable tests.
- If unset, tests are disabled by default.

Every test script must respect this setting in both quiet and verbose modes. Disabled tests must not print a test-start message or be reported as passed.

## Rule 4: TypeScript runner and JSON logs

The test runner must be a TypeScript (`.ts`) script.

Each testing suite run must produce a JSON log file named with the timestamp when the suite started, for example `test-results-2026-10-24T14-30-00-123Z.json`.

The JSON log must record each test's name and whether it passed or failed:

- **Passed:** Record the passing result without any test output.
- **Failed:** Record the failing result and all captured test output, including stdout and stderr, for later debugging.

The runner must capture test output in both quiet and verbose modes. The same JSON logging rules apply in either mode; verbosity only controls console output.

## Rule 5: No version changes for test-only requests

When an agent is instructed only to run the test suite, without fixing possible errors, it must never update the project version, regardless of whether tests pass or fail.
