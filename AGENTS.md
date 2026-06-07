# AI Agent Guide for ghūl Examples

## Purpose

This guide is for AI agents and other automated contributors working on the ghūl example projects hosted in this repository. Follow these steps to keep changes safe and ensure the examples keep building and running correctly.

## Background

- The examples demonstrate the [ghūl programming language](https://ghul.dev/).
- The ghūl compiler and test tool are provided as .NET local tools. Run `dotnet tool restore` if needed.
- See [GHUL.md](./GHUL.md) for a quick language tutorial and reference. This file is a synced copy - see "Keeping GHUL.md in sync" below.

## Keeping GHUL.md in sync

`GHUL.md` is **not authored here.** The master copy lives in the [`ghul`](https://github.com/degory/ghul) compiler repo (`ghul/GHUL.md`), which is updated whenever the language changes. The copy in this repo exists so the examples are self-contained.

When you open a PR that touches this repo, check whether the master `GHUL.md` has moved ahead of the copy here, and if so refresh it as part of your PR:

```sh
diff path/to/ghul/GHUL.md GHUL.md   # any output => out of date
cp  path/to/ghul/GHUL.md GHUL.md    # refresh, then commit
```

Only sync when it's genuinely out of date and you're already touching this repo - don't open a PR solely to sync (the compiler repo's own PRs keep the master current). Never hand-edit `GHUL.md` here to fix a language-reference error; fix it in the `ghul` repo's master copy and let the sync carry it over.

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
