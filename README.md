# FirstPromoter skills

Official [Agent Skills](https://agentskills.io) for [FirstPromoter](https://firstpromoter.com), the affiliate and referral platform for SaaS. Use them from Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Windsurf, Amp and any other agent that supports `SKILL.md`.

| Skill | What it does |
|---|---|
| [`firstpromoter-integrate`](skills/firstpromoter-integrate/SKILL.md) | Adds FirstPromoter click, signup and sales tracking to your website or app, connects billing, and tests a referral end to end. |
| [`firstpromoter-manage-program`](skills/firstpromoter-manage-program/SKILL.md) | Answers affiliate support, commission, payout and reporting questions from live data, and lists pending applications. |
| [`firstpromoter-fraud-review`](skills/firstpromoter-fraud-review/SKILL.md) | Checks referrals and commissions for self-referrals, duplicates, refunds, leaked codes and spikes, and reports the evidence. |

The program skills use the [FirstPromoter MCP server](https://docs.firstpromoter.com/mcp/overview) (`https://mcp.firstpromoter.com`, OAuth with your FirstPromoter login). The plugin installs below connect it for you. Skills are read-only by default and ask before any change.

## Install

**Any agent** ([skills CLI](https://skills.sh)):

```bash
npx skills add firstpromoter/skills
```

This installs the skills only. For `firstpromoter-manage-program` and `firstpromoter-fraud-review`, also [connect the MCP server](https://docs.firstpromoter.com/mcp/overview) in your agent.

**Claude Code** (skills + MCP server):

```
/plugin marketplace add firstpromoter/skills
/plugin install firstpromoter@firstpromoter
```

**Codex:**

```bash
codex plugin marketplace add firstpromoter/skills
```

This registers the marketplace; then install **FirstPromoter** from the Codex plugins directory to get the skills and the MCP server.

**GitHub Copilot:**

```bash
gh skill install firstpromoter/skills --all
```

Requires gh 2.90 or later. This installs the skills only; [connect the MCP server](https://docs.firstpromoter.com/mcp/overview) for the program skills.

**Cursor:** copy `skills/` into `.cursor/skills/`, and [connect the MCP server](https://docs.firstpromoter.com/mcp/overview) for the program skills.

**MCP only** (no skills): see [connect the MCP server](https://docs.firstpromoter.com/mcp/overview) for Claude, ChatGPT, Cursor and others.

## Try it

What teams use these skills for most:

| You want to... | Ask your agent |
|---|---|
| Set up tracking | "Integrate FirstPromoter tracking into this app." |
| Fix tracking | "We get referrals but no sales in FirstPromoter. Find out why." |
| Answer an affiliate | "Is jane@example.com one of our affiliates, and which referrals are hers?" |
| Check a payout | "Why is this affiliate's payout still pending?" |
| Report | "Who were our top 10 affiliates last month, and what share of revenue did they bring?" |
| Keep a dashboard fresh | "Every Monday, summarize new referrals, customers and pending commissions." |
| Pending applications | "Show me pending affiliate applications with their website and country." |
| Fraud signals | "Check pending commissions for self-referrals and refunds." |

## Docs

- Developer docs: https://docs.firstpromoter.com ([llms.txt](https://docs.firstpromoter.com/llms.txt))
- MCP tools: https://docs.firstpromoter.com/mcp/tools
- Help center: https://help.firstpromoter.com

## Community

Questions and ideas: [GitHub Discussions](https://github.com/firstpromoter/skills/discussions). Bugs and skill requests: [issues](https://github.com/firstpromoter/skills/issues/new/choose). Contributions welcome, see [CONTRIBUTING.md](CONTRIBUTING.md). For account problems, contact support@firstpromoter.com.

## License

[MIT](LICENSE) · [Privacy](https://firstpromoter.com/privacy)
