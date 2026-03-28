# Proposal: POS Guard and Shebang Argument Passing
**Status: Archived**

## Intent

Two related issues with the script's invocation setup:

1. **POS style violation**: The uv/venv guard is at module level rather than in the `__main__` guard. POS specifies the guard belongs in `if __name__ == "__main__"` as an invocation-mode concern, not business logic. The current placement means it runs even when the module is imported (e.g. by the test suite), which requires tests to set environment variables to avoid the guard firing.

2. **Shebang defensive hardening**: When `tok` is invoked, the shebang expands to `uv run --script /path/to/tok <args>`. Adding `--` (`uv run --script --`) explicitly terminates `uv`'s own argument parsing, making it unambiguous that all subsequent arguments belong to the script. This guards against any future `uv` version introducing a short flag that collides with one of `tok`'s arguments. The current POS.md shebang example does not include `--`; this proposal extends it.

## Specification Deltas

### MODIFIED
- The uv/venv guard must be placed inside the `__main__` guard, not at module level.
- The shebang must use `uv run --script --` to unambiguously terminate `uv`'s argument parsing.

### MODIFIED (POS.md)
- Update the POS.md shebang example to include `--`.
