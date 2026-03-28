# Proposal: Semantic Versioning
**Status: Draft**

## Intent

A version mismatch between systems was the likely cause of unexpected behaviour (a secret being stored under the wrong name). With no version number in the script, there is no easy way to identify which version is installed or whether it is out of date. Introducing a `__version__` string and exposing it via `--version` makes mismatches immediately visible.

## Specification Deltas

### ADDED
- The script must define a version using semantic versioning (`MAJOR.MINOR.PATCH`).
- `tok --version` must print the version and exit.
- The initial version is `1.0.0`.
