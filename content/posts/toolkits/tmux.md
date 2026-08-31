+++
title = 'Tmux'
date = 2026-08-31T15:22:05Z
tags = ["tmux", "terminal", "utility", "toolkit"]
author = "Aum Pauskar"
showToc = true
TocOpen = false
draft = false
hidemeta = false
comments = false
description = "A simple handbook on tmux a terminal uitility and multiplexer program"
disableShare = false
disableHLJS = false
hideSummary = false
searchHidden = true
ShowReadingTime = true
ShowBreadCrumbs = true
ShowPostNavLinks = true
ShowWordCount = true
ShowRssButtonInSectionTermList = true
UseHugoToc = true
[editPost]
    URL = "https://github.com/AumPauskar/blog/blob/main/content"
    Text = "Suggest Changes"
    appendFilePath = true
+++


# Tmux?

`tmux` is a terminal multiplexer that enables you to create, access, and control multiple terminal sessions from a single screen. Key advantages include:

* **Session Persistence:** Detach from a session and re-attach later, preserving running processes even if your SSH connection drops.
* **Window & Pane Management:** Divide your terminal into multiple windows (tabs) and panes (splits).
* **Scriptability:** Automate terminal layouts and development environments.

---

## Installation

Install tmux using your distribution's native package manager:

### Debian / Ubuntu / Linux Mint
```bash
sudo apt update
sudo apt install tmux -y

```

### Fedora / RHEL / CentOS

```bash
# Fedora
sudo dnf install tmux -y

# RHEL / CentOS (8+)
sudo dnf install tmux -y

# Older RHEL/CentOS
sudo yum install tmux -y

```

### Arch Linux / Manjaro

```bash
sudo pacman -S tmux

```



## Basic Concepts & Usage Flow

A tmux hierarchy consists of three levels:

1. **Server / Session:** A collection of windows managed by the background daemon.
2. **Window:** A single screen within a session (like a browser tab).
3. **Pane:** A subdivided section within a window (vertical or horizontal split).

```
+-------------------------------------------------------------+
| Session: "dev"                                              |
| +-------------------------+ +-----------------------------+ |
| | Window 0: "editor"      | | Window 1: "logs"            | |
| | +-----------+---------+ | | +-------------------------+ | |
| | | Pane 0    | Pane 1  | | | | Pane 0                  | | |
| | | (nvim)    | (htop)  | | | | (tail -f server.log)    | | |
| | +-----------+---------+ | | +-------------------------+ | |
| +-------------------------+ +-----------------------------+ |
+-------------------------------------------------------------+

```

### Command Line Workflow

| Action | Command |
| --- | --- |
| **Start a new unnamed session** | `tmux` |
| **Start a named session** | `tmux new -s <session-name>` |
| **List active sessions** | `tmux ls` |
| **Attach to last session** | `tmux a` or `tmux attach` |
| **Attach to named session** | `tmux a -t <session-name>` |
| **Detach from current session** | Press `Ctrl+b` then `d` |
| **Kill a specific session** | `tmux kill-session -t <session-name>` |
| **Kill all tmux sessions** | `tmux kill-server` |


## Default Hotkeys Quick Reference

All tmux default shortcuts start with the **Prefix key**: `Ctrl+b` (written as `Prefix`).

### Session Control

* `Prefix` `d` : Detach from current session.
* `Prefix` `s` : Interactively select/switch session.
* `Prefix` `$` : Rename current session.
* `Prefix` `(` / `)` : Switch to previous / next session.

### Window Management

* `Prefix` `c` : Create a new window.
* `Prefix` `,` : Rename current window.
* `Prefix` `w` : List and select windows/sessions interactively.
* `Prefix` `n` : Go to **next** window.
* `Prefix` `p` : Go to **previous** window.
* `Prefix` `0`..`9` : Switch to window by index number.
* `Prefix` `&` : Kill current window.

### Pane Management

* `Prefix` `%` : Split pane **vertically** (left | right).
* `Prefix` `"` : Split pane **horizontally** (top / bottom).
* `Prefix` `o` : Swap/cycle focus to the next pane.
* `Prefix` `Arrow Keys` : Move focus to adjacent pane (Up/Down/Left/Right).
* `Prefix` `z` : Toggle **zoom** on focused pane (full screen toggle).
* `Prefix` `x` : Kill current pane.
* `Prefix` `{` / `}` : Swap current pane with previous / next pane.
* `Prefix` `Space` : Cycle through preset pane layouts.
* `Prefix` `Ctrl+Arrow` : Resize current pane in 1-cell increments.

### Copy / Scroll Mode

* `Prefix` `[` : Enter Copy / Scroll mode.
* Use **Arrow keys** or **Page Up/Down** to navigate buffer.
* Press `Space` to start text selection.
* Press `Enter` to copy selection to buffer and exit copy mode.


* `Prefix` `]` : Paste text from tmux copy buffer.
* `Prefix` `#` : View all buffer history.


## Customization (`~/.tmux.conf`)

Create or edit `~/.tmux.conf` to configure your tmux preferences.

```tmux
# -----------------------------------------------------------------------------
# General Settings
# -----------------------------------------------------------------------------
# Change prefix from Ctrl+b to Ctrl+a (easier to reach)
unbind C-b
set -g prefix C-a
bind C-a send-prefix

# Start window and pane numbering at 1 instead of 0
set -g base-index 1
setw -g pane-base-index 1

# Automatically renumber windows when one is closed
set -g renumber-windows on

# Enable mouse support (clickable windows, panes, resizable borders)
set -g mouse on

# Increase scrollback buffer size (default is 2000 lines)
set -g history-limit 10000

# Faster command sequences (removes delay after ESC)
set -s escape-time 10

# -----------------------------------------------------------------------------
# Key Bindings
# -----------------------------------------------------------------------------
# Reload configuration file with 'Prefix r'
bind r source-file ~/.tmux.conf \; display-message "tmux config reloaded!"

# Intuitive pane splitting (opens in current working directory)
bind | split-window -h -c "#{pane_current_path}"
bind - split-window -v -c "#{pane_current-path}"

# Vim-style pane navigation
bind h select-pane -L
bind j select-pane -D
bind k select-pane -U
bind l select-pane -R

# -----------------------------------------------------------------------------
# Visual Styling & Status Line
# -----------------------------------------------------------------------------
# Enable 256 color terminal support
set -g default-terminal "screen-256color"

# Status bar aesthetic
set -g status-style bg=#1e1e2e,fg=#cdd6f4
set -g status-left "#[fg=#89b4fa,bold] [#S] "
set -g status-right "#[fg=#a6e3a1]%Y-%m-%d %H:%M "
set -g window-status-current-style bg=#89b4fa,fg=#11111b,bold

```
