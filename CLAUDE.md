# CLAUDE.md

Guidance for Claude Code when working in this repository.

## Purpose

This repo holds a personal `tmux` configuration file (`.tmux.conf`) used in a WSL environment, plus a `README.md` documenting related terminal setup (including Shift+Enter keybindings for Windows Terminal and VS Code). It is a dotfiles-style config repo, not an application — there is no build, test, or lint step.

## Working in this repo

- The canonical config file is `.tmux.conf`. Keep changes minimal and preserve the existing comment style (a short comment above each setting explaining *why*, not just what).
- This repo is not currently a git repository. If the user asks to commit, confirm whether to run `git init` first.
- When adding new keybindings or options to `.tmux.conf`, group them near related existing settings rather than appending to the end.
- Don't add plugin managers (e.g. TPM) or split `.tmux.conf` into multiple files unless the user asks — the config is intentionally a single flat file.
- `README.md` documents companion terminal config that lives outside this repo (e.g. Windows Terminal's `settings.json`, VS Code's `keybindings.json`). When editing JSON snippets in `README.md`, keep escape sequences like `\r` as literal text (JSON source), never as raw control bytes — a raw ESC byte pasted into the file is a bug, not a valid alternative.
