# Claude Code Manager

A lightweight, single-file browser tool for browsing, previewing, and importing [Claude Code](https://docs.anthropic.com/en/docs/claude-code) skills and agents into your projects.

> No installation. No server. No dependencies. Just open `claude-manager.html` in Chrome or Edge.

---

## Features

- **Skills & Agents tabs** — switch between managing `/commands` skills and `@agents` in one interface
- **Full SKILL.md preview** — rendered markdown with syntax highlighting for code blocks
- **Agent frontmatter display** — shows `name`, `description`, `model`, `tools` and full system prompt
- **Imported status** — scans your destination directory and marks already-imported items with a green badge
- **Overwrite protection** — confirms before overwriting existing files
- **Search & multi-select** — filter by name, select individual items or all at once
- **Persistent directories** — remembers your last source and destination folders across sessions (IndexedDB)
- **Universal compatibility** — works with any skills collection, not just one specific repository

---

## Usage

### Requirements

- Chrome 86+ or Edge 86+ (requires [File System Access API](https://developer.mozilla.org/en-US/docs/Web/API/File_System_API))
- Firefox is not supported (Mozilla has not implemented this API)

### Getting started

1. Download `claude-manager.html`
2. Open it in Chrome or Edge (double-click or drag into browser)
3. Click **Browse…** next to **Source** and select your skills/agents repository folder
4. Switch between **Skills** and **Agents** tabs as needed
5. Click any item to preview its content on the right
6. Check the items you want to import
7. Click **Browse…** next to **Import to** and select your destination folder
8. Click **Import Selected**

### Destination directories

| Tab | Destination |
|-----|-------------|
| Skills | `.claude/commands/` (project) or `~/.claude/commands/` (global) |
| Agents | `.claude/agents/` (project) or `~/.claude/agents/` (global) |

> Skills are imported as `skill-name.md` and called with `/skill-name` in Claude Code.  
> Agents are imported as `agent-name.md` and invoked with `@agent-name` in Claude Code.

---

## Compatible Skills Collections

Any repository that stores skills as subdirectories containing a `SKILL.md` file is supported. A few well-known collections:

| Repository | Description |
|------------|-------------|
| [levnikolaevich/claude-code-skills](https://github.com/levnikolaevich/claude-code-skills) | 116 production-ready skills covering the full Agile delivery workflow |
| [garrytan/gstack](https://github.com/garrytan/gstack) | Garry Tan's (YC CEO) opinionated software factory with 20 role-based skills |
| [obra/superpowers](https://github.com/obra/superpowers) | TDD-focused skills with automatic triggering, 93k stars |

Agent repositories follow the same pattern: any `.md` file with a YAML frontmatter block containing `name` or `description` is recognized as an agent.

---

## How it works

**Skills** are detected by scanning subdirectories for a `SKILL.md` file. The directory name is used to derive the command name (the `ln-NNN-` prefix is stripped automatically for levnikolaevich-style repositories).

**Agents** are detected by scanning for `.md` files — either at the top level or inside subdirectories — that contain a YAML frontmatter block (`---`) with at least a `name` or `description` field.

**Imported status** is determined by scanning the destination directory for existing `.md` files and comparing names. Items already present are shown with an `imported` badge and dimmed name.

---

## Screenshot

> *(Add a screenshot here after first use)*

---

## Contributing

Pull requests are welcome. Some ideas for improvement:

- Dark/light theme toggle
- Batch update: re-import all previously imported items in one click
- Side-by-side diff view when overwriting an existing skill
- Support for reading skills directly from a GitHub repository URL

---

## License

MIT — free to use, modify, and distribute.
