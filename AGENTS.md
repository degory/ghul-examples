# AI Agent Guide for ghūl Examples

## Purpose

This guide is for AI agents and other automated contributors working on the ghūl example projects hosted in this repository. Follow these steps to keep changes safe and ensure the examples keep building and running correctly.

## Background

- The examples demonstrate the [ghūl programming language](https://ghul.dev/).
- The ghūl compiler and test tool are provided as .NET local tools. Run `dotnet tool restore` if needed.
- See [GHUL.md](./GHUL.md) for a quick language tutorial and reference.

## Test Requirements

All builds and integration tests must succeed before opening a pull request.

| Step   | How to Run | Typical Duration | Notes |
|--------|-----------|------------------|-------|
| Build  | `dotnet build` | Seconds | Compiles all example projects |
| Integration Tests | `dotnet ghul-test --use-dotnet-build integration-tests` | ~3 minutes | Snapshot-based tests in `integration-tests/` |

### Integration Test Notes

- There is normally **one** test folder per example project.
- Tests typically assert that the program's text output exactly matches the expected output file.
- Source files under `examples/` are symlinked into their corresponding test folder. Preserve these symlinks when modifying or adding tests.
- When you create a new example you must also create a matching test folder that symlinks to the example sources.
- Keep test output deterministic—avoid current dates, random numbers, stack traces, or anything else that changes from run to run.
- Use `integration-tests/capture.sh` to update expectation files after validating output.
- Add or update tests when you change behavior or add new examples.

## Additional Notes

- If tests fail unexpectedly, flag them for human review.
- Keep the `.NET` tool versions up to date. Update `.config/dotnet-tools.json` and run `dotnet tool restore` if newer versions of `ghul.compiler` or `ghul.test` are available.
- Keep commits focused and well documented.
- See [README.md](./README.md) for environment setup and usage tips.

## See Also
- [GHUL.md](./GHUL.md) – Language reference
- [README.md](./README.md) – Project overview
