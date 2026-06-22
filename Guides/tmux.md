# tmux Guide

> Terminal multiplexer — multiple sessions, windows, and panes in one terminal.
> Keeps everything running even when you close the terminal or your SSH drops.
>
> **This doc matches my actual `~/.tmux.conf`.** Prefix is remapped to **`Ctrl+a`** (not the default `Ctrl+b`), splits are `|` and `-`, and I run TPM with resurrect + continuum + tokyo-night.

---

## Mental Model

```
tmux server                 (one background process for everything)
  └── Session   work · api · vault      ← one per project
        └── Window   editor · server · git   ← like tabs
              └── Pane   nvim | logs | shell  ← splits inside a tab
```

- **Detach** a session and it keeps running in the background — reboot-safe with continuum.
- One **session per project** is the workflow. Windows are tabs, panes are splits.

---

## Prefix Key

> Everything starts with the prefix: **`Ctrl+a`**
> Press and *release* `Ctrl+a`, then press the next key.

```
unbind C-b
set -g prefix C-a
bind C-a send-prefix   # press Ctrl+a twice to send a literal Ctrl+a to the app inside
```

Throughout this doc, `prefix` means `Ctrl+a`.

---

## Starting & Managing Sessions (from the shell)

| Command | Action |
|---------|--------|
| `tmux` | New unnamed session |
| `tmux new -s work` | New **named** session |
| `tmux ls` | List all sessions |
| `tmux attach` | Re-attach to last session |
| `tmux attach -t work` | Re-attach to named session |
| `tmux a -t work` | Same, short form |
| `tmux kill-session -t work` | Kill one session |
| `tmux kill-server` | Kill everything |

> **My habit:** `tmux new -s <project>`, work, `prefix d` to detach, `tmux a -t <project>` to come back. Nothing is lost.

---

## Sessions (inside tmux)

| Key | Action |
|-----|--------|
| `prefix d` | Detach (session keeps running) |
| `prefix s` | Interactive session list (jump between) |
| `prefix $` | Rename current session |
| `prefix (` | Previous session |
| `prefix )` | Next session |

### My custom binding

| Key | Action | What it does |
|-----|--------|--------------|
| `prefix M-c` | Attach to current pane's path | `attach-session -c "#{pane_current_path}"` — sets the session's default dir to wherever the current pane is, so new windows/panes open there |

> `M-c` = **Alt+c**. Handy after you've `cd`'d deep into a project: run it so every new split starts in that directory.

---

## Windows (tabs)

| Key | Action |
|-----|--------|
| `prefix c` | New window |
| `prefix ,` | Rename window |
| `prefix &` | Close window (asks to confirm) |
| `prefix n` | Next window |
| `prefix p` | Previous window |
| `prefix 0–9` | Jump to window by number |
| `prefix w` | Window/session picker with preview |
| `prefix f` | Find window by name |

---

## Panes (splits) — my custom binds

> I rebound the split keys to be intuitive: **`|` looks like a vertical divider, `-` looks like a horizontal one.**

| Key | Action | Config |
|-----|--------|--------|
| `prefix \|` | Split **vertically** (left \| right) | `bind \| split-window -h` |
| `prefix -` | Split **horizontally** (top / bottom) | `bind - split-window -v` |
| `prefix x` | Close current pane (confirm) | default |
| `prefix z` | Zoom pane fullscreen / unzoom | default |
| `prefix m` | **Zoom toggle** (my alias, repeatable) | `bind -r m resize-pane -Z` |
| `prefix o` | Cycle to next pane | default |
| `prefix q` | Show pane numbers (press number to jump) | default |
| `prefix !` | Break pane out into its own window | default |
| `prefix {` / `}` | Swap pane with prev / next | default |
| `prefix Space` | Cycle through layout presets | default |

> Both `prefix z` and `prefix m` zoom — `m` is the muscle-memory alias and is `-r` (repeatable, no need to re-press prefix).

### Navigating panes — vim-tmux-navigator

> Plugin `christoomey/vim-tmux-navigator`. **No prefix needed.** These keys move seamlessly between tmux panes *and* Neovim splits as if they were one grid.

| Key | Action |
|-----|--------|
| `Ctrl+h` | Move left |
| `Ctrl+j` | Move down |
| `Ctrl+k` | Move up |
| `Ctrl+l` | Move right |
| `Ctrl+\` | Move to previously active pane |

> This is the killer feature: jump from a Neovim split straight into your tmux terminal pane with the same `Ctrl+h/j/k/l` — no thinking about which program you're in.

### Resizing panes — my custom binds

> These **do** need the prefix (they reuse `h/j/k/l`, which Ctrl-versions are taken by the navigator).

| Key | Action | Config |
|-----|--------|--------|
| `prefix h` | Shrink left (−5) | `resize-pane -L 5` |
| `prefix j` | Grow down (+5) | `resize-pane -D 5` |
| `prefix k` | Grow up (+5) | `resize-pane -U 5` |
| `prefix l` | Grow right (+5) | `resize-pane -R 5` |

> Mnemonic: same `hjkl` directions as movement, just held behind the prefix. Tap repeatedly to keep resizing.

---

## Copy Mode (scroll + select like vim)

> `mode-keys vi` is set, so copy mode uses vim motions. Selection/copy keys are customized.

| Key | Action | Config |
|-----|--------|--------|
| `prefix [` | Enter copy mode | default |
| `q` | Exit copy mode | default |
| `h j k l` | Move around | vi |
| `/` then text | Search forward | vi |
| `?` then text | Search backward | vi |
| `n` / `N` | Next / previous match | vi |
| `v` | **Start** selection | `bind -T copy-mode-vi v send -X begin-selection` |
| `y` | **Copy** selection (and exit) | `bind -T copy-mode-vi y send -X copy-selection` |
| `prefix ]` | Paste tmux buffer | default |

> Mouse is on (`set -g mouse on`), so you can also scroll with the wheel and drag to select — and I unbound `MouseDragEnd1Pane` so **dragging the mouse no longer kicks you out of copy mode** mid-selection.

---

## Plugins (TPM)

> Plugins are managed by **TPM** (Tmux Plugin Manager). The init line lives at the very bottom of the config:
> `run '~/.tmux/plugins/tpm/tpm'`

| Plugin | What it gives me |
|--------|------------------|
| `tmux-plugins/tpm` | The plugin manager itself |
| `christoomey/vim-tmux-navigator` | Seamless `Ctrl+hjkl` between tmux + Neovim |
| `tmux-plugins/tmux-resurrect` | Save/restore sessions, windows, panes manually |
| `tmux-plugins/tmux-continuum` | Auto-saves every 15 min + auto-restores on boot |
| `fabioluciano/tmux-tokyo-night` | The Tokyo Night status bar theme |

### First-time setup (do this once)

```bash
# 1. Install TPM itself
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm

