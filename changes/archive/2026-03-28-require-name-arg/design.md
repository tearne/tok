# Design: Require Name Argument
**Status**: Implementing

## Approach

In `tok.py`, change the `name` positional from optional to required by removing `nargs="?"` and `default=None`. Argparse will then enforce presence and emit a usage error automatically, so the manual `if not args.name` guards in the `--add` and retrieve paths can be removed.

## Tasks

1. ✓ Tests: existing tests already cover no-name cases; no changes needed
2. ✓ Impl: enforce `name` via `parser.error` in both `--add` and retrieve paths; `--list` exempted since it doesn't need a name
3. ✓ Verify: all 9 tests pass
4. Process: confirm ready to archive
