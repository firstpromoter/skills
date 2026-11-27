# Contributing

Thanks for helping improve the FirstPromoter skills.

- **Questions and ideas:** start a thread in [Discussions](https://github.com/firstpromoter/skills/discussions).
- **Bugs and skill requests:** open an [issue](https://github.com/firstpromoter/skills/issues/new/choose).
- **Pull requests:** welcome. Every PR is reviewed by the FirstPromoter team before merge, because these skills run against real affiliate programs.

## Writing or changing a skill

- One folder per skill: `skills/<name>/SKILL.md`, names prefixed `firstpromoter-`.
- Frontmatter needs `name` (same as the folder) and a `description` that says what the skill does and when to use it.
- Link to https://docs.firstpromoter.com for facts (endpoints, snippets, settings) instead of copying them, so skills stay correct when the product changes.
- Skills that use the MCP server are read-only by default and must confirm every write.
- Never include API keys, customer data or real affiliate data in examples.
- Before opening a PR, run `claude plugin validate .` and `npx skills add . --list`.

## Pull requests

- Branch names: `{type}-{short-description}`, e.g. `fix-integrate-nextjs-snippet`.
- PR titles follow Conventional Commits: `<type>: <description>` or `<type>(<skill>): <description>`, imperative, 50 characters or less. PRs are squash-merged, so the title becomes the commit message.
- The description says what changed and how it was checked. This repository is public: no internal links, ticket IDs, customer data or internal plans.
- Don't commit agent guidance files (`AGENTS.md`, `CLAUDE.md`, `.claude/`, `.agents/rules/`). The whole repository is the plugin, and plugin directories refuse them.

## Releases

Maintainers bump `version` in `plugin.json`, `.claude-plugin/plugin.json`, `.codex-plugin/plugin.json`, `.cursor-plugin/plugin.json` and each `SKILL.md`, update `CHANGELOG.md`, and push a `vX.Y.Z` tag.
