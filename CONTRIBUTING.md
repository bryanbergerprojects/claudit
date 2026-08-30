# Contributing to claudit

## Setup

See [`aidd_docs/INSTALL.md`](aidd_docs/INSTALL.md).

## Workflow

1. Open an issue first — a branch without an issue has no name (`aidd_docs/memory/vcs.md`).
2. Branch off `main`, named `{type}/{issue_number}`.
3. Implement while keeping the architecture boundaries: `src/core/` imports neither `electron` nor `node:fs`.
4. Add or extend tests alongside the code.
5. Run the validation gates before opening a pull request.

## Conventions

- Commits: conventional commits (`<type>(<scope>): description`), imperative, lowercase, no trailing period.
- Scopes follow the zones of `src/`: `core`, `ingest`, `main`, `preload`, `renderer`, `db`, `config`, `recommend`, `ipc`, plus `deps` and `ci`.
- Issues, pull request bodies and review threads are written in French; commit messages and pull request titles in English.
- Pull requests open ready for review, never as drafts, and close their issue with `Closes #<n>`.
- Validation runs locally, not in CI: `biome check` before a commit, then `tsc --noEmit` and `vitest run` before a push.

## AI context

Changing project memory, skills, rules, agents, commands or hooks follows
[`aidd_docs/CONTRIBUTING.md`](aidd_docs/CONTRIBUTING.md).
