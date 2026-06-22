# Obsidian Guide

> Setup, workflow, plugins, and all shortcuts for using Obsidian directly and via Neovim.

---

## Vault Location

```
~/Documents/Obsidian Vault
```

---

## Folder Structure (PARA)

```
Obsidian Vault/
├── 00-Inbox/          # Dump everything here first, triage weekly
├── 01-Projects/       # Active work with a finish line
├── 02-Areas/
│   ├── engineering/   # Architecture, decisions, tech notes
│   ├── management/    # 1:1s, team notes, leadership
│   └── learning/      # Courses, books, exploration
├── 03-Resources/
│   ├── tech-notes/    # Language & framework references
│   └── snippets/      # Code snippets & patterns
├── 04-Archive/        # Completed projects, old notes
├── Daily/             # Daily notes (YYYY-MM-DD.md)
├── Weekly/            # Weekly reviews
├── Guides/            # This folder
├── Templates/         # Templater templates
└── Attachments/       # Images, PDFs
```

> **Rule:** Nothing lives in Inbox permanently. Weekly — move or delete everything.

---

## Templates

Insert via `Space ot` in Neovim or `Cmd+P` → "insert template" in Obsidian.

| Template | Use for |
|----------|---------|
| `daily.md` | Daily standup, top 3 priorities, notes |
| `weekly.md` | Weekly review — wins, carry-overs, next week |
| `meeting.md` | Meeting agenda, decisions, action items |
| `project.md` | New project kickoff |
| `note.md` | General note |

---

## Community Plugins to Install

Settings → Community Plugins → Browse → search and install:

| Plugin | Purpose |
|--------|---------|
| **Dataview** | Query vault like a database — lists, tables, task views |
| **Templater** | Dynamic templates with dates, prompts, JavaScript |
| **Periodic Notes** | Daily/weekly notes with proper folder routing |
| **Calendar** | Sidebar calendar — click a day to open daily note |
| **Tasks** | Task management with due dates, priorities, recurrence |
| **Obsidian Git** | Auto-commit & push vault to git |
| **Omnisearch** | Much better full-text search |
| **QuickAdd** | Rapid capture via hotkeys |
| **Style Settings** | Customize theme via UI panel |

---

## Theme

Settings → Appearance → Themes → Browse → **Minimal** → Install → Enable

Also install **Style Settings** plugin for color customization.

---

## Plugin Configuration

**Templater:**
- Template folder → `Templates`
- Enable "Trigger on new file creation"
- Enable "Automatic jump to cursor"

**Periodic Notes:**
- Daily → Folder: `Daily` · Template: `Templates/daily.md` · Format: `YYYY-MM-DD`
- Weekly → Folder: `Weekly` · Template: `Templates/weekly.md` · Format: `YYYY-[W]WW`

**Obsidian Git:**
- Auto pull/push interval → `10` minutes

---

## Using Obsidian Directly — App Shortcuts

### The two most important

| Shortcut | Action |
|----------|--------|
| `Cmd+P` | **Command palette** — run ANY action. If you forget a shortcut, open this. |
| `Cmd+O` | **Quick switcher** — jump to any note by typing its name. |

### File & note management

| Shortcut | Action |
|----------|--------|
| `Cmd+N` | New note |
| `Cmd+Shift+N` | New note in new pane |
| `Cmd+W` | Close tab |
| `Cmd+Shift+T` | Reopen last closed tab |
| `F2` | Rename note |
| `Cmd+S` | Save |
| `Cmd+,` | Settings |

Create folder → right-click in File Explorer → New folder
Delete note → right-click → Delete

### Navigation

| Shortcut | Action |
|----------|--------|
| `Cmd+O` | Quick switcher |
| `Cmd+P` | Command palette |
| `Cmd+G` | Graph view |
| `Cmd+Option+←` | Navigate back |
| `Cmd+Option+→` | Navigate forward |
| `Option+Enter` | Follow link under cursor |
| `Cmd+Option+Enter` | Open link in new pane |

### Search

| Shortcut | Action |
|----------|--------|
| `Cmd+F` | Search in current note |
| `Cmd+Option+F` | Find & replace in note |
| `Cmd+Shift+F` | Search entire vault |

### Editing & formatting

| Shortcut | Action |
|----------|--------|
| `Cmd+B` | Bold |
| `Cmd+I` | Italic |
| `Cmd+K` | Insert link (with text selected) |
| `Cmd+/` | Toggle comment |
| `Cmd+E` | Toggle reading / editing mode |
| `Cmd+Enter` | Toggle checkbox done/undone |

### While typing — links, tags, headings

