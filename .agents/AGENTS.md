# Agent rules and adapters

Applies when editing `.agents/`, `.claude/`, or any `AGENTS.md` / `CLAUDE.md`.

- **Root `AGENTS.md`:** what every task needs, plus a pointer to each rule. Keep it short.
- **`.agents/rules/*.md`:** conventions for one kind of change. `paths` frontmatter scopes them for clients
  that support it; `.claude/rules` is a symlink to this folder.
- **`.agents/plugins/`:** the Codex marketplace manifest. It is part of the published plugin, not guidance.
- **`CLAUDE.md`** files only contain `@AGENTS.md`.

Put each lesson in the first place that can hold it: a check (`claude plugin validate`, CI), then a rule,
then the root `AGENTS.md` only if every task needs it.
