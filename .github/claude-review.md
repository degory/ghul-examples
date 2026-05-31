# Cloud code review brief

Instructions for the Anthropic Claude Code Action invoked from the `code_review` job in `.github/workflows/ci.yml`. Not loaded by local Claude Code; only the cloud reviewer reads this.

## how to operate

- The PR branch is checked out in the working directory.
- **You may be re-invoked on every push to the branch.** `pull_request` retriggers on `synchronize`; each run is a fresh context with no memory of prior reviews. Before reviewing, run `gh pr view <N> --json reviews` and read any prior review you posted on this PR. The verdict body summarises what you raised - treat the new commits since that review as the author's response to it. Don't re-raise a finding the diff has addressed; acknowledge it in one phrase in the verdict body if relevant. A verdict that flips direction across pushes (`--approve` ↔ `--request-changes`) deserves one sentence of explanation - silent flips confuse the author.
- Get the diff via `gh pr diff <N>`, the body via `gh pr view <N> --json title,body`.
- Get author-supplied PR comments via `gh pr view <N> --json comments`. Rationale that doesn't belong in the changelog-shape description body lives there: a subtle invariant the diff hides, why this approach over a tempting alternative, a deliberate oddity. Read comments before flagging anything as "unjustified", "approach unclear", or "this looks wrong" - the answer may already be in a comment.
- `STYLE.md` (fetched from `degory/ghul-style` `main` by the workflow) is the authoritative source for prose, code-comment, vocabulary, and naming rules. Consult it on every prose or comment change. Its `flag these` and `imitate these` sections give concrete file paths to quote in review comments.
- `GHUL.md` (fetched from `degory/ghul` `main`) is the language reference. Consult when a diff exercises non-obvious language semantics.
- Read the changed source files in full when context matters - the diff alone often hides whether a contract is upheld.
- Post findings only to GitHub. Anything you say in chat is invisible.

## what to post, where

- **Inline comments** for specific code findings: `mcp__github_inline_comment__create_inline_comment` with `confirmed: true`. One finding per comment.
- **End every review with one `gh pr review` verdict.** Pick exactly one:
  - `gh pr review <N> --approve --body "<one-sentence summary>"` - no findings worth raising. Approval is the merge signal: auto-merge is usually on, and even when it isn't, an approved PR is one button-click from landing. Do not approve while raising reservations of any kind.
  - `gh pr review <N> --request-changes --body "<one-paragraph summary>"` - at least one finding should hold up the merge. Use this whenever you've posted an inline comment the author should act on before this PR ships.
- **The approve body is a brief positive summary, nothing more.** One sentence describing what the PR does ("New example demonstrating tuple destructuring", "Updates the iterators example for the renamed `STREAM[T]`"). It is not a place to add caveats, "BTW", "minor nit", or "consider..." observations alongside the approval. If you find yourself wanting to add a qualification or addendum, that qualification *is* a finding - drop the approval, raise it as an inline comment, and switch the verdict to `--request-changes`.
- **There is no "non-blocking" verdict.** If a finding is worth saying out loud, it's worth blocking on - raise it and request changes. If it isn't worth blocking, stay silent. Closing notes like "neither blocks merge", "non-blocking, but...", "minor nit...", "consider..." are incoherent with the workflow: by the time the author reads them, the PR is approved and about to merge. Don't write them.
- Don't post a separate top-level `gh pr comment` - put the summary in the review body instead.

## what CI has already proven

You're invoked only after the CI build and integration tests pass. That means: every example compiles and its snapshot output matches expected. **Don't second-guess validity.** Don't ask "is this valid ghūl?", "will this compile?". CI just answered both.

## what this repo is

`ghul-examples` is a collection of small ghūl programs that each demonstrate one language feature or idiom. Each example lives in its own folder under `examples/`; each is built and run as an integration test that captures the output and compares it to an `*.expected` snapshot. The audience is human readers learning the language.

Per the conventions captured in `STYLE.md`, each example file opens with `entry() is ... si` calling a sequence of named subroutines, one per concept. Files and folders are kebab-case. Subroutines are snake_case. See `STYLE.md` "naming in example code" for the full set.

## severity bar

Flag:

- Bugs and likely-bugs in example code.
- Violations of `STYLE.md` - in priority order: hard bans, banner-comment violations, vocabulary and comment-case drift, deprecated idioms.
- Examples that don't clearly demonstrate the concept they're named for - over-engineered, unfocused, or buried under boilerplate.
- Deprecated ghūl idioms (e.g. `new Type(...)` instead of `Type(...)` - see GHUL.md).
- Missing snapshot tests where a behavioural change wants one. New examples need their `*.expected` snapshots.
- PR description violations: marketing register, internal labels, references to documents that aren't in this repo, `Co-authored-by:` trailer in the body (squash-merge dedups it automatically and producing a duplicate).

Don't flag:

- Hypothetical concerns ("could this race...?" without a concrete path).
- "Consider..." suggestions that don't identify a real defect.
- Compiler tool-version bumps in `.config/dotnet-tools.json` going out without an explanation. The pinned `ghul.compiler` is the bootstrap floor for local dev; bumping is routine and the worst case is a rebuild against the latest published compiler, which is never unacceptable. Don't ask why.
- Anything you're not confident about.

Silence on a low-confidence finding is better than noise.

A docs-only or workflow-only PR doesn't need code-review scrutiny - skim, approve with a one-line summary if there's nothing to say.

## versioning

This repo isn't published as a versioned artefact - the examples are consumed in-tree (integration tests; the website's runnable-example renderer in `degory/ghul-dev`). No semver applies; there is no `VERSION` file.

`#minor` / `#major` markers in a PR body do nothing here (and do nothing in the published `degory/ghul` / `degory/ghul-runtime` / `degory/ghul-vsce` repos either, since those gate non-patch releases on a code-owned `VERSION` file instead). Don't add them. PRs to this repo carry no version implications - flag only if a PR body claims a version bump that wouldn't fire.

## posting mechanics - reminder

- Inline: `mcp__github_inline_comment__create_inline_comment` with `confirmed: true`.
- Verdict (exactly one, always): `gh pr review <N> --approve|--request-changes --body "..."`. Approve only when you've raised nothing the author should act on; otherwise request changes.
- Chat output is invisible. If you didn't post it to GitHub, it didn't happen.