| Type | Result |
|------|--------|
| `[[` | Autocomplete link to any note |
| `[[Note\|Label]]` | Link with custom display text |
| `[[Note#Heading]]` | Link to specific heading |
| `#tagname` | Add tag (hierarchical: `#area/work`) |
| `# ` | Heading 1 |
| `## ` | Heading 2 |
| `### ` | Heading 3 |
| `- [ ] ` | Checkbox / task |
| `---` | Horizontal divider |

> **Tip:** Type `[[New Note Name]]` and click it — Obsidian creates that note instantly.

### Templater

| Action | How |
|--------|-----|
| Insert template | `Cmd+P` → "insert template" |
| New note from template | `Cmd+P` → "create from template" |
| Assign shortcut | Settings → Hotkeys → search "Templater" |

Suggested: bind "Insert template" to `Cmd+Shift+I`

### Tasks plugin

| Action | How |
|--------|-----|
| Toggle done | `Cmd+Enter` |
| Create/edit with GUI | `Cmd+P` → "create or edit task" |

```
- [ ] Normal task
- [ ] Due date 📅 2026-04-01
- [ ] High priority ⏫
- [ ] Recurring 🔁 every week
- [x] Done ✅ 2026-03-28
```

### Calendar plugin

Appears in right sidebar. Dot under date = note exists.

| Action | How |
|--------|-----|
| Open daily note | Click the day |
| Open weekly note | Click week number (left column) |
| Navigate months | `<` / `>` arrows |
| Re-open panel | `Cmd+P` → "Calendar: open view" |

### Graph view (`Cmd+G`)

| Action | How |
|--------|-----|
| Pan | Click and drag |
| Zoom | Scroll wheel |
| Open note | Click its node |
| See connections | Hover over node |
| Filter | Cog → search bar |
| Local graph | `Cmd+P` → "local graph" |

---

## Neovim Integration (obsidian.nvim)

Config: `~/.config/nvim/lua/sabir/plugins/obsidian.lua`

| Key | Action |
|-----|--------|
| `Space od` | Today's daily note |
| `Space oy` | Yesterday's note |
| `Space of` | Find note (fuzzy) |
| `Space os` | Search text in vault |
| `Space on` | New note (goes to Inbox) |
| `Space ot` | Insert template |
| `Space ob` | Backlinks (what links here) |
| `Space ol` | Outbound links |
| `Space or` | Rename note + update backlinks |
| `Space ox` | Toggle checkbox |
| `Space oo` | Open in Obsidian app |
| `Space oe` | Extract selection to new note (Visual) |
| `gf` | Follow `[[link]]` under cursor |
| Type `[[` | Autocomplete wikilinks |
| Type `#` | Autocomplete tags |

---

## Dataview Examples

Paste inside any note (requires Dataview plugin):

**Active projects:**
```dataview
TABLE status, file.mtime as "Updated"
FROM "01-Projects"
WHERE type = "project" AND status = "active"
SORT file.mtime DESC
```

**All meeting notes:**
```dataview
LIST FROM #meeting SORT file.day DESC LIMIT 10
```

**Incomplete tasks across vault:**
```dataview
TASK WHERE !completed SORT file.mtime DESC
```

**Recent notes (last 7 days):**
```dataview
LIST FROM ""
WHERE file.mtime >= date(today) - dur(7 days)
SORT file.mtime DESC
```

---

## Daily Workflow

| When | Action |
|------|--------|
| Morning | `Space od` → daily note → fill standup + top 3 |
| During day | Capture notes, meetings, decisions inline |
| End of day | Energy level + reflection |
| Weekly (Friday) | Create weekly note → review → clear Inbox |

---

## Tips

- **Link everything** — wrap projects, people, concepts in `[[]]`. Builds your knowledge graph.
- **Tags vs folders** — folders for PARA structure, tags for cross-cutting: `#meeting` `#decision` `#bug`
- **Don't over-organize** — drop in Inbox first, sort during weekly review
- **Dataview is your dashboard** — `Home.md` queries your whole vault live

---

## Full Shortcut Cheat Sheet

```
Cmd+P          → Command palette
Cmd+O          → Quick switcher
Cmd+N          → New note
Cmd+G          → Graph view
Cmd+F          → Search in note
Cmd+Shift+F    → Search vault
Cmd+B          → Bold
Cmd+I          → Italic
Cmd+K          → Insert link
Cmd+E          → Toggle preview/edit
Cmd+Enter      → Toggle checkbox
Cmd+W          → Close tab
Cmd+,          → Settings
Cmd+Option+←   → Back
Cmd+Option+→   → Forward
Option+Enter   → Follow link
F2             → Rename note
[[             → Link to another note
#              → Add tag
```
