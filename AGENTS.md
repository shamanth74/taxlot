# Rules for AI agents working on taxlot

- Go, stdlib-first. Do not add dependencies or edit go.mod without being told.
- `internal/domain` and `internal/engine` must not import store, importers or cmd.
- Money is `decimal.Decimal`, never float64. No I/O in domain or engine.
- Show a plan and wait for approval before changing files. Only touch files named in the task.
- Never run git push, rm -rf, or commands with sudo. Never read or request real tradebooks.
- Do not state tax rules as fact; mark them unverified.

## Project
taxlot: a local-first, open-source Indian capital-gains engine, single Go binary.
- Imports broker tradebooks (xlsx/csv), normalizes them into trades, runs FIFO per
  demat account and instrument, and explains every number.
- v0.1 scope: equity delivery only, Zerodha plus one more broker, CLI only.
- Non-goals: web UI, mutual funds, F&O/intraday, any LLM in the calculation path.
- Architecture: domain and engine import nothing from importers/store. The engine is a
  pure function with no I/O. Imports are idempotent. Derived data is rebuildable.
- Tax rules are unverified until checked against the Income Tax Department or a CA.