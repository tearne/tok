# Require Name Argument
**Type**: Proposal
**Status**: Archived

## Intent
`tok -a grit` stores the secret as `default` instead of `grit` because `name` is an optional positional with a `None` default, and the `-a` flag does not consume `grit` as the name. The fix removes the concept of a default secret entirely, making `name` a required positional argument.

## Specification Deltas

### MODIFIED
- `name` argument: was optional (with no default), now required; `tok` and `tok -a` without a name produce a usage error

### REMOVED
- The concept of a default secret (previously possible via `nargs="?"`)
