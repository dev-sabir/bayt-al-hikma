# Neovim Guide

> Personal reference. Leader key = `Space`. Escape = `jk`.

---

## Modes

| Mode | Enter | Exit |
|------|-------|------|
| **Normal** | Default (home base) | Already here |
| **Insert** | `i` `a` `o` `I` `A` `O` | `jk` or `Esc` |
| **Visual** | `v` char · `V` line · `Ctrl+v` block | `jk` or `Esc` |
| **Command** | `:` | `Enter` to run · `Esc` to cancel |

> Status bar color: blue = Normal, green = Insert, purple = Visual

### Insert mode entry keys

| Key | Where cursor goes |
|-----|------------------|
| `i` | Before current character |
| `a` | After current character |
| `I` | Beginning of line |
| `A` | End of line |
| `o` | New line below |
| `O` | New line above |
| `gi` | Where you last stopped typing |

---

## Movement

### Basic

| Key | Action |
|-----|--------|
| `h j k l` | Left / down / up / right |
| `w` | Start of next word |
| `b` | Start of previous word |
| `e` | End of current/next word |
| `0` | Start of line |
| `^` | First non-blank character |
| `$` | End of line |
| `gg` | Top of file |
| `G` | Bottom of file |
| `50G` | Go to line 50 |
| `%` | Jump to matching bracket |

### Scrolling

| Key | Action |
|-----|--------|
| `Ctrl+d` | Half page down |
| `Ctrl+u` | Half page up |
| `Ctrl+f` | Full page down |
| `Ctrl+b` | Full page up |
| `zz` | Center current line |
| `zt` | Current line to top |
| `zb` | Current line to bottom |

### Jump history

| Key | Action |
|-----|--------|
| `Ctrl+o` | Jump back (use after `gd`) |
| `Ctrl+i` | Jump forward |
| `''` | Jump to last position |

### Within-line

| Key | Action |
|-----|--------|
| `fx` | Jump forward to char x |
| `Fx` | Jump backward to char x |
| `tx` | Jump to just before char x |
| `;` | Repeat last f/F/t jump |
| `,` | Repeat in reverse |

### Treesitter jumps

| Key | Action |
|-----|--------|
| `]m` / `[m` | Next / prev function start |
| `]M` / `[M` | Next / prev function end |
| `]c` / `[c` | Next / prev class |
| `]i` / `[i` | Next / prev conditional |
| `]l` / `[l` | Next / prev loop |

---

## Editing

### Operator + motion formula

```
[operator] [motion or text object]

d w    → delete word
c i "  → change inside quotes
y i p  → copy paragraph
v a {  → select including braces
```

| Operator | Action |
|----------|--------|
| `d` | Delete (cut) |
| `y` | Yank (copy) |
| `c` | Change (delete + insert) |
| `>` | Indent right |
| `<` | Indent left |
| `=` | Auto-indent |
| `gu` | Lowercase |
| `gU` | Uppercase |

### Text objects

| Object | Selects |
|--------|---------|
| `iw` / `aw` | Word / word + space |
| `i"` / `a"` | Inside / around double quotes |
| `i'` / `a'` | Inside / around single quotes |
| `i(` / `a(` | Inside / around parentheses |
| `i{` / `a{` | Inside / around curly braces |
| `i[` / `a[` | Inside / around square brackets |
| `it` / `at` | Inside / around HTML tag |
| `ip` / `ap` | Paragraph |
| `im` / `am` | Method/function (treesitter) |
| `ic` / `ac` | Class (treesitter) |
| `ia` / `aa` | Function argument (treesitter) |

> **Examples:** `ciw` replace word · `di"` delete inside quotes · `cam` change entire function

### Quick edits

| Key | Action |
|-----|--------|
| `dd` | Delete line |
| `yy` | Copy line |
| `cc` | Replace line |
| `D` | Delete to end of line |
| `C` | Change to end of line |
| `x` | Delete character |
| `r` | Replace single character |
| `J` | Join line with line below |
| `>>` / `<<` | Indent / dedent line |
| `u` | Undo |
| `Ctrl+r` | Redo |
| `.` | Repeat last change |
| `Space +` | Increment number |
| `Space -` | Decrement number |

### Commenting

| Key | Action |
|-----|--------|
| `gcc` | Toggle comment on line |
| `gc` + motion | Toggle comment on motion |
| `gc` (Visual) | Toggle comment on selection |

### Surround

