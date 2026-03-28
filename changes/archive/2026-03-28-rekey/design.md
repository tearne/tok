# Design: Rekey
**Status: Implementing**

## Approach

Add `--rekey` to `tok.py`. The flow:

1. Prompt for old passphrase, new passphrase, and confirmation.
2. Iterate all `.enc` files in `TOK_DIR`.
3. For each file, attempt to decrypt with the old passphrase. If decryption fails, skip silently.
4. If decryption succeeds, re-encrypt the plaintext with the new passphrase, writing to a temp file in the same directory, then atomically replacing the original via `os.replace`. This ensures a failure mid-batch cannot leave a secret partially written.
5. Report the count of rekeyed secrets.

No new helpers needed — the openssl subprocess calls follow the same pattern as add and retrieve.

## Tasks

1. ✓ **Tests**: Add `test_rekey_matching` — store two secrets with the same passphrase and one with a different passphrase; rekey the first two; verify all three still decrypt correctly under their respective new/unchanged passphrases
2. ✓ **Tests**: Add `test_rekey_no_matches` — rekey with a passphrase that matches nothing; assert exit code 0 and 0 rekeyed reported
3. ✓ **Verify**: Run new tests, confirm they fail
4. ✓ **Impl**: Add `--rekey` flag and handler to `tok.py`
5. ✓ **Verify**: Run all tests — 12 passed
6. **Process**: Confirm ready to archive
