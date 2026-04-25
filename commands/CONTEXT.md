# commands — Slash commands
> Last updated: 2026-04-25

Standalone `.md` files that define slash commands. Each file is a
prompt that gets loaded when the user types the corresponding
`/<command-name>` in Claude Code.

Inherits: top-level `CONTEXT.md`.

## Inventory
| Command                | Purpose                                          | Related skill       |
|------------------------|--------------------------------------------------|---------------------|
| `/gleam-review`        | Review Gleam code against best practices         | `gleam`             |
| `/gleam-backend`       | Build a Gleam backend feature                    | `gleam`             |
| `/gleam-frontend`      | Build a Gleam/Lustre frontend feature            | `gleam`             |
| `/otp-review`          | Audit OTP actors, supervision, concurrency       | `gleam`             |
| `/code-simplifier`     | Simplify and refine Gleam code                   | `code-simplifier`   |
| `/observability-master`| Find unlogged error branches, add logging        | `observability-master` |
| `/tdd`                 | Test-Driven Development workflow                 | `tdd`               |

## Convention
- File name matches the command name: `gleam-review.md` → `/gleam-review`
- Commands reference skills for detailed patterns but are self-contained prompts
- Keep commands focused on a single workflow or audit
