# gleam — Comprehensive Gleam skill
> Last updated: 2026-04-25

The largest skill in the repo. Covers language fundamentals, backend
(OTP, Wisp, Mist, SQL codegen), frontend (Lustre 5.x, rsvp, modem),
and library design. The `SKILL.md` provides decision trees; reference
files contain the detailed patterns.

Inherits: `skills/CONTEXT.md`.

## Layout
```
gleam/
├── SKILL.md                         # Main prompt with decision trees
└── references/
    ├── fundamentals/                # Language syntax, patterns, conventions
    │   ├── language-basics.md       # No if, records, imports, constants
    │   ├── language-features.md     # Label shorthand, let assert, pipelines
    │   ├── case-patterns.md         # Pattern matching
    │   ├── code-patterns.md         # use/result.try, helpers
    │   ├── conventions.md           # Official conventions (C1-C10) & anti-patterns (A1-A10)
    │   ├── error-handling.md        # AppError patterns
    │   ├── type-design.md           # Opaque types, parse-don't-validate
    │   ├── decoding.md              # JSON decoding (modern decode API)
    │   ├── decode-map-vs-then.md    # decode.map vs decode.then
    │   ├── stdlib.md                # Useful stdlib functions
    │   ├── stdlib-module-names.md   # Module name gotchas (regexp/regex)
    │   ├── tooling.md               # gleam check/format/fix, LSP actions
    │   ├── common-pitfalls.md       # Frequent mistakes
    │   ├── validation-valid.md      # Input validation (valid library)
    │   ├── parsing-nibble.md        # Parser combinators (nibble)
    │   ├── birdie-snapshot-testing.md
    │   ├── helper-first-refactoring.md
    │   ├── higher-order-sql-helpers.md
    │   └── string-character-filtering.md
    ├── backend/                     # Erlang target — HTTP, DB, OTP, auth
    │   ├── wisp-framework.md        # Wisp routing, middleware, responses
    │   ├── mist-server.md           # Mist HTTP server config
    │   ├── otp.md                   # OTP actors: basics, state, messages
    │   ├── otp-supervision.md       # Supervision trees, strategies
    │   ├── otp-advanced.md          # Selectors, timers, ETS
    │   ├── squirrel-guide.md        # SQL codegen (Squirrel)
    │   ├── parrot-guide.md          # SQL codegen (Parrot/sqlc)
    │   ├── cigogne.md               # Database migrations
    │   ├── three-tier-error-handling.md
    │   ├── decoder-defaults-anti-pattern.md
    │   ├── http-logging-middleware.md
    │   ├── http-runner.md           # HTTP client runner pattern
    │   ├── jwt-ywt.md               # JWT authentication
    │   ├── auth.md                  # Password hashing, timestamps
    │   ├── bucket-s3.md             # S3 / object storage
    │   ├── ansel-image.md           # Image processing
    │   ├── paddlefish-pdf.md        # PDF generation
    │   └── midas-effect-task.md     # Midas algebraic effects
    ├── frontend/                    # JavaScript target — Lustre
    │   ├── lustre-core.md           # MVU architecture, state, messages
    │   ├── lustre-effects.md        # Effects, paint cycle
    │   ├── lustre-routing.md        # SPA routing (modem)
    │   ├── lustre-http.md           # HTTP requests (rsvp)
    │   ├── lustre-components.md     # Web components, slots, CSS parts
    │   ├── lustre-events.md         # Events, debounce, throttle
    │   ├── lustre-ui-patterns.md    # Composable UI, prop pattern
    │   ├── lustre-advanced.md       # Hydration, server components, FFI
    │   ├── lustre-browser-apis.md   # Browser APIs (plinth)
    │   ├── lustre-testing.md        # Testing (query, simulate, birdie)
    │   └── lustre-gotchas.md        # Common Lustre gotchas
    └── library/                     # Library design & FFI
        ├── library-design.md        # Effects as data, no IO in core
        └── ffi.md                   # Erlang + JavaScript FFI
```

## Reference counts
| Category      | Files | Key topics                                      |
|---------------|-------|-------------------------------------------------|
| fundamentals  | 19    | Syntax, patterns, conventions, decoding, tooling |
| backend       | 18    | Wisp, OTP, SQL codegen, auth, storage            |
| frontend      | 11    | Lustre MVU, routing, HTTP, components, testing   |
| library       | 2     | Library design, FFI                              |

## Common Gleam/framework gotchas

These are general language and framework traps the skills cover to
varying degrees. When updating references, ensure these stay documented:

### Decoding
- **`decode.optional_field` crashes on `null`** — it only handles
  *missing* fields. If JSON sends `null`, use `Option(String)`

### SQL codegen (Parrot/Squirrel)
- **SQL is the contract, Gleam bends to it.** Never edit generated
  `sql.gleam` files. Fix the `.sql` source, regenerate, then update
  handlers to match the new types

### Testing with pog
- **No `pog.transaction` inside a rollback test context** — inner
  `COMMIT` commits the outer transaction, killing rollback. Execute
  queries directly on the connection

### Wisp HTTP
- **`wisp.path_segments(req)` returns the FULL path**, not relative
  to mount point
- **There is no `get_header`.** Use `list.key_find(req.headers, name)`.
  Header names are lowercase

### Frontend state (Lustre)
- **Prefer sum types over `Bool` fields in model state.** Aligns with
  convention P4 (Replace Bools with Custom Types). Especially important
  for async states: `Idle | Loading | Loaded(data) | Failed(err)`

## Editing guidance
- `SKILL.md` decision trees must stay in sync with the reference file list
- Reference files are loaded on demand — keep each self-contained
- Follow `references/token-efficiency.md` (shared) for budget strategy
- When adding a reference, add a routing entry in `SKILL.md`
