---
created: 2026-06-22
type: reference
tags: [obsidian, setup]
---

# 🔌 Plugin Checklist

> How to install community plugins: **Settings → Community plugins → Turn on community plugins → Browse →** search the name → **Install → Enable**.
> ⚠️ Keep total plugins under ~20 for snappy startup.

## ⭐ The core stack

- [x] **Dataview** — query notes like a database (live tables/lists from metadata)
- [x] **Templater** — supercharged templates with JS, prompts, auto-dates ⚙️ *needs config (below)*
- [ ] **Obsidian Git** — auto-commit the vault to GitHub on a timer (version history + backup) ← only one missing
- [x] **Tasks** — real task management: due dates, recurring, priorities, queries
- [x] **QuickAdd** — one-hotkey capture & macros from anywhere

## 🛠️ Engineer power tools

- [x] **Excalidraw** — hand-drawn diagrams & architecture sketches inside notes
- [x] **Advanced URI** — drive Obsidian from scripts/shortcuts via URLs
- [x] **Terminal** — embedded shell inside Obsidian
- [x] **Style Settings** — UI knobs for themes/snippets

## ⚙️ Required config

**Templater** (so `<% %>` in your templates actually runs):
1. Settings → Templater → set **Template folder location** = `Templates`
2. Turn ON **Trigger Templater on new file creation**
3. (Optional) **Folder Templates**: map `Daily` → `Templates/daily`, `01-Projects` → `Templates/project` so new notes auto-fill

**Tasks**: works out of the box — write `- [ ] thing 📅 2026-07-01 🔁 every week`.

**QuickAdd**: add a "Capture" choice → target `00-Inbox`, bind a hotkey.

## 🧩 Native (no plugin — already on)

- [x] **Bases** — database views from note properties (used in [[Home]])
- [x] **Canvas** — infinite whiteboard linking live notes
- [x] **Properties / Backlinks / Outline / Bookmarks**

---

## 🤖 Claude + Obsidian — ✅ DONE (2026-06-22)

Claude can now read & write this vault natively via MCP. Setup used:

- [x] Installed **Local REST API with MCP** (by Adam Coddington)
- [x] Enabled the **non-encrypted HTTP server** (loopback-only, `127.0.0.1:27123` — safe; still token-protected)
- [x] Registered the MCP server with Claude Code (user scope):
  ```
  claude mcp add --scope user --transport http obsidian \
    http://127.0.0.1:27123/mcp/ --header "Authorization: Bearer <API-KEY>"
  ```
- [x] Verified: `claude mcp list` → `obsidian … ✔ Connected`

> **Restart Claude Code** for the obsidian tools to load in a session.
> The API key lives in `~/.claude.json` (not in this vault). If you ever rotate it
> in the plugin, re-run the `claude mcp add` command with the new key.

### Optional next level — second-brain skill packs
- `obsidian-second-brain` (cross-CLI, 40+ commands)
- `claude-obsidian` (self-organizing knowledge graph)
Drop into `~/.claude/` per their GitHub README.

> Once loaded, Claude can run a **morning briefing**, turn meeting notes into action
> items, auto-link notes, and file new captures for you.

---

## ✅ After installing

- [ ] Set hotkeys you'll actually use (`Cmd+P` → search "hotkeys")
- [ ] Templater: point it at the `Templates/` folder
- [ ] Obsidian Git: create a private GitHub repo per vault, set auto-commit interval
- [ ] Re-open [[Home]] — the Projects base should be live
