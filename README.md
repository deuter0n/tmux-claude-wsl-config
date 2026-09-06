# tmux-claude-wsl-config

Personal `tmux` configuration used in a WSL (Windows Subsystem for Linux) environment alongside Claude Code.

## Contents

- [`.tmux.conf`](./.tmux.conf) — tmux configuration file

## What's configured

- **Mouse support** — click to select panes/windows, drag to resize, scroll to view history
- **Focus events** — so Claude Code can fire notifications correctly (also used by vim/nvim and similar apps)
- **50,000-line scrollback** — increased from the default 2,000
- **1-indexed windows/panes** — easier to reach on the keyboard than 0
- **vi-style copy mode** — enter with `prefix + [`, then arrow keys (or `h/j/k/l`) to navigate, `Space` (or `v`) to start selection, `Enter` (or `y`) to copy
- **Custom split bindings** — `prefix + |` for horizontal split, `prefix + -` for vertical split, both opening in the current pane's path
- **`prefix + c`** — new window, opening in the current pane's path
- **Alt+Arrow** — switch panes *without* needing the tmux prefix
- **`prefix + r`** — reload the config with a status-bar confirmation

## Installation

```bash
cp .tmux.conf ~/.tmux.conf
tmux source-file ~/.tmux.conf   # or restart tmux
```

## Enable Shift+Enter

Inside tmux/WSL, some apps (e.g. Claude Code) treat `Shift+Enter` as "insert a newline without submitting." Neither Windows Terminal nor VS Code sends this by default, so it must be mapped explicitly by sending the `Esc` + `Enter` sequence (`\u001b\r`), which is what Claude Code interprets as a newline instead of a submit.

### Windows Terminal (WSL)

1. Open Windows Terminal.
2. Open **Settings** (`Ctrl+,`), then click **Open JSON file** (bottom-left) to edit `settings.json` directly.
3. Add the following entry to the top-level `"actions"` array:

   ```json
   {
       "command": { "action": "sendInput", "input": "\u001b\r" },
       "keys": "shift+enter"
   }
   ```

4. Save the file — Windows Terminal picks up `settings.json` changes immediately, no restart needed.
5. Test it inside a WSL tab: `Shift+Enter` should insert a newline instead of submitting.

This change lives in Windows Terminal's `settings.json` (on the Windows side), not in this repo's `.tmux.conf`, but is documented here since it's part of the same WSL terminal setup.

### VS Code (integrated terminal)

The VS Code integrated terminal needs the same `Esc`+`Enter` sequence mapped via a keybinding.

1. Open **Keyboard Shortcuts (JSON)**: `Ctrl+Shift+P` → "Preferences: Open Keyboard Shortcuts (JSON)".
2. Add the following entry to the array in `keybindings.json`:

   ```json
   {
       "key": "shift+enter",
       "command": "workbench.action.terminal.sendSequence",
       "args": { "text": "\u001b\r" },
       "when": "terminalFocus"
   }
   ```

3. Save the file — VS Code picks up `keybindings.json` changes immediately, no restart needed.
4. Test it in the integrated terminal (including inside WSL): `Shift+Enter` should insert a newline instead of submitting.
