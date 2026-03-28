# Design: POS Guard and Shebang Argument Passing
**Status: Draft**

## Approach

Two small, independent edits to `tok.py`:

1. **Shebang**: change `#!/usr/bin/env -S uv run --script` to `#!/usr/bin/env -S uv run --script --`.

2. **Guard**: remove the module-level guard block and move it into the `__main__` guard at the bottom of the file, per POS style. The guard checks both `VIRTUAL_ENV` and `UV_INTERNAL__PARENT_INTERPRETER` — both must be retained because `uv run --script` sets `UV_INTERNAL__PARENT_INTERPRETER` (not `VIRTUAL_ENV`), so dropping either would break normal invocation or direct venv use. The POS.md example only shows `VIRTUAL_ENV` as a simplified illustration; the intent is that the check lives in `__main__`, not that it must use exactly that variable.

The signal test (`test_signal_clears_clipboard`) currently passes `VIRTUAL_ENV=1` via `env_extra` to work around the module-level guard firing on import. Once the guard is in `__main__`, that workaround is no longer needed and should be removed.

## Tasks

1. **Impl**: Update shebang to `#!/usr/bin/env -S uv run --script --`
2. **Impl**: Remove module-level guard; add it to the `__main__` block before `main()`
3. **Tests**: Remove `env_extra={"VIRTUAL_ENV": "1"}` from `test_signal_clears_clipboard`
4. **Verify**: Run tests
5. **Process**: Confirm ready to archive
