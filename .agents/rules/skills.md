---
paths:
  - "skills/**"
---

# Writing skills

The human-facing rules are in [CONTRIBUTING.md](../../CONTRIBUTING.md); follow them. In short:

- One folder per skill, `skills/<name>/SKILL.md`, `name` equal to the folder, prefixed `firstpromoter-`.
- The `description` says what the skill does and when to use it; agents pick skills from it.
- Facts (endpoints, snippets, settings, tool names) come from https://docs.firstpromoter.com
  (`/llms.txt`) and the MCP tool reference; link to them instead of copying, and check a fact there before
  writing it.
- MCP skills are read-only by default and confirm every write. Money movement stays in the dashboard.
- No API keys, customer data or real affiliate data in examples. Use `example.com` addresses.
- After a change: `claude plugin validate .` and `npx skills add . --list`.
