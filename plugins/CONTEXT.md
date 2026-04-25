# plugins — Tool integrations
> Last updated: 2026-04-25

Plugins extend Claude Code with tool integrations (LSP servers, MCP
tools, etc.). Each plugin is a directory with a `README.md` and
configuration files.

Inherits: top-level `CONTEXT.md`.

## Inventory
| Plugin       | Purpose                                              |
|--------------|------------------------------------------------------|
| `gleam-lsp`  | Gleam language server for code intelligence          |

## gleam-lsp
Spawns `gleam lsp` over stdio. Provides diagnostics, go-to-definition,
find-references, hover, completion, formatting, and code actions.

Requires the `gleam` binary in PATH. No configuration beyond the
LSP command itself.
