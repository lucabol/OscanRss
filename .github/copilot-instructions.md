# Copilot Instructions for OscanRss

## Build & Test

```powershell
.\build.ps1              # Build (requires oscan in PATH)
.\build.ps1 -Run         # Build and run
.\build.ps1 -V           # Verbose
.\build.ps1 -Test        # Run all tests
.\build.ps1 -Clean       # Remove build/
```

## Language: Oscan

Written in [Oscan](https://github.com/lucabol/Oscan). Critical reminders:

- `fn` = pure (no I/O), `fn!` = impure. Pure cannot call impure.
- Use `and`/`or`/`not` instead of `&&`/`||`/`!`.
- All variables require explicit type annotations: `let x: i32 = 5;`
- Semicolons after **every** block statement: `if {} else {};` `while {};` `for {};`
- String comparison: `str_eq(a, b)`, not `==`.
- Anti-shadowing: variable names cannot be reused in nested scopes.
- No self-referential structs. Use flat arrays with integer indices.

## Architecture

`main.osc` is the entry point. Module imports:

```
main.osc
  ├── use "url.osc"       — URL parsing
  ├── use "http.osc"      — HTTP/HTTPS client
  ├── use "rss_parse.osc" — RSS XML parser
  ├── use "storage.osc"   — Persistent storage
  └── use "libs/ui.osc"   — UI widgets
```

### Data Model

Groups/feeds use flat arrays. No self-referential structs.
Read state tracked via `map` (guid → "1").

### Key Conventions

- No `arena {}` blocks around persistent `push()` calls.
- Clear arrays in-place: `while len(arr) > 0 { pop(arr); };`
- Keyboard input processed before render, outside arena scope.