| Key | Action |
|-----|--------|
| `ysiw"` | Wrap word in double quotes |
| `cs"'` | Change `"` to `'` |
| `ds"` | Delete surrounding quotes |
| `S"` (Visual) | Surround selection |

### Incremental selection

| Key | Action |
|-----|--------|
| `Ctrl+Space` | Expand selection (word → expression → function → class) |
| `Backspace` | Shrink selection |

---

## Copy, Cut & Paste

> Your setup has `clipboard = unnamedplus` — Neovim clipboard IS your system clipboard.

| Key | Action |
|-----|--------|
| `yy` | Copy line |
| `y` + motion | Copy by motion |
| `p` | Paste after / below |
| `P` | Paste before / above |
| `dd` | Cut line |
| `d` + motion | Cut by motion |

### Visual mode

| Key | Action |
|-----|--------|
| `v` | Character visual |
| `V` | Line visual |
| `Ctrl+v` | Block/column visual |
| `gv` | Re-select last selection |

> **Column editing:** `Ctrl+v` → select lines → `I` → type → `Esc`

---

## Search

### In file

| Key | Action |
|-----|--------|
| `/word` + `Enter` | Search forward |
| `?word` + `Enter` | Search backward |
| `n` | Next match |
| `N` | Previous match |
| `*` | Search word under cursor |
| `#` | Search word backward |
| `Space nh` | Clear highlights |

### In file — find & replace

```vim
:%s/old/new/g     → replace all
:%s/old/new/gc    → replace with confirmation
:s/old/new/g      → current line only
```

### Project-wide (Telescope)

| Key | Action |
|-----|--------|
| `Space fs` | Live grep — search text in all files |
| `Space fc` | Search word under cursor |
| `Space ff` | Find file by name |
| `Space fr` | Recent files |
| `Space ft` | Find TODO/FIXME comments |

### Flash — jump anywhere

| Key | Action |
|-----|--------|
| `s` | Flash jump — type 2 chars, pick label |
| `S` | Flash treesitter node select |
| `Ctrl+s` | Toggle flash in `/` search |

---

## Buffers, Splits & Tabs

### Buffers

| Key | Action |
|-----|--------|
| `:e filename` | Open file |
| `:ls` | List open buffers |
| `:bn` / `:bp` | Next / prev buffer |
| `Ctrl+^` | Toggle last buffer |
| `:bd` | Close buffer |

### Splits

| Key | Action |
|-----|--------|
| `Space sv` | Split vertical |
| `Space sh` | Split horizontal |
| `Space se` | Equalize splits |
| `Space sx` | Close split |
| `Space sm` | Maximize / minimize split |
| `Ctrl+h/j/k/l` | Navigate between splits |

### Tabs

| Key | Action |
|-----|--------|
| `Space to` | New tab |
| `Space tx` | Close tab |
| `Space tn` | Next tab |
| `Space tp` | Previous tab |
| `Space tf` | Current buffer in new tab |

### Sessions

| Key | Action |
|-----|--------|
| `Space ws` | Save session |
| `Space wr` | Restore session |

---

## Saving & Quitting

| Command | Action |
|---------|--------|
| `:w` | Save |
| `:q` | Quit |
| `:wq` | Save and quit |
| `:q!` | Quit without saving |
| `:qa` | Quit all |
| `:qa!` | Quit all without saving |

---

## File Explorer — nvim-tree

| Key | Action |
|-----|--------|
| `Space ee` | Toggle file tree |
| `Space ef` | Focus tree on current file |
| `Space ec` | Collapse all folders |
| `Space er` | Refresh tree |

### Inside the tree

| Key | Action |
|-----|--------|
| `j` / `k` | Move down / up |
| `Enter` / `o` | Open file / expand folder |
| `h` | Collapse folder |
| `l` | Expand / open |
| `H` | Toggle hidden files |
| `R` | Refresh |
| `W` | Collapse all |
| `q` | Close tree |
| `g?` | Show all keymaps |

### Open files

| Key | Action |
|-----|--------|
| `Enter` | Open in current window |
| `Tab` | Preview (keep focus in tree) |
| `Ctrl+v` | Open in vertical split |
| `Ctrl+h` | Open in horizontal split |
| `Ctrl+t` | Open in new tab |

### File operations

| Key | Action |
|-----|--------|
| `a` | Create file (end with `/` for folder) |
| `r` | Rename |
| `d` | Delete |
| `x` | Cut |
| `c` | Copy |
| `p` | Paste |
| `y` | Copy filename |
| `Y` | Copy relative path |
| `gy` | Copy absolute path |

