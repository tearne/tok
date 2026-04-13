# Tab Completion for Secret Names

## Intent
When a user types `tok` followed by a partial name and presses Tab, the shell should complete the name against the list of stored secrets. If multiple secrets share the given prefix, all matches should be listed so the user can see what's available and refine their choice. This removes the need to run `tok --list` separately to recall exact names, which is the most common friction point when retrieving a secret.

## Approach
Add a `--completions <shell>` flag to `tok` that prints a shell-specific completion script to stdout. The user sources or installs this script once, and from then on Tab triggers completions.

Supported shells: **Bash** and **Zsh**. These cover the vast majority of interactive users. Fish can be added later if needed.

The generated completion scripts will call `tok --list` to obtain candidates at completion time. This reuses existing logic and stays correct as secrets are added or removed — no caching or stale state. The `--list` path is cheap (a single directory glob) so latency is negligible.

Completion applies to the positional `name` argument only. It should not fire after `--add` (since the user is choosing a new name, not picking from existing ones). Flag completion (`--add`, `--list`, etc.) is included for convenience.

The `--completions` flag is mutually exclusive with other operations — it prints the script and exits.

Version bump: patch (1.1.0 → 1.1.1) since this adds a convenience feature with no change to existing behaviour.

Review cadence: at the end.

SPEC update: add `--completions` to Usage and a verification note.

## Plan
- [x] UPDATE SPEC — add `--completions <shell>` to Usage, document behaviour (prints completion script and exits, supported shells: bash/zsh), and add a verification note that completions can be tested by sourcing the output and checking candidates
- [x] ADD IMPL — add `--completions` argument to argparse (choices: `bash`, `zsh`), mutually exclusive with other operations; when supplied, print the appropriate completion script to stdout and exit
- [x] ADD IMPL — write the Bash completion script as an inline string in `tok.py`; complete secret names via `tok --list` for the positional argument, complete flags for option arguments, suppress name completion after `--add`
- [x] ADD IMPL — write the Zsh completion script as an inline string in `tok.py`; same behaviour as the Bash variant
- [x] ADD TEST — `tok --completions bash` exits 0 and produces output containing the expected function name
- [x] ADD TEST — `tok --completions zsh` exits 0 and produces output containing the expected function name
- [x] ADD TEST — `tok --completions invalid` exits non-zero
- [x] UPDATE IMPL — bump VERSION from 1.1.0 to 1.1.1
- [x] REVIEW — run full test suite, verify no regressions

## Conclusion
All tasks completed as planned — no deviations or surprises.
