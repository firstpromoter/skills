# Git conventions

This repository is public. Nothing internal goes into git or GitHub: no ticket IDs or links, no internal
analytics, customer data, internal repo or secret names, or internal plans.

## Authorization

- Leave changes uncommitted by default. Commit, push or open/update a PR when the user requests it.
- Never force-push, amend published commits or push directly to `main` without an explicit request.

## Branch naming

Format: `{type}-{short-description}`, e.g. `feat-migrate-skill`, `fix-integrate-nextjs-snippet`. No ticket IDs.

## Commit messages and PR titles

Conventional Commits without a ticket scope: `<type>: <description>` (or `<type>(<skill>): <description>`).

- `<type>`: feat, fix, docs, refactor, chore, ci, build, revert
- Imperative mood, first line 50 characters or less; body explains why and what.

## Pull requests

- Target `main`; PRs are squash-merged, so the PR title becomes the commit message.
- The description says what changed and how it was checked (`claude plugin validate .`, `npx skills add . --list`).
  Nothing else: no internal links, numbers or follow-up plans.

## Releases

Bump `version` in `plugin.json`, `.claude-plugin/plugin.json`, `.codex-plugin/plugin.json`,
`.cursor-plugin/plugin.json` and every `SKILL.md`, update `CHANGELOG.md`, then tag `vX.Y.Z` on `main` and
create a GitHub Release with the changelog entry.
