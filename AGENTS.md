# FirstPromoter skills

This guide applies to the whole repository. `CLAUDE.md` imports it for Claude Code. Rules live in
[.agents/rules/](.agents/rules); [.agents/AGENTS.md](.agents/AGENTS.md) explains that layout.

## This project

The public, MIT-licensed repository of FirstPromoter [Agent Skills](https://agentskills.io), installable
in Claude Code, Codex, Cursor, Copilot and any `SKILL.md`-compatible agent. **Everything here is public**:
the code, commit messages, branch names, PR titles and descriptions, issues and releases.

## Layout

```
skills/<name>/SKILL.md     # the product: one folder per skill, names prefixed firstpromoter-
plugin.json                # Agent Plugins manifest
.claude-plugin/            # Claude Code plugin + marketplace (source "./")
.codex-plugin/             # Codex plugin manifest
.agents/plugins/           # Codex marketplace manifest (published, not agent guidance)
.cursor-plugin/            # Cursor plugin manifest
.mcp.json                  # bundled FirstPromoter MCP server (https://mcp.firstpromoter.com)
assets/icon.png            # listing icon (square PNG)
.github/workflows/sync-docs.yml  # on v* tags, syncs skills/ to docs.firstpromoter.com
.agents/rules/             # rules for agents working in this repo (.claude/rules links here)
```

## Key commands

- Validate the plugin and marketplace: `claude plugin validate .`
- Check skill discovery: `npx skills add . --list`

Run both before opening a PR that touches `skills/` or any manifest.

## Rules

- **No internal context, ever.** Never put internal ticket links or IDs (Fibery), internal analytics or usage
  numbers, customer names or data, internal repo names, secret names or internal plans in files, commit
  messages, branch names, PR titles or descriptions, issues or release notes. Describe what the change does
  and how it was checked. Internal tracking stays in internal tools.
- Git and PR conventions: [.agents/rules/git-conventions.md](.agents/rules/git-conventions.md).
- Writing or changing a skill: [.agents/rules/skills.md](.agents/rules/skills.md).
