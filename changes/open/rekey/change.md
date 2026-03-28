# Rekey
**Type**: Proposal
**Status**: Draft

## Intent

When a passphrase needs to be rotated, there is no way to update it without manually re-adding each secret. `--rekey` addresses this by iterating all stored secrets, decrypting those that match the old passphrase, and re-encrypting them under the new one. Secrets encrypted with a different passphrase are left untouched.

## Specification Deltas

### ADDED
- `tok --rekey` prompts interactively for an old passphrase, a new passphrase, and a confirmation of the new passphrase.
- All secrets that decrypt successfully with the old passphrase are re-encrypted under the new passphrase.
- Secrets that do not decrypt with the old passphrase are left unchanged.
- On completion, `tok --rekey` reports how many secrets were rekeyed.
