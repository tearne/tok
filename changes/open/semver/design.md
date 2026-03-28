# Design: Semantic Versioning
**Status: Draft**

## Approach

Two small edits to `tok.py`:

1. Add `__version__ = "1.0.0"` near the top of the file, after the imports.
2. Add `parser.add_argument("--version", action="version", version=f"%(prog)s {__version__}")` to the argparse setup. argparse handles this natively — it prints `tok 1.0.0` and exits with code 0.

One new test in `tests.py` to cover `--version` output.

## Tasks

1. **Tests**: Add `test_version_flag` — run `tok --version`, assert exit code 0 and `1.0.0` in output
2. **Verify**: Run new test, confirm it fails
3. **Impl**: Add `__version__` and `--version` argument to `tok.py`
4. **Verify**: Run tests
5. **Process**: Confirm ready to archive
