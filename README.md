# tok

Encrypt and retrieve secrets (such as GitHub fine-grained personal access tokens) from the terminal. Secrets are encrypted with a passphrase using OpenSSL and copied to the clipboard via OSC 52.

## Prerequisites

[uv](https://docs.astral.sh/uv/) - handles Python and dependencies automatically.

## Install

```bash
curl -fsSL https://raw.githubusercontent.com/tearne/tok/main/tok.py -o ~/.local/bin/tok && chmod +x ~/.local/bin/tok
```

Ensure `~/.local/bin` is on your `PATH`.

## Tab Completion

**Bash** — add to `~/.bashrc`:

```bash
eval "$(tok --completions bash)"
```

**Zsh** — add to `~/.zshrc`:

```zsh
eval "$(tok --completions zsh)"
```

Restart your shell or source the file to activate.