# 2. Start tmux, then INSTALL the plugins listed in the config:
#    press  prefix + I   (capital i)
```

### TPM keybindings

| Key | Action |
|-----|--------|
| `prefix I` | **Install** new plugins from the config |
| `prefix U` | **Update** all plugins |
| `prefix Alt+u` | Uninstall plugins removed from the config |

### Sessions persistence (resurrect + continuum)

> My config: `@resurrect-capture-pane-contents on` and `@continuum-restore on`.
> That means **pane contents are saved too**, and sessions auto-restore when tmux starts after a reboot.

| Key | Action |
|-----|--------|
| `prefix Ctrl+s` | Manually **save** the environment (resurrect) |
| `prefix Ctrl+r` | Manually **restore** the environment (resurrect) |

> With continuum on, you rarely need these manually — it snapshots every 15 minutes and restores automatically. They're the panic buttons.

---

## Reloading the Config

> I rebound `r` to source the config — no need to restart tmux.

| Key | Action | Config |
|-----|--------|--------|
| `prefix r` | Reload `~/.tmux.conf` | `bind r source-file ~/.tmux.conf` |

> Workflow: edit `~/.tmux.conf` → `prefix r` → changes live instantly. (If you added a *new plugin*, also run `prefix I` to install it.)

---

## What Else My Config Sets

```bash
set -g default-terminal "tmux-256color"
set -ag terminal-overrides ",xterm-256color:RGB"   # true-color (24-bit) support
set -g mouse on                                     # scroll + click + drag-select
set-window-option -g mode-keys vi                   # vim keys in copy mode
set -sg escape-time 10                              # near-instant ESC in Neovim (no lag)
```

> `escape-time 10` is the small-but-critical one: the default delay makes `Esc` feel sluggish inside Neovim. 10ms fixes it without breaking escape sequences.

---

## My Daily Workflow

```
1. cd ~/projects/myapp

2. tmux new -s myapp              → start the project session

3. Window 1 — Editor
   nvim .

4. prefix |                       → split, run a dev server on the right
   npm run dev  /  go run .  /  python app.py

5. prefix c → Window 2 — Git
   lazygit

6. Move around WITHOUT prefix:
   Ctrl+h/j/k/l   (flows straight into Neovim splits too)

7. Need space? prefix m           → zoom the focused pane fullscreen
   prefix m again                 → back to the split layout

8. Done for the day:
   prefix d                       → detach, everything keeps running

9. Reboot happens → continuum auto-restores the whole session

10. Back in:
    tmux a -t myapp
```

---

## Quick Reference

```
Prefix            → Ctrl+a
New session       → tmux new -s name
Attach            → tmux a -t name
Detach            → prefix d
Session switcher  → prefix s

New window        → prefix c
Switch window     → prefix n/p  or  prefix 0-9
Rename window     → prefix ,

Split vertical    → prefix |
Split horizontal  → prefix -
Navigate panes    → Ctrl+h/j/k/l   (no prefix, works in nvim)
Resize panes      → prefix h/j/k/l
Zoom pane         → prefix m  (or prefix z)
Close pane        → prefix x

Copy mode         → prefix [   (v select, y copy, q quit)
Paste             → prefix ]

Reload config     → prefix r
Install plugins   → prefix I
Update plugins    → prefix U
Save / restore    → prefix Ctrl+s / prefix Ctrl+r
```

---

## Troubleshooting

| Problem | Fix |
|---------|-----|
| `Ctrl+a` does nothing | Wrong prefix in muscle memory? It's **a**, not **b**. Reload with `prefix r`. |
| Plugins not working | Run `prefix I` to install. Check TPM exists: `ls ~/.tmux/plugins/tpm`. |
| `Ctrl+hjkl` not jumping to Neovim | The vim-tmux-navigator plugin must be installed **on the Neovim side too** (`christoomey/vim-tmux-navigator`). |
| Colors look washed out | The `RGB` terminal-override needs a true-color terminal (Ghostty/Kitty/WezTerm/iTerm2 — all fine). |
| Session didn't restore after reboot | continuum restores on the *first tmux server start*. Start it once with plain `tmux` and wait a moment. |
| Sending a literal `Ctrl+a` to an app (e.g. shell start-of-line) | Press `Ctrl+a` **twice**. |

---

> Related: [[neovim]] · [[obsidian]]
