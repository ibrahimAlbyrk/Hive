<div align="center">
  <br>
  <img src=".github/assets/banner.svg" alt="Hive" width="800">
  <br>
  <br>

  <a href="#quick-start"><img src="https://img.shields.io/badge/python-3.12+-f59e0b?style=flat-square&logo=python&logoColor=white&labelColor=0a0a0f" alt="Python 3.12+"></a>
  &nbsp;
  <a href="#requirements"><img src="https://img.shields.io/badge/platform-macOS%20%7C%20Linux-f59e0b?style=flat-square&labelColor=0a0a0f" alt="Platform"></a>
  &nbsp;
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-f59e0b?style=flat-square&labelColor=0a0a0f" alt="License"></a>
  &nbsp;
  <a href="#tech-stack"><img src="https://img.shields.io/badge/built_with-Textual-f59e0b?style=flat-square&labelColor=0a0a0f" alt="Textual"></a>

  <br>
  <br>

  <strong>Stop juggling terminals. See every Claude Code instance on one screen.</strong>

  <br>
  <br>
</div>

<div align="center"><img src=".github/assets/divider.svg" width="400"></div>

<br>

```
╭─ HIVE ──────────────────────────────────────────────────────────────╮
│  ● Projects    ○ Instances    ○ Files                     14:32    │
├───────────────────┬─────────────────────────────────────────────────┤
│                   │                                                 │
│  ▸ api-server     │  api-server                                     │
│  ▸ web-app        │  ├── Path: ~/projects/api                       │
│    mobile-app     │  ├── Instances: 3                               │
│                   │  └── Status: 2 working, 1 idle                  │
│                   │                                                 │
│                   │  Instances                                       │
│                   │  ● main       Working (Edit src/auth.py)        │
│                   │  ● refactor   Working (Bash)                    │
│                   │  ○ tests      Idle                              │
│                   │                                                 │
├───────────────────┴─────────────────────────────────────────────────┤
│  3 projects │ 7 instances │ 2 working │ 1 waiting       [?] Help   │
╰─────────────────────────────────────────────────────────────────────╯
```

<br>

<div align="center"><img src=".github/assets/divider.svg" width="400"></div>

<br>

## Why?

Running multiple Claude Code instances across projects means:

- **Lost in tabs** — Which terminal has which instance? Where's the one fixing auth?
- **Status blindness** — Is Claude thinking, waiting for input, or done? Check every tab to know
- **Subagent black box** — Claude spawned 5 subagents. Where? Doing what?
- **Context tax** — Copying paths, managing `@references`, switching contexts endlessly

Hive unifies everything into one terminal with real-time tracking, embedded terminals, and smart file management.

<br>

<div align="center"><img src=".github/assets/divider.svg" width="400"></div>

<br>

## Features

<table>
<tr>
<td width="50%" valign="top">

### ⬡ Real-Time Status

Hook into Claude Code's lifecycle. See which instances are **working**, **waiting**, **asking questions**, or **idle** — all at a glance.

```
● api-refactor   Working (Edit auth.py)
◉ bug-fix-123    Waiting for input
◉ code-review    Asking question
○ test-runner    Idle
```

</td>
<td width="50%" valign="top">

### ⬡ Embedded Terminals

Full PTY output for each instance, directly in the TUI. Send prompts, read responses. Zero tab switching.

Every terminal preserves ANSI colors, cursor movement, and interactive output — exactly like your native terminal.

</td>
</tr>
<tr>
<td width="50%" valign="top">

### ⬡ Subagent Tracking

Claude spawns subagents? See them. A tree view shows every parent and child with live status indicators and active tool names.

```
● api-refactor
  ├── ● subagent-1  Working (Grep)
  ├── ○ subagent-2  Idle
  └── ● subagent-3  Working (Edit)
```

</td>
<td width="50%" valign="top">

### ⬡ Smart File Management

Browse project files, multi-select with <kbd>Space</kbd>, copy as `@references` with <kbd>Cmd</kbd>+<kbd>C</kbd>. Paste into any Claude instance.

Toggle inline git diffs with <kbd>d</kbd> to see exactly what Claude changed — green for added, red for deleted.

</td>
</tr>
</table>

<br>

### ⬡ Hook-Based Architecture

Zero polling. Claude Code fires hooks, Hive listens via Unix Domain Socket, UI updates reactively.

```
Claude Code hook fires
  → Hook script serializes JSON
    → Unix Domain Socket (~/.hive/hive.sock)
      → StateManager updates instance status
        → Textual reactive UI refreshes
```

<br>

<div align="center"><img src=".github/assets/divider.svg" width="400"></div>

<br>

## Architecture

```
┌──────────────────────────────────────────────┐
│              TUI  (Textual)                  │
├──────────────────────────────────────────────┤
│             State Manager                    │
├────────────────────┬─────────────────────────┤
│   Hook Collector   │   Instance Controller   │
│   (Unix Socket)    │   (PTY Manager)         │
├────────────────────┴─────────────────────────┤
│            Project Registry                  │
├────────────────────┬─────────────────────────┤
│    File Manager    │    Storage (JSON)        │
└────────────────────┴─────────────────────────┘
```

Each Claude Code instance runs in its own PTY process. Hook scripts intercept lifecycle events (`PreToolUse`, `PostToolUse`, `Notification`, `Stop`) and send JSON to Hive's socket. The state manager processes events and triggers reactive UI updates — no polling, no timers.

<br>

<div align="center"><img src=".github/assets/divider.svg" width="400"></div>

<br>

## Quick Start

### Install

```bash
uv tool install hive-cli
```

### Run

```bash
hive
```

### Development

```bash
git clone https://github.com/your-username/hive.git
cd hive
uv sync
uv run hive
```

<br>

<div align="center"><img src=".github/assets/divider.svg" width="400"></div>

<br>

## Keybindings

| Key | Action |
|:----|:-------|
| <kbd>1</kbd> <kbd>2</kbd> <kbd>3</kbd> | Switch tabs (Projects, Instances, Files) |
| <kbd>Tab</kbd> / <kbd>Shift</kbd>+<kbd>Tab</kbd> | Cycle tabs |
| <kbd>n</kbd> | New project / instance |
| <kbd>Enter</kbd> | Select / Open |
| <kbd>Space</kbd> | Multi-select files |
| <kbd>d</kbd> | Toggle diff view |
| <kbd>Cmd</kbd>+<kbd>C</kbd> | Copy `@references` |
| <kbd>s</kbd> | Stop instance |
| <kbd>r</kbd> | Restart instance |
| <kbd>q</kbd> | Quit |

<br>

## Tech Stack

| Component | Technology |
|:----------|:-----------|
| TUI Framework | [Textual](https://textual.textualize.io) |
| Process Management | `asyncio` + `pty` |
| Hook IPC | Unix Domain Socket |
| File Watching | [watchfiles](https://github.com/samuelcolvin/watchfiles) |
| Git Integration | [GitPython](https://github.com/gitpython-developers/GitPython) |
| Package Manager | [uv](https://github.com/astral-sh/uv) |

<br>

## Requirements

- Python 3.12+
- macOS or Linux (PTY + Unix socket)
- 256-color terminal, min 80x24

<br>

## License

[MIT](LICENSE)

<br>

<div align="center">
  <img src=".github/assets/divider.svg" width="400">
  <br>
  <br>
  <sub>Built for developers who refuse to lose track of their AI agents.</sub>
  <br>
  <br>
</div>
