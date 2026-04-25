# aboio-skills — Agent Skills for Gleam + Postgres development
> Last updated: 2026-04-25

Marketplace of skills, commands, and plugins that extend Claude Code
with Gleam language expertise, Postgres best practices, and development
workflows. Consumed by Claude Code via the Aboio marketplace registry.

## Layout
```
aboio-skills/
├── skills/              # Skill packages (SKILL.md + references/)
├── commands/            # Slash commands (standalone .md files)
├── plugins/             # LSP and tool integrations
├── references/          # Shared references used across skills
├── docs/                # Design plans and historical notes
├── registry.json        # Marketplace registry — lists all skills + plugins
├── .claude-plugin/      # marketplace.json (plugin metadata)
├── CONTRIBUTING.md      # How to add/update skills
└── README.md            # Public-facing repo description
```

## Sub-workspaces
| Working on...                    | Read                                  |
|----------------------------------|---------------------------------------|
| Any skill                        | `skills/CONTEXT.md`                   |
| The main Gleam skill             | `skills/gleam/CONTEXT.md`             |
| Postgres skill                   | `skills/pg-gleam/CONTEXT.md`          |
| API design skill                 | `skills/api-gleam/CONTEXT.md`         |
| Slash commands                   | `commands/CONTEXT.md`                 |
| Plugins (LSP)                    | `plugins/CONTEXT.md`                  |
| Docs and plans                   | `docs/CONTEXT.md`                     |
| Publishing / marketplace         | `registry.json` + `.claude-plugin/`   |

## Registry
`registry.json` is the source of truth for what gets published to the
marketplace. Every new skill or plugin must be added here with name,
description, path, and tags.

## Shared references
`references/token-efficiency.md` is imported by multiple skills. Edit
it when changing the token budget strategy — all skills that reference
it will pick up the change.
