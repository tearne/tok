# README Installation Instructions

## Intent

The README currently contains only a heading. Users who find the repository have no way to know what `tok` is, how to install it, or how to configure it. The README should briefly explain what `tok` does — a way to manage secrets such as GitHub fine-grained personal access tokens — then tell them how to download the script, what prerequisites they need, and how to enable tab completion.

## Approach

Replace the current single-line README with minimal sections: a one-liner description, prerequisites, installation (curl from GitHub raw URL to `~/.local/bin/tok` and chmod), and tab completion setup for bash and zsh using `tok --completions <shell>`.

Keep it short — no usage reference (the script has `--help`), no feature list. The SPEC and `--help` are the authoritative sources for behaviour; the README just gets people running.

The GitHub raw URL will use the pattern `https://raw.githubusercontent.com/tearne/tok/main/tok.py`.

## Plan
