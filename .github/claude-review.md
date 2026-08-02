# Cloud code review brief

What this repository is, and what to watch for in it. Everything else - what PR
context is available, how to post a review, what makes a finding worth raising,
comment hygiene, PR-description shape, the versioning mechanism - comes from the
review workflow's runtime notes. Don't restate it here: this file is read first,
so a stale copy would silently override the current text.

Not loaded by local Claude Code; only the cloud reviewer reads this.

## What this repo is

`ghul-examples` is the worked-example corpus for the ghūl language: standalone
programs that people read to decide whether the language is usable, and that CI
compiles and runs against snapshot expectations. `STYLE.md`, fetched from
`degory/ghul-style`, is authoritative for prose, comments and code style here.

Clarity outranks cleverness. Code a newcomer to ghūl would find surprising is a
defect in this repo even when it is correct.

## What to watch for here

- Non-idiomatic ghūl. An idiom nobody would recommend teaches the wrong thing to
  the audience this repo exists for. Prefer the plain construction.
- `STYLE.md` violations, in priority order: hard bans on any occurrence;
  conditional bans where the qualifier holds; banner-comment violations;
  vocabulary and comment-case drift; deprecated idioms.
- Comment prose that explains the language rather than the example. These files
  are read top to bottom by someone learning; a comment restating what the line
  plainly does is noise, and one narrating compiler internals is off-topic.
- Examples drifting from what the compiler now accepts, or from the README's
  stated prerequisites.

## Versioning

This repo publishes nothing. Version bumps are not a concern here; the compiler
pin in `.config/dotnet-tools.json` should track the latest published release.