---

## Telescope — Fuzzy Finder

| Key | Action |
|-----|--------|
| `Space ff` | Find files |
| `Space fr` | Recent files |
| `Space fs` | Live grep |
| `Space fc` | Find word under cursor |
| `Space ft` | Find TODOs |

### Inside Telescope

| Key | Action |
|-----|--------|
| `Ctrl+j` / `Ctrl+k` | Navigate results |
| `Enter` | Open file |
| `Ctrl+v` | Open in vertical split |
| `Ctrl+x` | Open in horizontal split |
| `Ctrl+t` | Open in new tab |
| `Ctrl+q` | Send to Trouble quickfix |
| `Ctrl+u` / `Ctrl+d` | Scroll preview |
| `Esc` | Close |

---

## LSP — Code Intelligence

### Navigation

| Key | Action |
|-----|--------|
| `gd` | Go to definition |
| `gD` | Go to declaration |
| `gi` | Go to implementation |
| `gt` | Go to type definition |
| `gR` | Show all references |
| `Ctrl+o` | Jump back |

### Docs & info

| Key | Action |
|-----|--------|
| `K` | Hover documentation |
| `Space d` | Line diagnostics |
| `Space D` | File diagnostics (Telescope) |
| `[d` / `]d` | Prev / next diagnostic |

### Code actions

| Key | Action |
|-----|--------|
| `Space ca` | Code actions |
| `Space rn` | Rename symbol (all files) |
| `Space mp` | Format file |
| `Space rs` | Restart LSP |

> **Workflow:** `K` to read docs → `gd` to see implementation → `Ctrl+o` to come back

---

## Autocompletion

| Key | Action |
|-----|--------|
| `Ctrl+j` | Next completion item |
| `Ctrl+k` | Previous completion item |
| `Ctrl+Space` | Trigger completion |
| `Enter` | Confirm selection |
| `Ctrl+e` | Close menu |
| `Ctrl+b` / `Ctrl+f` | Scroll docs |
| `Tab` | Expand snippet / next field |
| `Shift+Tab` | Previous snippet field |

---

## Git

### Lazygit

| Key | Action |
|-----|--------|
| `Space lg` | Open Lazygit full UI |

> Inside Lazygit: `?` for help · `q` to close

### Gitsigns (inline)

| Key | Action |
|-----|--------|
| `]h` / `[h` | Next / prev changed hunk |
| `Space hs` | Stage hunk |
| `Space hr` | Reset hunk |
| `Space hS` | Stage entire buffer |
| `Space hR` | Reset entire buffer |
| `Space hu` | Undo stage |
| `Space hp` | Preview hunk diff |
| `Space hb` | Blame current line |
| `Space hB` | Toggle blame for all lines |
| `Space hd` | Diff file against HEAD |

---

## Trouble — Diagnostics Panel

| Key | Action |
|-----|--------|
| `Space xw` | Workspace diagnostics |
| `Space xd` | Document diagnostics |
| `Space xq` | Quickfix list |
| `Space xl` | Location list |
| `Space xt` | All TODOs in project |
| `]t` / `[t` | Next / prev TODO |
| `Space l` | Trigger linting |

---

## Obsidian (obsidian.nvim)

| Key | Action |
|-----|--------|
| `Space od` | Today's daily note |
| `Space oy` | Yesterday's note |
| `Space of` | Find note |
| `Space os` | Search vault |
| `Space on` | New note |
| `Space ot` | Insert template |
| `Space ob` | Backlinks |
| `Space ol` | Outbound links |
| `Space or` | Rename note |
| `Space ox` | Toggle checkbox |
| `Space oo` | Open in Obsidian app |
| `Space oe` | Extract to new note (Visual) |
| `gf` on `[[link]]` | Follow link |
| Type `[[` | Autocomplete wikilinks |

---

## Markdown

| Key | Action |
|-----|--------|
| `:Markview` | Toggle inline rendering |
| `Space ms` | Start browser preview |
| `Space mx` | Stop browser preview |

---

## Plugin Management

| Command | Action |
|---------|--------|
| `:Lazy` | Open plugin manager |
| `:Lazy sync` | Install / update all plugins |
| `:Mason` | Open LSP/tool manager |
| `:checkhealth` | Check Neovim health |
| `Space ?` | Show all keymaps (which-key) |
