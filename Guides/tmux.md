# tmux Guide

> Terminal multiplexer — multiple sessions, windows, panes. Keeps everything running when you close the terminal.

---

## The Hierarchy

```
Server
  └── Session  (e.g. "work", "api", "personal")
        └── Window  (like browser tabs)
              └── Pane  (splits within a window)
```

---

## Prefix Key

> All tmux commands start with: **`Ctrl+b`**
> Press and *release* Ctrl+b, then press the next key.

---

## Starting tmux

| Command | Action |
|---------|--------|
| `tmux` | New session |
| `tmux new -s work` | New named session |
| `tmux ls` | List all sessions |
| `tmux attach` | Re-attach to last session |
| `tmux attach -t work` | Re-attach to named session |
| `tmux kill-session -t work` | Kill a session |

---

## Sessions

| Key | Action |
|-----|--------|
| `Ctrl+b d` | Detach (session keeps running) |
| `Ctrl+b $` | Rename session |
| `Ctrl+b s` | List sessions interactively |
| `Ctrl+b (` | Previous session |
| `Ctrl+b )` | Next session |

> **Best workflow:** One session per project. Detach with `Ctrl+b d`. Come back with `tmux attach -t name`. Everything is still running.

---

## Windows

| Key | Action |
|-----|--------|
| `Ctrl+b c` | New window |
| `Ctrl+b ,` | Rename window |
| `Ctrl+b &` | Close window |
| `Ctrl+b n` | Next window |
| `Ctrl+b p` | Previous window |
| `Ctrl+b 0–9` | Switch to window by number |
| `Ctrl+b w` | List all windows with preview |
| `Ctrl+b l` | Toggle last active window |

---

## Panes (Splits)

| Key | Action |
|-----|--------|
| `Ctrl+b %` | Split vertical (side by side) |
| `Ctrl+b "` | Split horizontal (top/bottom) |
| `Ctrl+b x` | Close current pane |
| `Ctrl+b z` | Zoom / fullscreen pane (again to unzoom) |
| `Ctrl+b o` | Cycle to next pane |
| `Ctrl+b q` | Show pane numbers |
| `Ctrl+b !` | Break pane into its own window |

### Navigating panes

> Your setup has **vim-tmux-navigator** — use `Ctrl+h/j/k/l` everywhere (works in both Neovim splits AND tmux panes).

| Key | Action |
|-----|--------|
| `Ctrl+h` | Move left |
| `Ctrl+j` | Move down |
| `Ctrl+k` | Move up |
| `Ctrl+l` | Move right |

### Resizing panes

| Key | Action |
|-----|--------|
| `Ctrl+b Ctrl+↑` | Resize up |
| `Ctrl+b Ctrl+↓` | Resize down |
| `Ctrl+b Ctrl+←` | Resize left |
| `Ctrl+b Ctrl+→` | Resize right |
| `Ctrl+b Space` | Cycle layout presets |

---

## Copy Mode (scroll terminal history)

| Key | Action |
|-----|--------|
| `Ctrl+b [` | Enter copy mode |
| `q` | Exit copy mode |
| `h/j/k/l` | Navigate |
| `/` | Search forward |
| `Space` | Start selection |
| `Enter` | Copy selection |
| `Ctrl+b ]` | Paste from tmux buffer |

---

## Recommended tmux + Neovim Workflow

```
1. cd ~/projects/myapp

2. tmux new -s myapp           → start session

3. Window 1 — Editor
   nvim .

4. Ctrl+b c → Window 2 — Terminal
   npm run dev  /  python app.py  /  go run main.go

5. Ctrl+b c → Window 3 — Git
   (lazygit or git commands)

6. Switch windows: Ctrl+b 1 · Ctrl+b 2 · Ctrl+b 3

7. Done for the day:
   Ctrl+b d  → detach (everything keeps running)

8. Come back:
   tmux attach -t myapp
   Space wr  → restore Neovim session
```

---

## Recommended ~/.tmux.conf

```bash
set -g mouse on                  # enable mouse
set -g mode-keys vi              # vi keys in copy mode
set -g history-limit 10000       # longer scroll history
set -g base-index 1              # windows start at 1
setw -g pane-base-index 1        # panes start at 1
set -g renumber-windows on       # renumber on close
```

---

## Quick Reference

```
Prefix         → Ctrl+b
New session    → tmux new -s name
Detach         → Ctrl+b d
Reattach       → tmux attach -t name
New window     → Ctrl+b c
Switch window  → Ctrl+b n/p  or  Ctrl+b 0-9
Split V        → Ctrl+b %
Split H        → Ctrl+b "
Navigate       → Ctrl+h/j/k/l  (works in nvim too)
Zoom pane      → Ctrl+b z
Session list   → Ctrl+b s
Copy mode      → Ctrl+b [
```
